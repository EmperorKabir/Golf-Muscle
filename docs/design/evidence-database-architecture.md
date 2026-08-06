# Evidence database architecture (T-042 support document)

- Scope: the Stage 0–8 evidence corpus (`docs/research/`, `docs/design/data-programme.md`,
  `docs/design/muscle-zone-list.md`) transcribed into a computable, cross-referenceable store.
- **Not shipped in the app.** Development/analysis artefact only. App consumes a frozen Stage 8 export.
- Owner authorisation: several GB permitted. Priorities, in order: no data loss, no corner-cutting,
  efficiency, structure, cross-referencing, inference support.

## Requirements traceability

| # | Hard requirement | Where satisfied in this design |
|---|---|---|
| 1 | Grain: muscle × side × time window × profile cell × source | `activation_record` table, §Full schema |
| 2 | Five unit families, never silently pooled/converted | `unit_family` lookup + `unit_conversion_rule`/`unit_conversion_application`, §Full schema |
| 3 | Provenance lineage graph, detect reproduction chains | `source_lineage_edge` + recursive CTE, §Lineage graph |
| 4 | Verbatim quote + citation on every record | `verbatim_quote`, `citation_locator` NOT NULL + CHECK, §Full schema |
| 5 | Uncertainty stored, never discarded | `value_low`/`value_high`, `crosstalk_risk`, `contradiction` table, §Full schema |
| 6 | Master timeline in ms + source's own verbatim phase label/definition retained | `phase_definition` + `source_phase_registration`, §Full schema |
| 7 | Sufficiency query, four-way status | §Sufficiency scoring |
| 8 | Inference records, derivation traceable, distinguished from measured | `is_inference`/`derivation_id` + `derivation` table, §Full schema |
| 9 | Append-only, corrections never destroy prior values | Immutability trigger + `record_supersession`, §Full schema |
| 10 | Single-dev, local-first, Windows, git-diffable or documented alternative | §Storage engine, §Backup/versioning |

---

## Storage engine recommendation

### Comparison

| Criterion | SQLite (+JSON1/FTS5) | DuckDB (native .duckdb) | Parquet + DuckDB | PostgreSQL | Plain versioned JSON/CSV |
|---|---|---|---|---|---|
| Analytical query speed at this scale (low millions of rows) | Good — row-store but fine at this volume, indexable | Excellent — vectorised columnar | Excellent for scans; poor for row-level lookups | Good | None — no query engine, hand-rolled scripts only |
| Embeddability (no server process) | Yes — in-process, zero admin | Yes — in-process, zero admin | Yes (via DuckDB) | **No** — requires a running service, port, auth | Yes (trivially, but no engine) |
| Single-file portability | Yes — one `.db` file | Yes — one `.duckdb` file, less mature format history | No — one file per table per snapshot | No — cluster data directory, needs `pg_dump` | Yes, but many small files |
| Schema evolution | Good — `ALTER TABLE`, STRICT tables, CHECK constraints, migrations | Good, `ALTER TABLE` supported | Poor — rewriting Parquet files to change schema | Good | None — no enforced schema at all |
| Git-diffability | Binary file itself: no. Text export (`.dump`/CSV): yes, deterministic | Binary file: no. `EXPORT DATABASE (FORMAT csv)`: yes | Binary Parquet: no | Binary cluster: no: `pg_dump` text is diffable but not row-granular | Yes, natively |
| Tooling maturity (single dev, Windows) | Best-in-class — CLI, DB Browser for SQLite, Python `sqlite3` stdlib, every language binds it | Good, growing fast, CLI + Python/R bindings | Good via DuckDB/Arrow tooling | Heavyweight — pgAdmin, service management, backup tooling | Text editor / git only |
| Constraint enforcement (CHECK, FK, types) | Yes — CHECK, FK (`PRAGMA foreign_keys=ON`), STRICT tables (typed columns, SQLite ≥3.37) | Yes, native typing | None at the file level — whatever wrote the Parquet decided | Yes, most mature of all | **None** — the exact failure mode requirement 2/5/9 forbid |
| Fit for "written rarely, queried heavily, several GB" | Very good | Very good | Very good for read-heavy scans, bad for the append-only correction pattern (whole-file rewrite per correction) | Good but administratively heavy for a one-person project | Poor — no indexing, every query is a full scan by hand |

### Recommendation

- **Primary: SQLite as the single authoritative store, with DuckDB attached as an analytical
  companion — not a separate database.**
- Rationale, strongest reason first: SQLite is the only candidate that gives full constraint
  enforcement (CHECK, FK, STRICT typed columns, generated columns), single-file portability,
  zero server administration, and mature Windows tooling **simultaneously** — the combination the
  "no data loss / no corner-cutting" requirement actually needs. It only underperforms a columnar
  engine on wide aggregate scans, and that gap is closed for free: DuckDB's `sqlite_scanner`
  extension attaches directly to the live `.db` file —
  `ATTACH 'evidence.db' AS ev (TYPE sqlite);` — and queries it with DuckDB's vectorised engine,
  read **and** write, at query time, with zero duplication and zero ETL step (confirmed current
  behaviour via Context7 `/duckdb/duckdb-web`). Stage 3B sufficiency scoring, Stage 4 chain
  cross-checks, and any heavy join/aggregation run through this attachment. SQLite remains the
  single source of truth throughout; DuckDB never holds data SQLite doesn't also hold.
- PostgreSQL is rejected as primary: it requires a running server process, port and auth
  management — exactly the "server administration burden" requirement 10 rules out for a
  single-developer local project. Kept in mind only as a future path if this ever becomes
  multi-user/networked, which is explicitly out of scope.
- Parquet+DuckDB is rejected as primary: Parquet files are effectively immutable per write: every
  correction under the append-only model would mean rewriting whole column files, which is the
  opposite of an efficient correction-heavy workload. Retained in a narrow secondary role below.
- Plain versioned JSON/CSV is rejected as primary: zero constraint enforcement is precisely the
  "silent corner-cut" this project is designed to prevent (a bad unit comparison, a missing
  citation, a cross-family pooled value would all be representable and nothing would refuse them).
  Its genuine strength — git-diffability — is captured instead as an **export target** layered on
  top of SQLite (§Backup/versioning), not as the engine of record.
- **Fallback:** if SQLite ever becomes the bottleneck for a specific heavy analytical pattern
  (unlikely at this row count and with a single user, no write concurrency), migrate the
  authoritative store to a native DuckDB `.duckdb` file. DuckDB supports the same constraint
  vocabulary, and `EXPORT DATABASE 'dir'` (CSV is the **default** format, confirmed via Context7)
  produces exactly the schema.sql + per-table-CSV directory structure needed for the git-diffable
  snapshot described in §Backup/versioning, with `IMPORT DATABASE 'dir'` to restore — a
  documented, tested migration path, not a hand-wave.
- **Secondary, narrow role for Parquet:** Stage 3 per-muscle envelope construction can produce
  dense derived grids (one row per muscle × side × profile cell × ms sample) that are large,
  read-only, fully regenerable from `activation_record`, and never individually corrected. These
  are cached as Parquet (`COPY (SELECT ...) TO 'cache/envelope.parquet' (FORMAT parquet);`),
  rebuilt by a committed script whenever the source rows change, gitignored, and never treated as
  authoritative. This is what keeps the "several GB" allowance efficient without letting a
  disposable derived cache pollute the audited fact store.

## Full schema

- Dialect: SQLite, `STRICT` tables throughout (typed columns, rejects silent coercion —
  SQLite ≥3.37), `PRAGMA foreign_keys = ON` mandatory every connection (off by default in SQLite —
  flagged explicitly because forgetting it silently disables every FK constraint below, which
  would itself be exactly the kind of corner-cut this design forbids).
- All surrogate keys `INTEGER PRIMARY KEY`; the append-only fact table additionally uses
  `AUTOINCREMENT` so no id is ever reused.
- Layout below in five groups: reference/lookup, source/provenance/lineage, units/timeline,
  profile, and the core fact table + its satellite tables (sufficiency, inference, chain-check,
  ingestion/audit). This section (Part A) covers the first three groups.

### Reference / lookup tables

```sql
CREATE TABLE muscle_zone (
    muscle_zone_id   INTEGER PRIMARY KEY,
    canonical_name   TEXT NOT NULL UNIQUE,
    region           TEXT NOT NULL,               -- e.g. 'shoulder_girdle', 'trunk_posterior'
    is_pooled_site   INTEGER NOT NULL DEFAULT 0 CHECK (is_pooled_site IN (0,1)),
    default_tier     TEXT CHECK (default_tier IN ('A','B','C','D')),
    zone_list_ref    TEXT,                        -- pointer back to muscle-zone-list.md row
    anatomical_notes TEXT
) STRICT;

-- Pooled electrode sites (e.g. "wrist and finger flexors") map to the individual muscles
-- they are understood to cover, WITHOUT fabricating a per-muscle value (see §Ingestion pipeline).
CREATE TABLE muscle_zone_pool_member (
    pooled_zone_id INTEGER NOT NULL REFERENCES muscle_zone(muscle_zone_id),
    member_zone_id INTEGER NOT NULL REFERENCES muscle_zone(muscle_zone_id),
    PRIMARY KEY (pooled_zone_id, member_zone_id),
    CHECK (pooled_zone_id != member_zone_id)
) STRICT;

-- Exactly the five incompatible unit families in requirement 2. A new family is a migration,
-- never a free-text value, so "never silently pooled" is enforced by there being nowhere to put
-- an unclassified unit.
CREATE TABLE unit_family (
    unit_family_id   TEXT PRIMARY KEY CHECK (unit_family_id IN
                        ('MMT','MVC','EMGMAX','RAW_UV','ORDINAL')),
    description      TEXT NOT NULL,
    comparison_rule  TEXT NOT NULL   -- human-readable: what tolerance class applies (§Sufficiency)
) STRICT;
```

### Source, provenance and the lineage graph

```sql
CREATE TABLE source (
    source_id       INTEGER PRIMARY KEY,
    citation_short  TEXT NOT NULL,            -- 'Pink, Jobe & Perry 1990'
    citation_full   TEXT NOT NULL,
    year            INTEGER,
    doi             TEXT,
    pmid            TEXT,
    pmcid           TEXT,
    source_type     TEXT NOT NULL CHECK (source_type IN
                        ('peer_reviewed_journal','conference_proceedings','review_secondary',
                         'thesis','clinical_case_report','dataset','other')),
    access_status   TEXT NOT NULL CHECK (access_status IN
                        ('open_access','paywalled_abstract_only','paywalled_no_access',
                         'institutional_access','verified_primary_pdf')),
    local_file_path TEXT,          -- pointer to the PDF/scan on disk; large binaries NEVER
                                    -- stored in the DB itself (§Backup/versioning)
    retrieved_url   TEXT,
    retrieved_date  TEXT,          -- ISO date
    notes           TEXT
) STRICT;

-- Named subject cohorts, so reuse can be detected even when one paper doesn't literally
-- reprint another's table but draws on the same subjects (F-058: Severin/Zhou/Steele).
CREATE TABLE source_cohort (
    cohort_id   INTEGER PRIMARY KEY,
    cohort_name TEXT NOT NULL,
    description TEXT
) STRICT;

CREATE TABLE source_cohort_member (
    source_id INTEGER NOT NULL REFERENCES source(source_id),
    cohort_id INTEGER NOT NULL REFERENCES source_cohort(cohort_id),
    PRIMARY KEY (source_id, cohort_id)
) STRICT;

-- THE LINEAGE GRAPH. Directed edge: child_source reproduces/reuses data whose true origin is
-- parent_source. This is requirement 3, solved explicitly as a graph inside a relational table —
-- see §Lineage graph for the recursive-CTE traversal that turns this into independent-origin counts.
CREATE TABLE source_lineage_edge (
    edge_id             INTEGER PRIMARY KEY,
    child_source_id     INTEGER NOT NULL REFERENCES source(source_id),
    parent_source_id    INTEGER NOT NULL REFERENCES source(source_id),
    relationship_type   TEXT NOT NULL CHECK (relationship_type IN
                            ('reproduces_data','reuses_cohort','partial_reproduction',
                             'cites_only_no_data_reuse')),
    evidence_for_edge    TEXT NOT NULL CHECK (length(evidence_for_edge) > 0),  -- verbatim proof
    asserted_by_source_id INTEGER REFERENCES source(source_id),  -- who did this detective work
    confidence           TEXT NOT NULL CHECK (confidence IN
                            ('confirmed_explicit_citation','inferred_same_cohort',
                             'suspected_unconfirmed')),
    created_at            TEXT NOT NULL DEFAULT (datetime('now')),
    CHECK (child_source_id != parent_source_id)
) STRICT;

CREATE INDEX ix_lineage_child  ON source_lineage_edge(child_source_id);
CREATE INDEX ix_lineage_parent ON source_lineage_edge(parent_source_id);
```

- Cycle prevention: a `CHECK` constraint cannot verify graph-wide acyclicity in SQLite. Stated
  honestly as a process control, not a DB guarantee: the ingestion script runs the same
  `WITH RECURSIVE` traversal used for scoring (§Lineage graph) **before** committing a new edge,
  and refuses the insert if the new parent is already reachable from the new child (i.e. the edge
  would close a cycle). This is documented, scripted and mandatory — not merely advised.

### Units — conversions are explicit, recorded, reversible, never silent

```sql
-- A conversion rule may exist between two families. Absence of a row = conversion forbidden.
CREATE TABLE unit_conversion_rule (
    rule_id             INTEGER PRIMARY KEY,
    from_unit_family_id TEXT NOT NULL REFERENCES unit_family(unit_family_id),
    to_unit_family_id   TEXT NOT NULL REFERENCES unit_family(unit_family_id),
    applicability_scope TEXT NOT NULL,   -- e.g. 'same muscle, same normalisation_ref only'
    formula             TEXT NOT NULL,   -- human-readable AND machine-evaluable expression
    stated_error        TEXT NOT NULL,   -- documented error bound, never omitted
    justification_source_id INTEGER NOT NULL REFERENCES source(source_id),
    reversible          INTEGER NOT NULL CHECK (reversible = 1),  -- non-reversible = not permitted
    created_at          TEXT NOT NULL DEFAULT (datetime('now')),
    created_by          TEXT NOT NULL
) STRICT;

-- An ACTUAL application of a rule to one value. The converted number becomes a NEW
-- activation_record (chained via `derivation`, see Part C) — it never overwrites the original.
CREATE TABLE unit_conversion_application (
    application_id     INTEGER PRIMARY KEY,
    source_record_id   INTEGER NOT NULL,   -- FK to activation_record, added after Part B
    rule_id             INTEGER NOT NULL REFERENCES unit_conversion_rule(rule_id),
    derived_record_id   INTEGER NOT NULL,   -- FK to activation_record, added after Part B
    applied_at           TEXT NOT NULL DEFAULT (datetime('now')),
    CHECK (source_record_id != derived_record_id)
) STRICT;
```

### Master timeline and verbatim phase registration

```sql
CREATE TABLE timeline_master (
    timeline_id       INTEGER PRIMARY KEY,
    label             TEXT NOT NULL UNIQUE,        -- 'master_v1_full_swing'
    t_zero_definition TEXT NOT NULL,                -- verbatim: what real-world event is t=0
    t_end_ms          INTEGER NOT NULL,
    notes             TEXT
) STRICT;

-- Named instants (address, top, impact...) that are boundary INSTANTS, never sampled bins (F-014).
CREATE TABLE timeline_event (
    event_id               INTEGER PRIMARY KEY,
    timeline_id             INTEGER NOT NULL REFERENCES timeline_master(timeline_id),
    event_name               TEXT NOT NULL,
    t_ms                      INTEGER,               -- NULL if only a range is known
    t_ms_range_low            INTEGER,
    t_ms_range_high           INTEGER,
    is_interpolated_boundary INTEGER NOT NULL DEFAULT 0 CHECK (is_interpolated_boundary IN (0,1)),
    UNIQUE (timeline_id, event_name)
) STRICT;

-- Every source's own phase scheme, kept distinct (Kim's split-takeaway scheme must never be
-- merged cell-to-cell with McHardy's five-phase scheme).
CREATE TABLE phase_scheme (
    phase_scheme_id INTEGER PRIMARY KEY,
    scheme_name       TEXT NOT NULL,
    defining_source_id INTEGER REFERENCES source(source_id),
    n_phases            INTEGER NOT NULL
) STRICT;

-- The source's OWN printed label and OWN printed boundary definition, verbatim. Requirement 6.
CREATE TABLE phase_definition (
    phase_definition_id INTEGER PRIMARY KEY,
    phase_scheme_id       INTEGER NOT NULL REFERENCES phase_scheme(phase_scheme_id),
    phase_label             TEXT NOT NULL,             -- verbatim, e.g. 'Acceleration'
    printed_definition       TEXT NOT NULL CHECK (length(printed_definition) > 0),  -- verbatim
    boundary_kind             TEXT NOT NULL DEFAULT 'sampled_bin'
                                 CHECK (boundary_kind IN ('sampled_bin','instant')),
    UNIQUE (phase_scheme_id, phase_label)
) STRICT;

-- Stage 2: registers a phase_definition onto the master timeline using the SOURCE's own
-- boundary definition. Registering the PHASE (not each record) means a Stage 2 correction
-- automatically propagates to every activation_record that cites this phase_definition, without
-- ever touching activation_record itself (see Part B's normalisation note).
CREATE TABLE source_phase_registration (
    registration_id          INTEGER PRIMARY KEY,
    phase_definition_id        INTEGER NOT NULL REFERENCES phase_definition(phase_definition_id),
    timeline_id                 INTEGER NOT NULL REFERENCES timeline_master(timeline_id),
    t_start_ms                   INTEGER,
    t_end_ms                     INTEGER,
    t_start_ms_range_low         INTEGER,     -- ambiguity stored as a range, never collapsed
    t_start_ms_range_high        INTEGER,
    t_end_ms_range_low           INTEGER,
    t_end_ms_range_high          INTEGER,
    is_interpolated_boundary     INTEGER NOT NULL DEFAULT 0 CHECK (is_interpolated_boundary IN (0,1)),
    registration_method           TEXT NOT NULL,   -- e.g. 'verbatim ms given by source'
    registered_by                  TEXT NOT NULL,
    registered_at                   TEXT NOT NULL DEFAULT (datetime('now')),
    superseded_by_registration_id   INTEGER REFERENCES source_phase_registration(registration_id),
    is_current                       INTEGER NOT NULL DEFAULT 1 CHECK (is_current IN (0,1))
) STRICT;

-- Exactly one CURRENT registration per phase_definition at a time.
CREATE UNIQUE INDEX ux_registration_current
    ON source_phase_registration(phase_definition_id) WHERE is_current = 1;

CREATE TRIGGER trg_registration_supersede
AFTER UPDATE OF superseded_by_registration_id ON source_phase_registration
WHEN NEW.superseded_by_registration_id IS NOT NULL
BEGIN
    UPDATE source_phase_registration SET is_current = 0 WHERE registration_id = NEW.registration_id;
END;
```

### Profile dimensions (D-011 — first-class from the outset)

```sql
-- One row per distinct combination actually used. 'unspecified' is a real, distinct value —
-- never conflated with a value that was pooled away by a collapse rule (see below).
CREATE TABLE profile_cell (
    profile_cell_id   INTEGER PRIMARY KEY,
    sex                 TEXT NOT NULL CHECK (sex IN ('male','female','unspecified')),
    stature_cm           INTEGER,               -- actual value where reported
    stature_band          TEXT,                 -- band where only a band was reported
    limb_proportion        TEXT,                 -- femur/torso ratio, almost never reported (F-003)
    skill                   TEXT NOT NULL CHECK (skill IN
                               ('professional','low_handicap','mid_handicap','high_handicap',
                                'unspecified')),
    club                     TEXT NOT NULL CHECK (club IN
                               ('driver','long_iron','mid_iron','short_iron','wedge','putter',
                                'unspecified')),
    shot_type                 TEXT NOT NULL CHECK (shot_type IN
                               ('full','three_quarter','punch','pitch','chip','bunker','shaped',
                                'unspecified')),
    handedness                 TEXT NOT NULL CHECK (handedness IN ('right','left','unspecified')),
    age_band                    TEXT,
    UNIQUE (sex, stature_cm, stature_band, limb_proportion, skill, club, shot_type, handedness,
            age_band)
) STRICT;

-- Every evidence-based pooling decision (F-002/F-006/F-019/F-005-style), recorded as a rule with
-- its justifying finding, and reversible (requirement: collapses are never silent or permanent-by-default).
CREATE TABLE profile_collapse_rule (
    collapse_rule_id   INTEGER PRIMARY KEY,
    dimension_collapsed  TEXT NOT NULL,      -- e.g. 'club'
    applies_to_muscle_zone_id INTEGER REFERENCES muscle_zone(muscle_zone_id),
    applies_to_region          TEXT,          -- e.g. 'trunk' when scoped by region not one zone
    justifying_finding_code     TEXT NOT NULL, -- e.g. 'F-002', cross-referenced to TASKS.md
    justifying_source_id         INTEGER REFERENCES source(source_id),
    rule_text                     TEXT NOT NULL CHECK (length(rule_text) > 0),
    active                         INTEGER NOT NULL DEFAULT 1 CHECK (active IN (0,1)),
    superseded_by_collapse_rule_id INTEGER REFERENCES profile_collapse_rule(collapse_rule_id),
    created_at                       TEXT NOT NULL DEFAULT (datetime('now')),
    CHECK (applies_to_muscle_zone_id IS NOT NULL OR applies_to_region IS NOT NULL)
) STRICT;
```

### The core fact table

- Grain: exactly requirement 1 — one row per (muscle × side × phase/time-window × profile cell ×
  source), disambiguated further by `citation_locator` so two distinct table cells in the same
  paper for the same grain don't collide.
- **Timeline normalisation choice, stated explicitly:** `activation_record` references
  `phase_definition_id`, not a per-record ms window directly. The real-ms window is always
  resolved by joining to the **current** `source_phase_registration` row for that phase
  definition. This means a Stage 2 correction (a re-registration) automatically applies to every
  record that cites the phase, with no update to `activation_record` at all — and a record that
  hasn't been registered yet simply has no current registration to join to, so it is captured
  (Stage 0) without being forced to wait for Stage 2 to complete, while being naturally excluded
  from any timeline-dependent query (including sufficiency scoring) until it is registered.

```sql
CREATE TABLE activation_record (
    record_id            INTEGER PRIMARY KEY AUTOINCREMENT,

    muscle_zone_id         INTEGER NOT NULL REFERENCES muscle_zone(muscle_zone_id),
    side                     TEXT NOT NULL CHECK (side IN ('lead','trail','midline','unspecified')),
    phase_definition_id       INTEGER NOT NULL REFERENCES phase_definition(phase_definition_id),
    profile_cell_id             INTEGER NOT NULL REFERENCES profile_cell(profile_cell_id),
    source_id                     INTEGER NOT NULL REFERENCES source(source_id),

    -- value: a point OR a range, never a fabricated midpoint of a range (see §Ingestion pipeline)
    value                     REAL,
    value_low                  REAL,
    value_high                   REAL,
    unit_family_id                 TEXT NOT NULL REFERENCES unit_family(unit_family_id),
    normalisation_ref                TEXT NOT NULL CHECK (length(normalisation_ref) > 0),
    comparison_key GENERATED ALWAYS AS (unit_family_id || '::' || normalisation_ref) STORED,

    electrode_type              TEXT NOT NULL CHECK (electrode_type IN
                                   ('surface','fine_wire','indwelling','ultrasound_proxy',
                                    'model_estimate','not_applicable')),
    crosstalk_risk                TEXT NOT NULL DEFAULT 'none_stated'
                                   CHECK (crosstalk_risk IN ('none_stated','low','moderate','high')),
    crosstalk_note                  TEXT,

    n_subjects                        INTEGER,
    population_note                     TEXT,

    contraction_mode                     TEXT NOT NULL DEFAULT 'unassigned' CHECK (contraction_mode IN
                                          ('unassigned','concentric','eccentric','isometric',
                                           'ambiguous_biarticular')),   -- Stage 4 sets this; see trigger below

    confidence_tier                        TEXT NOT NULL CHECK (confidence_tier IN ('A','B','C','D')),

    verbatim_quote                           TEXT NOT NULL CHECK (length(verbatim_quote) > 0),
    citation_locator                           TEXT NOT NULL CHECK (length(citation_locator) > 0),

    is_inference                                 INTEGER NOT NULL DEFAULT 0 CHECK (is_inference IN (0,1)),
    derivation_id                                  INTEGER REFERENCES derivation(derivation_id),

    pooled_electrode_site                            INTEGER NOT NULL DEFAULT 0
                                                      CHECK (pooled_electrode_site IN (0,1)),

    record_status                                      TEXT NOT NULL DEFAULT 'active'
                                                      CHECK (record_status IN ('active','superseded','retracted')),
    retraction_reason                                    TEXT,

    ingestion_batch_id                                     INTEGER NOT NULL REFERENCES ingestion_batch(batch_id),
    entered_by                                               TEXT NOT NULL,
    entered_at                                                 TEXT NOT NULL DEFAULT (datetime('now')),

    UNIQUE (muscle_zone_id, side, phase_definition_id, profile_cell_id, source_id, citation_locator),
    CHECK (value IS NOT NULL OR (value_low IS NOT NULL AND value_high IS NOT NULL)),
    CHECK ( (is_inference = 0 AND derivation_id IS NULL)
         OR (is_inference = 1 AND derivation_id IS NOT NULL) ),
    CHECK ( (record_status = 'retracted' AND retraction_reason IS NOT NULL AND length(retraction_reason) > 0)
         OR (record_status != 'retracted') )
) STRICT;

CREATE INDEX ix_ar_muscle_side_profile ON activation_record(muscle_zone_id, side, profile_cell_id);
CREATE INDEX ix_ar_source   ON activation_record(source_id);
CREATE INDEX ix_ar_phasedef ON activation_record(phase_definition_id);
CREATE INDEX ix_ar_compkey  ON activation_record(comparison_key);
CREATE INDEX ix_ar_status   ON activation_record(record_status);
```

- `muscle_zone`, `phase_definition`, `source`, `unit_family`, `derivation`, `ingestion_batch` are
  forward/backward references resolved by table creation order in the actual migration script
  (`derivation` and `ingestion_batch` are defined in Part C below; SQLite allows this via deferred
  FK creation in a single migration transaction).

#### Append-only enforcement — the concrete guarantee behind requirement 9

```sql
-- Core evidentiary fields are immutable once inserted. A "correction" is always a NEW row,
-- linked back via record_supersession. This is enforced at the database layer, not by policy alone.
CREATE TRIGGER trg_activation_record_immutable
BEFORE UPDATE OF muscle_zone_id, side, phase_definition_id, profile_cell_id, source_id,
                  value, value_low, value_high, unit_family_id, normalisation_ref,
                  electrode_type, crosstalk_risk, n_subjects, confidence_tier,
                  verbatim_quote, citation_locator, is_inference, derivation_id,
                  pooled_electrode_site
ON activation_record
BEGIN
    SELECT RAISE(ABORT,
        'activation_record core fields are immutable; insert a corrected row and link it via record_supersession');
END;

-- Mutable exceptions, each with its own audit path:
--   record_status / retraction_reason  -> changed directly (retraction), or flipped by the
--                                         trigger below when a supersession is recorded.
--   contraction_mode                   -> Stage 4's own annotation layer, NOT part of the
--                                         verbatim measured evidence. Changeable directly, but
--                                         every change is logged to chain_check automatically.

CREATE TABLE record_supersession (
    supersession_id INTEGER PRIMARY KEY AUTOINCREMENT,
    old_record_id     INTEGER NOT NULL REFERENCES activation_record(record_id),
    new_record_id       INTEGER NOT NULL REFERENCES activation_record(record_id),
    reason                 TEXT NOT NULL CHECK (length(reason) > 0),
    corrected_by             TEXT NOT NULL,
    corrected_at               TEXT NOT NULL DEFAULT (datetime('now')),
    CHECK (old_record_id != new_record_id)
) STRICT;

CREATE TRIGGER trg_supersession_flip_status
AFTER INSERT ON record_supersession
BEGIN
    UPDATE activation_record SET record_status = 'superseded' WHERE record_id = NEW.old_record_id;
END;

CREATE TRIGGER trg_contraction_mode_audit
BEFORE UPDATE OF contraction_mode ON activation_record
WHEN OLD.contraction_mode != NEW.contraction_mode
BEGIN
    INSERT INTO chain_check (activation_record_id, check_type, outcome, detail, checked_at)
    VALUES (OLD.record_id, 'sequence_timing_or_moment_arm',
            CASE WHEN OLD.contraction_mode = 'unassigned' THEN 'corroborated' ELSE 'reassigned' END,
            'contraction_mode: ' || OLD.contraction_mode || ' -> ' || NEW.contraction_mode,
            datetime('now'));
END;

-- Pooled electrode sites must have a declared mapping before a record can claim to be pooled —
-- prevents an unexplained pooled value being silently attributed as if it were a clean single-muscle reading.
CREATE TRIGGER trg_pooled_site_requires_mapping
BEFORE INSERT ON activation_record
WHEN NEW.pooled_electrode_site = 1
BEGIN
    SELECT RAISE(ABORT, 'pooled_electrode_site=1 requires a muscle_zone_pool_member row for this muscle_zone_id')
    WHERE NOT EXISTS (SELECT 1 FROM muscle_zone_pool_member m WHERE m.pooled_zone_id = NEW.muscle_zone_id);
END;
```

#### Full-text search on the verbatim anchor (FTS5, external-content — no duplicated storage)

```sql
CREATE VIRTUAL TABLE activation_record_fts USING fts5(
    verbatim_quote, citation_locator,
    content='activation_record', content_rowid='record_id'
);

-- Records are never UPDATEd on these columns (guarded above) and never DELETEd (retraction only
-- flips a status flag), so only an AFTER INSERT sync trigger is required — no update/delete triggers.
CREATE TRIGGER trg_ar_fts_insert AFTER INSERT ON activation_record BEGIN
    INSERT INTO activation_record_fts(rowid, verbatim_quote, citation_locator)
    VALUES (new.record_id, new.verbatim_quote, new.citation_locator);
END;
```

#### Safe-by-construction comparison views

```sql
-- The sanctioned path for any cross-record numeric comparison: only pairs sharing BOTH unit
-- family AND normalisation reference are ever joined. Ad hoc SQL could still bypass this by
-- querying activation_record directly — documented as a residual risk, see §Design risks.
CREATE VIEW v_comparable_pairs AS
SELECT a.record_id AS record_id_a, b.record_id AS record_id_b,
       a.muscle_zone_id, a.side, a.unit_family_id, a.normalisation_ref
FROM activation_record a
JOIN activation_record b
  ON a.muscle_zone_id = b.muscle_zone_id
 AND a.side = b.side
 AND a.record_id < b.record_id
 AND a.comparison_key = b.comparison_key
WHERE a.record_status = 'active' AND b.record_status = 'active';

CREATE VIEW v_current_activation_record AS
SELECT * FROM activation_record WHERE record_status = 'active';
```

### Inference / derivation (requirement 8)

```sql
-- HOW an inferred/derived record was produced, whatever the route: Stage 6 bounded inference,
-- a unit conversion, a Stage 3 interpolated curve point, or a Stage 4 contraction-mode call.
CREATE TABLE derivation (
    derivation_id       INTEGER PRIMARY KEY,
    derivation_kind        TEXT NOT NULL CHECK (derivation_kind IN
                              ('mechanical_necessity','anatomical_obligation','analogue_transfer',
                               'unit_conversion','curve_interpolation','other_reasoned')),
    method_description       TEXT NOT NULL CHECK (length(method_description) > 0),
    input_record_ids           TEXT NOT NULL,   -- JSON1 array of activation_record.record_id
    input_derivation_ids         TEXT,          -- JSON1 array, for inference-on-inference chains
    uncertainty_note               TEXT NOT NULL CHECK (length(uncertainty_note) > 0),
    produced_by                      TEXT NOT NULL,
    produced_at                        TEXT NOT NULL DEFAULT (datetime('now')),
    validated_by_holdout                 INTEGER NOT NULL DEFAULT 0 CHECK (validated_by_holdout IN (0,1)),
    holdout_agreement_note                 TEXT
) STRICT;

-- Example traversal: every activation_record feeding a given inference, via JSON1 (confirmed
-- current syntax via Context7 /websites/devdocs_io_sqlite):
--   SELECT ar.* FROM activation_record ar, json_each(
--       (SELECT input_record_ids FROM derivation WHERE derivation_id = :id)
--   ) j WHERE ar.record_id = j.value;
```

### Kinematic chain cross-checks and contradiction audit (Stage 4/5)

```sql
CREATE TABLE chain_check (
    check_id                INTEGER PRIMARY KEY,
    activation_record_id       INTEGER NOT NULL REFERENCES activation_record(record_id),
    check_type                    TEXT NOT NULL CHECK (check_type IN
                                     ('joint_motion_direction','moment_arm_sign','sequence_timing',
                                      'sequence_timing_or_moment_arm')),
    outcome                          TEXT NOT NULL CHECK (outcome IN
                                     ('corroborated','reassigned','contradiction_flagged')),
    detail                             TEXT,
    checked_at                           TEXT NOT NULL DEFAULT (datetime('now'))
) STRICT;

-- Requirement 5: disagreements are stored, never averaged away.
CREATE TABLE contradiction (
    contradiction_id  INTEGER PRIMARY KEY,
    record_id_a          INTEGER NOT NULL REFERENCES activation_record(record_id),
    record_id_b            INTEGER NOT NULL REFERENCES activation_record(record_id),
    resolved_cause            TEXT NOT NULL DEFAULT 'unresolved' CHECK (resolved_cause IN
                                 ('unit_normalisation_error','phase_misregistration',
                                  'crosstalk_contamination','genuine_population_difference',
                                  'genuine_literature_dispute','unresolved')),
    resolution_note              TEXT,
    flagged_at                      TEXT NOT NULL DEFAULT (datetime('now')),
    resolved_at                       TEXT,
    CHECK (record_id_a != record_id_b)
) STRICT;
```

### Sufficiency scoring (requirement 7 — full computation in §Sufficiency scoring)

```sql
-- Tunable, versioned, never hard-coded (Stage 3B explicitly requires this).
CREATE TABLE sufficiency_tolerance_param (
    param_id           INTEGER PRIMARY KEY,
    data_class            TEXT NOT NULL CHECK (data_class IN
                             ('same_unit_same_norm','cross_percent_family','raw_uv_shape',
                              'ordinal','timing')),
    param_name              TEXT NOT NULL,
    param_value                REAL NOT NULL,
    param_unit                   TEXT,
    version                        INTEGER NOT NULL,
    effective_from                   TEXT NOT NULL DEFAULT (datetime('now')),
    superseded_by_param_id              INTEGER REFERENCES sufficiency_tolerance_param(param_id)
) STRICT;

-- Permanent "physically unmeasurable" status (the fourth, non-looping status). Requirement:
-- "marked permanently unmeasurable, never pending."
CREATE TABLE irreducibility_declaration (
    declaration_id     INTEGER PRIMARY KEY,
    muscle_zone_id         INTEGER NOT NULL REFERENCES muscle_zone(muscle_zone_id),
    side                      TEXT CHECK (side IN ('lead','trail','midline','unspecified')),  -- NULL = both
    reason                      TEXT NOT NULL CHECK (length(reason) > 0),
    justifying_source_id           INTEGER NOT NULL REFERENCES source(source_id),
    declared_at                       TEXT NOT NULL DEFAULT (datetime('now'))
) STRICT;

-- A REBUILDABLE CACHE, not authoritative — always reproducible from activation_record + the
-- lineage graph + the current tolerance parameters. History retained (not overwritten) so the
-- collection loop's progress over time is itself visible.
CREATE TABLE sufficiency_score (
    score_id                    INTEGER PRIMARY KEY,
    muscle_zone_id                  INTEGER NOT NULL REFERENCES muscle_zone(muscle_zone_id),
    side                               TEXT NOT NULL CHECK (side IN ('lead','trail','midline','unspecified')),
    timeline_id                          INTEGER NOT NULL REFERENCES timeline_master(timeline_id),
    t_window_start_ms                       INTEGER NOT NULL,
    t_window_end_ms                           INTEGER NOT NULL,
    profile_cell_id                              INTEGER NOT NULL REFERENCES profile_cell(profile_cell_id),
    n_sources_independent                          INTEGER NOT NULL,
    n_subjects_pooled                                INTEGER,
    concordance                                        REAL,
    unit_spread                                          INTEGER NOT NULL,
    method_spread                                          INTEGER NOT NULL,
    crosstalk_flag                                           INTEGER NOT NULL CHECK (crosstalk_flag IN (0,1)),
    status                                                     TEXT NOT NULL CHECK (status IN
                                                                  ('sufficient','provisional','insufficient','irreducible')),
    deficiency_reason                                            TEXT,
    contributing_record_ids                                        TEXT NOT NULL,  -- JSON1 array, traceability
    tolerance_param_version                                          INTEGER NOT NULL,
    scored_at                                                          TEXT NOT NULL DEFAULT (datetime('now')),
    is_current                                                           INTEGER NOT NULL DEFAULT 1 CHECK (is_current IN (0,1))
) STRICT;

CREATE INDEX ix_suff_lookup ON sufficiency_score(muscle_zone_id, side, profile_cell_id, is_current);
```

### Ingestion and audit infrastructure

```sql
CREATE TABLE ingestion_batch (
    batch_id        INTEGER PRIMARY KEY,
    source_id           INTEGER NOT NULL REFERENCES source(source_id),
    started_at             TEXT NOT NULL DEFAULT (datetime('now')),
    completed_at             TEXT,
    records_created             INTEGER,
    ingested_by                   TEXT NOT NULL,
    notes                           TEXT
) STRICT;

-- Generic append-only audit trail, layered on top of the more specific mechanisms above
-- (defence in depth for requirement 9).
CREATE TABLE audit_log (
    audit_id     INTEGER PRIMARY KEY AUTOINCREMENT,
    table_name       TEXT NOT NULL,
    row_id               INTEGER NOT NULL,
    action                  TEXT NOT NULL CHECK (action IN ('insert','correction','retraction','supersession')),
    changed_at                 TEXT NOT NULL DEFAULT (datetime('now')),
    changed_by                    TEXT NOT NULL,
    detail_json                      TEXT
) STRICT;

CREATE TABLE schema_migration (
    version      INTEGER PRIMARY KEY,
    applied_at       TEXT NOT NULL DEFAULT (datetime('now')),
    description         TEXT NOT NULL
) STRICT;
```

## Lineage graph — solving requirement 3 explicitly

- The problem restated: source C (e.g. Kim 2004) may reproduce source B (e.g. McHardy 2005) which
  reproduces source A (e.g. Kao 1995) — three citations, one underlying measurement of the world.
  Counting all three as independent corroboration is self-deception (F-051).
- Solved as a directed graph (`source_lineage_edge`, child → parent = "reproduces/reuses"), with
  independent-origin counting computed by finding each source's **root(s)** — a source with no
  outgoing `reproduces_data`/`reuses_cohort` edge — via `WITH RECURSIVE` (SQLite and DuckDB both
  support this; syntax confirmed current via Context7 `/duckdb/duckdb-web`, which documents the
  identical cycle-safe pattern used here).

```sql
WITH RECURSIVE origin(source_id, root_id) AS (
    -- Base case: a source with no reproduces/reuses edge is its own root.
    SELECT s.source_id, s.source_id
    FROM source s
    WHERE NOT EXISTS (
        SELECT 1 FROM source_lineage_edge e
        WHERE e.child_source_id = s.source_id
          AND e.relationship_type IN ('reproduces_data','reuses_cohort')
    )
    UNION
    -- Recursive case: follow child -> parent edges outward to find deeper roots.
    SELECT e.child_source_id, o.root_id
    FROM source_lineage_edge e
    JOIN origin o ON o.source_id = e.parent_source_id
    WHERE e.relationship_type IN ('reproduces_data','reuses_cohort')
)
SELECT * FROM origin;
```

- A source can resolve to more than one root (rare: a review that synthesises two independent
  prior origins into one printed figure) — this is retained as multiple rows, not collapsed to
  one, so that case is visible rather than silently resolved.
- **Independent origin count** for any set of contributing records = `COUNT(DISTINCT root_id)`
  among the roots reachable from their `source_id`s.
- **Cycle safety at write time:** before inserting a new `source_lineage_edge`, the ingestion
  script runs the same traversal starting from the proposed `parent_source_id` and refuses the
  insert if it reaches the proposed `child_source_id` (which would make the graph cyclic — two
  sources claiming to reproduce each other). SQLite cannot express "this insert must not close a
  cycle" as a `CHECK` constraint, so this is a scripted precondition, stated as such rather than
  implied to be a database-level guarantee.
- `source_cohort` / `source_cohort_member` extend the same idea to shared-subject reuse that
  never shows up as a citation relationship at all (F-058's Severin/Zhou/Steele case): a cell's
  independent-origin count treats two sources sharing a `cohort_id` as a single origin, exactly
  as it treats two sources connected by a `reproduces_data` edge.

## Sufficiency scoring — the actual computation (requirement 7)

- Run as an offline batch job (`scripts/score_sufficiency.py` or a DuckDB SQL script attached to
  the SQLite file), triggered as the mandatory last step of every ingestion batch and every new
  `source_lineage_edge` — **not** a live per-row trigger, because the computation spans lineage
  traversal, tolerance-band logic and cross-family magnitude banding that don't belong in a
  row-level trigger. This keeps `sufficiency_score` a cache that can go stale between batches;
  §Design risks names this explicitly as a residual risk to guard against operationally.
- Scored at the grain fixed by Stage 3B: muscle × side × time window × profile cell, **after**
  applying any currently-`active` `profile_collapse_rule` (scoring a pooled cell with no active
  rule justifying the pool is explicitly forbidden — see §Validation constraints).

### Step 1 — gather contributing records for one target cell

```sql
WITH cell_records AS (
    SELECT ar.*
    FROM activation_record ar
    JOIN source_phase_registration spr
      ON spr.phase_definition_id = ar.phase_definition_id AND spr.is_current = 1
    WHERE ar.muscle_zone_id = :muscle_zone_id
      AND ar.side           = :side
      AND ar.record_status   = 'active'
      AND spr.t_start_ms      < :window_end_ms
      AND spr.t_end_ms          > :window_start_ms
      AND ar.profile_cell_id IN (
            -- direct match, OR a profile cell legitimised into this target cell by an
            -- active collapse rule scoped to this muscle/region (view defined in the
            -- ingestion/collapse tooling; joins profile_cell against profile_collapse_rule)
            SELECT profile_cell_id FROM v_pool_eligible_cells
            WHERE target_profile_cell_id = :profile_cell_id
              AND muscle_zone_id = :muscle_zone_id
      )
),
```

### Step 2 — resolve independent origins (lineage collapse, §Lineage graph)

```sql
origin AS ( /* the WITH RECURSIVE block from §Lineage graph */ ),
rooted AS (
    SELECT cr.*, o.root_id
    FROM cell_records cr
    JOIN origin o ON o.source_id = cr.source_id
),
-- One representative n per origin (not summed across every reproduction of the same origin,
-- which would silently multiply-count a single cohort's subjects).
per_root AS (
    SELECT root_id, MAX(n_subjects) AS n_subjects_for_root,
           MIN(comparison_key)      AS a_comparison_key   -- probe value, refined in Step 3
    FROM rooted
    GROUP BY root_id
)
```

### Step 3 — concordance, by data class (tolerance bands from `sufficiency_tolerance_param`)

| Data class | Rule applied to one representative value per independent root |
|---|---|
| Same unit family, same `normalisation_ref` | Agree if within ±15 percentage points OR ±20% of the consensus (median of the roots), whichever is larger |
| Different units, all within the %-family (MMT/MVC/EMGMAX) | Map each to a magnitude band (`<20` low / `20–40` moderate / `40–60` high / `>60` very high — general sports-EMG convention, explicitly **not** traceable to a golf source, per F-029; the DB carries that caveat in `unit_family.comparison_rule`) — agree if same or adjacent band |
| Raw µV | Shape only: rank-order of phases and peak-phase match, and only between records sharing the same `phase_scheme_id` — magnitude comparison is refused outright (F-016) |
| Ordinal | Agree if same or adjacent ordinal level |
| Timing (onset/offset/peak) | Agree if within ±1 phase or ±40 ms on the registered master timeline |

```sql
concordant AS (
    SELECT root_id
    FROM per_root
    WHERE /* tolerance test per the table above, parameterised from
             sufficiency_tolerance_param WHERE data_class = <resolved class> */
),
scored AS (
    SELECT
        (SELECT COUNT(*) FROM per_root)                          AS n_sources_independent,
        (SELECT SUM(n_subjects_for_root) FROM per_root)           AS n_subjects_pooled,
        CAST((SELECT COUNT(*) FROM concordant) AS REAL)
            / NULLIF((SELECT COUNT(*) FROM per_root), 0)           AS concordance,
        (SELECT COUNT(DISTINCT unit_family_id) FROM rooted)         AS unit_spread,
        (SELECT COUNT(DISTINCT electrode_type) FROM rooted)          AS method_spread,
        (SELECT MAX(CASE WHEN crosstalk_risk IN ('moderate','high')
                          THEN 1 ELSE 0 END) FROM rooted)              AS crosstalk_flag
)
```

### Step 4 — four-way status (transcribed directly from Stage 3B)

```sql
SELECT
  CASE
    WHEN n_sources_independent = 0
         THEN 'insufficient'   -- zero data at this cell; see irreducibility check below first
    WHEN EXISTS (SELECT 1 FROM irreducibility_declaration ir
                 WHERE ir.muscle_zone_id = :muscle_zone_id
                   AND (ir.side = :side OR ir.side IS NULL))
         THEN 'irreducible'
    WHEN n_sources_independent >= 3 AND concordance >= 0.85 AND n_subjects_pooled >= 20
         THEN 'sufficient'
    WHEN n_sources_independent = 2 OR (concordance BETWEEN 0.60 AND 0.85)
         THEN 'provisional'
    ELSE 'insufficient'   -- 1 origin, OR concordance < 0.60, OR unresolved timing contradiction
  END AS status
FROM scored;
```

- The `irreducibility_declaration` check runs **before** the numeric thresholds so a muscle that
  is both zero-data and physically unmeasurable (diaphragm, pelvic floor) is correctly labelled
  `irreducible`, not `insufficient` — the distinction Stage 3B added specifically so the
  collection loop terminates rather than perpetually re-flagging an unmeasurable zone.
- An unresolved timing contradiction additionally forces `insufficient` regardless of the
  concordance number: join against `contradiction` where `resolved_cause = 'unresolved'` and
  either endpoint record is in `rooted`.
- `deficiency_reason` (populated for `provisional`/`insufficient`) names the exact failing
  criterion in text (e.g. `"1 independent origin (need >=2)"`, `"concordance 0.42 < 0.60"`,
  `"unit_spread=3, no conversion rule between EMGMAX and RAW_UV"`) — this is what feeds the
  targeted-collection ledger (T-054): the next research round is told precisely what is missing,
  never "go find more on muscle X" in general.

## Ingestion pipeline — research document to records, without losing the anchor

- Unit of work: one `ingestion_batch` per source document per pass, wrapped in a single SQL
  transaction (`BEGIN` … `COMMIT`), so a crash mid-ingestion leaves the batch entirely absent, not
  half-written — never a partially-ingested source.

1. **Register the source.** Insert/confirm `source` (citation, DOI/PMID if any, `access_status`).
   If the document is a PDF/scan, store it on disk and point `source.local_file_path` at it — the
   binary is never stored inside the database (§Backup/versioning explains why).
2. **Register the phase scheme.** If this source introduces a phase taxonomy not already in
   `phase_scheme`/`phase_definition`, insert it once, transcribing the source's own printed
   boundary definition verbatim into `printed_definition`. Reused by every record from this
   source. Timeline registration (Stage 2, `source_phase_registration`) can happen later — the
   Stage 0 schema fields do not require it, only Stage 3B scoring and rendering do.
3. **For each numeric/qualitative value in the source:**
   - Resolve `muscle_zone_id` against the canonical `muscle_zone` table. If the source used a
     pooled electrode site (e.g. Glazebrook's "wrist and finger flexors"), point at the **pooled**
     zone row and set `pooled_electrode_site = 1` — never attribute a pooled reading to one
     individual muscle (`muscle_zone_pool_member` records what the pool is understood to cover;
     the enforcement trigger refuses the insert if that mapping doesn't already exist).
   - Copy the exact sentence/table cell(s) into `verbatim_quote`; record a precise
     `citation_locator` ("Table 3, row Infraspinatus, column Lead/Early Follow-Through").
   - Classify `unit_family_id` strictly from what the source states. If the source's unit is
     ambiguous or unstated, ingestion for that value **halts** rather than defaulting to a guess
     — `unit_family_id` is `NOT NULL` with no catch-all value to fall back to, so an unclassified
     unit has nowhere to go until a human resolves it (recorded instead as a `source.notes` flag
     for follow-up).
   - Copy `normalisation_ref` verbatim from the source's methods (how 100% was defined); for raw
     µV/ordinal data, state explicitly "not applicable, raw amplitude" rather than leaving blank
     — enforced by the `NOT NULL CHECK (length(...) > 0)` constraint.
   - **Point value vs range** (explicit requirement): if the source prints one number, set
     `value`; if it prints a range (e.g. Li 2023's "13–52% MVC"), set `value_low`/`value_high` to
     the printed bounds exactly and leave `value` NULL. **No midpoint is computed or stored in
     this row.** If a single representative number is later needed for a specific purpose (e.g. a
     colour-ramp anchor), it is created as a **separate** `activation_record` with
     `is_inference = 1` and a `derivation` row of kind `other_reasoned` pointing back at the range
     record — so the range and any convenience midpoint remain distinguishable and both traceable,
     never silently merged into one number.
   - Set `electrode_type`, `crosstalk_risk`/`crosstalk_note` (from the source's own methods or a
     cross-referenced finding such as F-039), `n_subjects`, `population_note`, and resolve/insert
     the matching `profile_cell` row across all eight profile fields — most sources under-specify
     several of these, which correctly resolve to `'unspecified'`, never guessed.
   - `contraction_mode` is always inserted as `'unassigned'` — Stage 4 is the only writer of any
     other value, via the audited direct-update path (§Full schema), never at ingestion time.
   - `confidence_tier` assigned per the A/B/C/D rules already fixed in
     `docs/design/muscle-zone-list.md`; a record that would change a zone's published tier is a
     flag to reconcile that document, not a silent divergence between the two artefacts.
4. **Pooled electrode sites covering several muscles** (explicit requirement): the pooled value
   is inserted once, against the pooled `muscle_zone` row, with its coverage declared in
   `muscle_zone_pool_member`. Individual-muscle records from *other* sources that did isolate one
   muscle (e.g. Farber 2009 fine-wire on pronator teres alone) are ordinary, independent
   `activation_record` rows against the individual zone — the pooled and individual readings are
   never merged, averaged, or used to back-fill each other.
5. **Lineage detection is part of ingestion, not an afterthought.** While reading a new source,
   any statement that it reproduces or reuses another source's data/cohort is captured
   immediately as a `source_lineage_edge` (with `evidence_for_edge` quoting the source's own
   acknowledgement, e.g. a table captioned "adapted from Kao et al. 1995"), subject to the
   cycle-safety precondition in §Lineage graph.
6. **Commit, log, index.** The transaction commits; `ingestion_batch.completed_at`/
   `records_created` are set; `audit_log` gets one `insert` row per new `activation_record`;
   `activation_record_fts` is populated automatically by its sync trigger; the sufficiency
   scoring batch job is queued to re-run for every muscle/side/profile-cell touched by this batch.

## Validation constraints — what the database refuses to accept

| The database must refuse | Mechanism | Enforced by |
|---|---|---|
| A record with no source | `source_id NOT NULL REFERENCES source` + `PRAGMA foreign_keys=ON` | DB (hard) |
| A record with no verbatim quote | `CHECK (length(verbatim_quote) > 0)` | DB (hard) |
| A record with no precise citation locator | `CHECK (length(citation_locator) > 0)` | DB (hard) |
| A value with neither a point nor a full range | `CHECK (value IS NOT NULL OR (value_low IS NOT NULL AND value_high IS NOT NULL))` | DB (hard) |
| An inference record not flagged as inference, or vice versa | mutual `CHECK` on `is_inference`/`derivation_id` | DB (hard) |
| An unclassified/free-text unit | `unit_family_id NOT NULL REFERENCES unit_family` (fixed 5-row set) | DB (hard) |
| A silent unit conversion | conversion only via `unit_conversion_rule` (requires `reversible=1`, a `stated_error`, a `justification_source_id`) + `unit_conversion_application`, producing a **new** record, never an in-place edit | DB (hard, structural) |
| A cross-unit-family or cross-normalisation numeric comparison | `v_comparable_pairs` view only joins matching `comparison_key`s | Process (default-safe path; raw SQL against `activation_record` could still bypass it — see §Design risks) |
| A pooled electrode reading silently attributed to one muscle | `trg_pooled_site_requires_mapping` | DB (hard) |
| Editing a measured value, unit, citation or source after the fact | `trg_activation_record_immutable` (`RAISE(ABORT, ...)`) | DB (hard) |
| Deleting a record | No `DELETE` path used anywhere in the design; retraction only flips `record_status` | Process + DB (no delete statements in any script) |
| A phase definition with no printed boundary text | `CHECK (length(printed_definition) > 0)` | DB (hard) |
| A lineage edge that closes a cycle | pre-insert `WITH RECURSIVE` reachability check | Process (scripted, not a `CHECK` — SQLite cannot express graph acyclicity declaratively) |
| Scoring a pooled profile cell with no justifying collapse rule | `v_pool_eligible_cells` only includes cells covered by an `active` `profile_collapse_rule` | Process (view-mediated) |
| A tolerance band silently hard-coded in application logic | all thresholds read from `sufficiency_tolerance_param`, versioned | Process/DB hybrid |
| Type mismatch (e.g. text in a numeric column) | `STRICT` tables (SQLite ≥3.37) | DB (hard) |
| Foreign-key violations silently ignored | `PRAGMA foreign_keys = ON` mandated on every connection | Process (must be set explicitly — off by default in SQLite) |

- Two rows above are marked "Process" rather than "DB (hard)" deliberately, not glossed over:
  SQLite's `CHECK` constraints are row-scoped and cannot express "this insert must not close a
  cycle in another table" or "this view must only ever be queried, never the base table
  directly." Both are named explicitly in §Design risks rather than being claimed as guaranteed.

## Backup, versioning and corruption recovery

- **Crash resilience during a session:** `PRAGMA journal_mode = WAL` — protects against a torn
  write corrupting the main file if the process or machine dies mid-transaction; the last
  committed transaction is intact on next open. Every multi-row ingestion runs inside one
  explicit `BEGIN … COMMIT`, never autocommit-per-row.
- **End-of-session integrity check:** `PRAGMA quick_check;` after routine sessions; the full
  `PRAGMA integrity_check;` before any git commit — catches corruption before it propagates into
  version history.
- **Point-in-time binary backup:** `VACUUM INTO 'backups/evidence_<YYYYMMDD_HHMM>.db';` at the end
  of every working session — atomic and consistent even if the live DB is mid-session, reclaims
  space, and (per SQLite's own documentation) leaves no forensic trace of previously deleted
  content, i.e. it also gives a clean recovery point rather than a copy carrying stale bloat.
  Kept locally, timestamped, rotated (e.g. keep last 14 daily + 1 monthly).
- **Git-diffable snapshot (requirement 10's "or a documented alternative"):** the authoritative
  `.db` file itself is binary and gitignored — committing it directly would make every diff
  opaque and bloat the repository on every session, which defeats the point of version control
  for an evidence corpus. Instead, after each session, export the **current** (non-superseded,
  non-retracted where relevant) state of every core table as CSV, one file per table, rows in a
  fixed, deterministic order (primary key ascending), so unchanged rows produce byte-identical
  lines and `git diff` shows only genuinely new/changed/retracted rows:

  ```sql
  .mode csv
  .headers on
  .once db_export/activation_record.csv
  SELECT * FROM activation_record ORDER BY record_id;
  -- repeated per table
  ```

  This CSV tree — not the `.db` file — is what's committed. A companion
  `scripts/rebuild_db_from_csv.py` (or an equivalent `.sql` load script) can always reconstruct
  a fresh, correct `.db` from the CSVs alone, so the committed CSVs are themselves a sufficient
  disaster-recovery source even if every binary copy (working file and all `VACUUM INTO`
  backups) is lost — bounding worst-case data loss to "whatever changed since the last commit,"
  never "everything."
- **DuckDB needs no separate backup.** It attaches directly to the live SQLite file
  (`ATTACH ... TYPE sqlite`, confirmed read/write via Context7) rather than holding its own copy,
  so there is no second store to keep in sync or lose.
- **Derived Parquet caches** (dense envelope grids, §Storage engine) are explicitly disposable:
  gitignored, rebuilt on demand from `activation_record` by a committed script, never a backup
  target — losing one costs a re-run, not data.
- **Large binary source artefacts** (scanned PDFs, images) live on disk outside the database
  (`source.local_file_path`), not as BLOBs inside SQLite — this keeps the `.db` itself small and
  fast, and keeps genuinely large binaries out of git entirely. Documented alternative for these
  bytes specifically: periodic copy to a second local drive or a cloud-synced folder (OneDrive,
  matching the Windows environment) — stated explicitly rather than left implicit, per
  requirement 10.
- **Off-machine redundancy:** the CSV export tree is small, text, and compresses well — push it
  to the project's existing GitHub remote on every session's commit, riding the same discipline
  already in use for the rest of the repository. The `.db` working file and its `VACUUM INTO`
  backups get the OneDrive/second-drive treatment above.
- **Corruption recovery procedure, concretely:**
  1. `PRAGMA integrity_check;` to diagnose and scope the damage.
  2. If damaged, restore the most recent `VACUUM INTO` backup.
  3. If no usable recent backup exists, rebuild the `.db` from the last git-committed CSV export
     tree via the load script — the true floor of data-loss protection, independent of the
     working machine's disk state entirely.
- **Schema evolution:** numbered migration scripts (`migrations/0001_*.sql`, `0002_*.sql`, …)
  applied in strict order, each recording itself in `schema_migration`. No ad hoc schema drift
  with no record of what changed or when — the same "no data loss, no corner-cutting" discipline
  applied to the schema itself, not only to the data it holds.

## Design risks

1. **Query-discipline risk.** Several of the strongest guarantees (no cross-unit comparison, no
   collapsing without an active rule, no lineage cycles) are enforced by the *sanctioned* views
   and scripts (`v_comparable_pairs`, `v_pool_eligible_cells`, the pre-insert cycle check), not by
   `CHECK` constraints alone — SQLite cannot express all of them declaratively. A future session
   writing ad hoc SQL directly against `activation_record` or `source_lineage_edge` could still
   violate them. Stated as a residual risk, not hidden behind the schema's other hard guarantees.
2. **Lineage graph completeness.** `source_lineage_edge` is only as complete as the research
   already done (or yet to be done) to detect reproduction. An undetected reproduction — a source
   silently reprinting another's numbers without citing it — inflates `n_sources_independent` and
   can falsely promote a cell from Insufficient to Provisional or Sufficient. This is the single
   most consequential failure mode for requirement 7's entire purpose, and it is a research-
   coverage risk the schema cannot close by itself.
3. **Sufficiency score staleness.** `sufficiency_score` is a rebuildable cache refreshed by batch,
   not a live trigger. If a session acts on a status without re-running the scoring job after the
   most recent ingestion or lineage edge, a decision could be made against a stale status.
   Mitigation: score refresh is a mandatory, scripted last step of ingestion (§Ingestion
   pipeline), not an optional afterthought — but it depends on that discipline being followed.
4. **Unbounded volume growth.** "Several GB" is not yet bounded, particularly if raw source PDFs
   or dense per-ms interpolated grids were stored inside the database rather than referenced
   externally. Mitigated by design (`source.local_file_path` for binaries, Parquet cache for
   dense derived grids) but the mitigation only holds if every future ingestion follows it rather
   than taking the shortcut of a BLOB column.



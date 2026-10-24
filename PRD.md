# Esports Scouting & Multi-Roster Intelligence Platform
## Product Requirements Document

**Status:** Draft for implementation planning  
**Version:** 0.1  
**Date:** 24 October 2026  
**Problem statement:** Problem Statement 4  
**Product name:** Working title; not approved  
**Owner:** To be assigned

> This document specifies a proposed product and MVP. It does not claim the software, data integrations, scoring model, or validation studies have been implemented. A separate approved `product-decisions.md` was not supplied, so unresolved choices are recorded explicitly.

## 1. Executive summary

The proposed platform helps an esports organization define a recruitment need, evaluate candidates against it, compare evidence, and record a human decision. It combines game-specific performance metrics, configurable evaluation dimensions, roster context, deterministic ranking, and evidence-grounded explanations.

The core workflow is: create a recruitment brief; load an approved dataset or labelled synthetic data; validate and normalize metrics; calculate reproducible scores; inspect a ranked shortlist; compare candidates against the current roster and vacancy; record a human review decision.

**Product thesis:** Find the right fit, not just the highest stats.

The proposed differentiator is a recruitment-brief-driven shortlist whose scores can be traced to metrics and assessments, with uncertainty and missing data made visible. The initial game title remains open. Implement one game and one or two roles end-to-end for the hackathon, while keeping the architecture extensible to VALORANT, Counter-Strike 2 (CS2), and League of Legends (LoL).

### MVP success condition

A judge can create a recruitment brief, inspect a shortlist, understand score inputs, change priorities and see the ranking update deterministically, compare candidates in roster context, and record a human decision.

### Unresolved decisions

- Initial game and roles.
- Data source, permissions, license/terms, and available fields.
- Real dataset versus synthetic demo data.
- Missing-data policy.
- Authentication/deployment mode.
- Product name, team owners, and deadline.
- Whether an LLM provider will be used.

## 2. Problem statement and evidence

### 2.1 Problem statement

A single statistic such as K/D does not by itself establish role suitability, tactical contribution, consistency, communication, or compatibility with an existing roster. Multi-title organizations also need a shared way to manage teams, vacancies, briefs, and evaluation history without pretending different games have identical roles or metrics.

The proposed platform structures this workflow around game-specific metrics, configurable evaluation dimensions, roster context, transparent ranking, and human review.

### 2.2 Evidence versus hypotheses

| ID | Statement | Status | Product implication |
|---|---|---|---|
| E-01 | HLTV describes a composite CS rating with multiple performance dimensions. | Supported by published methodology. | Avoid treating one metric as a complete evaluation. |
| E-02 | GRID publishes a unified data offering across multiple esports titles. | Supported by provider documentation. | Multi-title normalization is plausible, but access/terms must be checked. |
| E-03 | Oracle's Elixir provides downloadable professional LoL match data. | Supported by its downloads page. | Potential historical dataset, subject to terms and field suitability. |
| E-04 | Awpy parses CS2 demo files into structured match data. | Supported by project documentation. | Potential CS2 data ingestion route if valid demo files are available. |
| E-05 | Riot's VALORANT policy restricts some scouting use cases. | Verify current policy before implementation. | Do not assume public visibility or opt-in alone authorizes a scouting app. |
| H-01 | Coaches want brief-driven rankings over generic leaderboards. | Unvalidated hypothesis. | Interview coaches and test a prototype. |
| H-02 | Roster context changes candidate preferences. | Unvalidated hypothesis. | Compare rankings against different roster configurations. |
| H-03 | Evidence-grounded explanations improve trust. | Unvalidated hypothesis. | Test explanation comprehension and accuracy. |
| H-04 | Multi-roster management is valuable to target organizations. | Unvalidated hypothesis. | Interview managers who oversee multiple teams. |

### 2.3 Primary pain points

1. **Statistics without role context:** aggregate metrics may not indicate suitability for a particular tactical role.
2. **Individual performance versus roster fit:** a strong player may not fill the team's actual capability gap.
3. **Fragmented multi-title operations:** shared organization management must coexist with game-specific metrics and data sources.

These are plausible problems, not quantified industry-wide findings. No customer interviews, adoption statistics, or measured recruitment outcomes were supplied.

### 2.4 Evidence register

Verify current policies, source terms, dates, and capabilities before implementation.

- HLTV Rating 2.1: https://www.hltv.org/news/40051/introducing-rating-21
- GRID games/data: https://grid.gg/data/games/
- GRID access/plans: https://grid.gg/plans/
- Oracle's Elixir downloads: https://oracleselixir.com/tools/downloads
- Awpy documentation: https://awpy.readthedocs.io/en/stable/
- Awpy repository: https://github.com/pnxenopoulos/awpy
- Riot VALORANT developer policy: https://developer.riotgames.com/docs/valorant
- Riot LoL developer policy: https://developer.riotgames.com/docs/lol
- VLR.gg statistics: https://www.vlr.gg/stats
- FOKUS reference site supplied in the concept: https://fokus.gg/

FOKUS is a reference for further investigation only. This PRD does not claim its internal scouting process or a specific scoring formula is publicly documented.

## 3. Target users and personas

### Primary: Head coach / analyst
**Goal:** identify candidates who fit a role and strategy using reviewable evidence.  
**Needs:** role-specific indicators, shortlist comparison, score context, override capability.  
**Success:** can explain why a candidate is shortlisted and what evidence is missing.

### Secondary: Team / roster manager
**Goal:** track roster composition, vacancies, recruitment progress, and decisions across teams.  
**Needs:** team overview, role coverage, briefs, candidate status, decision history.  
**Success:** can find open vacancies and associated shortlists without disconnected documents.

### Secondary: Data / scouting analyst
**Goal:** prepare and inspect player data and metric definitions.  
**Needs:** CSV validation, normalization rules, provenance, missing-data reports, reproducible scoring.  
**Success:** can reproduce a score from stored inputs and configuration.

### Proposed roles and permissions

| Role | Proposed permissions |
|---|---|
| Organization admin | Manage organization, users, teams, configuration |
| Coach/scout | Create briefs, compare candidates, record decisions |
| Analyst | Import/validate data, inspect metric definitions, view evaluations |
| Read-only reviewer | View approved reports and evidence |

A seeded demo workspace is acceptable for the MVP, but must not be represented as production authentication.

## 4. Competitive analysis and differentiation

The product is not positioned as the first esports analytics tool. The proposed opportunity is to connect a recruitment brief, candidate evaluation, roster context, and explainable decision record in one workflow.

| Product/resource | Documented strength | Potential distinction | Limitation |
|---|---|---|---|
| VLR.gg | Public VALORANT stats and filters. | Recruitment criteria and explanations, subject to permitted data use. | Public visibility does not grant reuse/scraping rights. |
| HLTV | CS statistics and published Rating 2.1 methodology. | Relate metrics to a specific vacancy and roster context. | Do not imply it lacks all scouting features without further research. |
| GRID | Multi-title data infrastructure. | Decision-support layer over data the team is licensed to use. | Access, coverage, price, and use rights require verification. |
| Oracle's Elixir | Downloadable professional LoL match data. | Convert suitable records into a recruitment workflow. | Not a universal source for every title or assessment dimension. |
| Proposed platform | Planned brief-driven ranking, configurable weights, roster context, evidence, decision history. | Traceability from team need to candidate recommendation. | Differentiation and demand are unvalidated. |

**Proposed value proposition:** A recruitment decision workspace that ranks candidates against a team's documented needs, explains each ranking using traceable evidence, and keeps the coach in control.

Do not claim “predicts chemistry,” “finds the objectively best player,” or “detects leadership with AI” without validated methods and suitable data.

## 5. Goals and non-goals

### Goals
- G-01: Create a structured recruitment brief.
- G-02: Load a valid candidate dataset for the selected title.
- G-03: Calculate reproducible scores from configurable dimensions and weights.
- G-04: Compare candidates with evidence and missing-data disclosure.
- G-05: Display roster context and the vacancy.
- G-06: Generate an explanation grounded in calculated results and supplied evidence.
- G-07: Record a human review decision and rationale.
- G-08: Keep the data model extensible to future game-specific adapters.

### Non-goals for MVP
- Production-grade live ingestion for three games.
- Automated transfer-market valuation or salary prediction.
- Personality, cognitive, communication, or leadership inference from K/D.
- Match-win or team-chemistry prediction without validated data.
- Autonomous recruitment decisions.
- Production-scale SaaS billing and provisioning.
- Claims of improved competitive results before evaluation.

## 6. Functional and non-functional requirements

Priorities: **P0** required for core demo; **P1** useful if time permits; **P2** future.

### 6.1 Functional requirements

| ID | Priority | Requirement | Acceptance criteria |
|---|---|---|---|
| FR-001 | P0 | Create recruitment brief | User selects configured game, role, playstyle, priorities, and weights; invalid fields show actionable errors. |
| FR-002 | P0 | Load candidate data | System accepts the agreed input format and reports imported, rejected, and incomplete rows. |
| FR-003 | P0 | Record provenance | Dataset records source/type, import timestamp, and synthetic/real status. |
| FR-004 | P0 | Normalize supported metrics | Rules are documented and comparability context is used where available. |
| FR-005 | P0 | Calculate fit scores | Identical data/configuration produces identical scores. |
| FR-006 | P0 | Rank candidates | Ranking is stable; ties and insufficient-data cases are handled and disclosed. |
| FR-007 | P0 | Explain score components | Candidate view shows component scores, weights, evidence, and missing-data indicators. |
| FR-008 | P0 | Compare candidates | At least two candidates can be compared against the same brief/configuration. |
| FR-009 | P0 | Show roster context | Team, vacancy, current role assignments, and linked shortlist are visible. |
| FR-010 | P0 | Record human decision | Decision state and optional rationale can be saved with reviewer and timestamp. |
| FR-011 | P0 | Prevent unsupported AI claims | Explanation cannot change score and uses only structured results/evidence. |
| FR-012 | P0 | Label synthetic data | Synthetic records and resulting scores are clearly labelled in UI and exports. |
| FR-013 | P1 | Export shortlist | Export includes score breakdown, source labels, and caveats. |
| FR-014 | P1 | Track evaluation history | Prior evaluations and configuration version can be inspected. |
| FR-015 | P1 | Multi-team overview | User can switch among seeded teams and see open vacancies/status. |
| FR-016 | P2 | Add game adapters | New game metrics can be added without rewriting shared recruitment workflow. |
| FR-017 | P2 | Approved live integration | Integrate only after terms, authorization, access, and fields are verified. |

### 6.2 Non-functional requirements

| ID | Priority | Requirement | Acceptance criteria |
|---|---|---|---|
| NFR-001 | P0 | Reproducibility | Identical inputs/configuration yield identical scores/order. |
| NFR-002 | P0 | Explainability | Each score traces to components, weights, and input evidence. |
| NFR-003 | P0 | Data quality | Invalid/missing/duplicate/out-of-range values are flagged, not silently coerced. |
| NFR-004 | P0 | Security hygiene | Secrets remain server-side; input is validated; write access is controlled for deployment mode. |
| NFR-005 | P0 | Provenance | Real, synthetic, derived, and manually assessed data are distinguishable. |
| NFR-006 | P0 | Usability | A first-time test user can complete the main journey without developer intervention. |
| NFR-007 | P1 | Performance | Proposed target: common scoring/display under 2 seconds for the agreed demo dataset. Not yet measured. |
| NFR-008 | P1 | Accessibility | Keyboard navigation, visible focus, labels, and adequate contrast for key flows. |
| NFR-009 | P1 | Reliability | Failures return clear errors and do not silently save partial evaluations. |
| NFR-010 | P1 | Portability | Schemas, metric definitions, and diagrams are version-controlled; export is documented. |

### 6.3 Scoring model

Initial weights from the concept are **prototype assumptions**:

- Role Performance (R): 35%
- Tactical Fit (T): 25%
- Roster Synergy (S): 20%
- Cognitive & Behavioral Assessment (B): 20%

\[
\text{Fit Score}=0.35R+0.25T+0.20S+0.20B
\]

Components are intended to be normalized to 0–100. The score is relative to a recruitment brief, not an absolute measure of talent.

Required safeguards:
1. Validate weights and document whether they must sum to 1.0 or are normalized.
2. Do not silently treat missing dimensions as zero or redistribute weights.
3. Show data coverage separately from score.
4. Mark manual coach ratings as assessments, not match-derived facts.
5. Store scoring configuration version with each evaluation.
6. Test weight changes, missing values, ties, and invalid inputs.

**Blocking decision:** the missing-data policy must be selected before implementation. Default recommendation: return “insufficient evidence” if a required dimension is absent, unless the team approves a documented alternative.

## 7. User stories and acceptance criteria

### US-001: Create recruitment brief
As a coach, I want to define a vacancy and priorities so candidates are evaluated against the same requirements.
- Required fields and weights are validated.
- Saved brief has unique ID, game, role, priorities, weights, creator, and timestamp.
- Invalid weight configuration is rejected with a clear message.

### US-002: Import and validate candidates
As an analyst, I want to load a dataset and see validation results.
- Required columns and types are validated.
- Invalid rows are counted and reported with reasons.
- Provenance and synthetic/real status are stored.
- Failed imports do not silently create partial valid datasets.

### US-003: Inspect candidate fit
As a coach, I want component scores and evidence.
- Candidate page shows overall score, components, weights, evidence, and missing-data status.
- Score can be reproduced from stored inputs/configuration.
- Fit is explicitly labelled as relative to the selected brief.

### US-004: Compare candidates
As a coach, I want side-by-side comparison.
- At least two candidates can be selected.
- Candidates use the same brief/configuration.
- Component scores, key evidence, and data coverage are visible.

### US-005: Review roster fit
As a roster manager, I want vacancy and role coverage in context.
- Roster members and role assignments are visible.
- Target vacancy is clear.
- Shortlist is linked to the relevant team/brief.
- No unsupported chemistry prediction is displayed.

### US-006: Read grounded explanation
As a coach, I want to understand why candidates differ.
- Explanation runs after deterministic scoring.
- It uses only supplied metrics, scores, assessments, and missing-data indicators.
- It cannot change the ranking.
- If explanation fails, deterministic score breakdown remains available.

### US-007: Record decision
As a coach, I want a review record and rationale.
- Supported states include shortlisted, hold, rejected, or further review.
- Saved decision includes brief, candidate, reviewer, timestamp, and optional rationale.
- The interface does not imply that a saved state equals an actual transfer.

## 8. MVP scope and prioritization

### P0: Must demonstrate
- One game, one or two roles.
- Recruitment brief builder.
- Validated CSV or seeded demo data.
- Documented metrics and deterministic weighted scoring.
- Ranked shortlist and candidate comparison.
- Roster/vacancy context.
- Evidence-grounded explanation.
- Human decision record.
- Provenance/synthetic-data labels.
- Loading, empty, error, and missing-data states.

### P1: If time permits
- Shortlist report export.
- Evaluation history and config version.
- Multi-team switching with seeded teams.
- Metric trend charts.
- Regression tests for import/scoring.

### P2: Future
- Additional game adapters and approved data integrations.
- Longitudinal player development tracking.
- Structured coach assessment modules.
- Evaluation against expert labels/historical outcomes.
- Production-grade access control and audit history.

### Explicitly out of scope
Unapproved scraping; automated personality detection; real transfer valuation without verified market data; predictive synergy without validation; production-grade multi-tenant guarantees.

## 9. User journeys and UX states

### Primary journey
1. Open organization dashboard.
2. Select team and vacancy.
3. Create recruitment brief.
4. Choose dataset.
5. Review validation and coverage.
6. Run deterministic evaluation.
7. Inspect ranked shortlist and evidence.
8. Compare candidates.
9. Review roster context and explanation.
10. Record human decision.

### Required UX states

| Screen | State | Behavior |
|---|---|---|
| Dashboard | Empty | Explain how to create team/brief or load demo data. |
| Brief builder | Invalid | Field-level errors; preserve valid inputs. |
| Import | Processing | Show pending/progress state and prevent duplicate submission. |
| Import | Invalid | Show row/column errors. |
| Candidate list | Empty | Explain filters/data limitations and offer reset. |
| Candidate detail | Missing dimension | Show insufficient evidence, not fabricated score. |
| Scoring | Failure | Preserve brief/data and offer retry. |
| Explanation | Unavailable | Keep deterministic score breakdown available. |
| Decision save | Failure | Do not show success; preserve input. |
| Export | Synthetic data | Include synthetic-data disclaimer. |

### Figma design specification

No Figma file is included. Implement the following as editable native frames.

**Visual direction:** premium analytics workspace; dark navy or neutral base; restrained accents; readable typography; avoid decorative gaming clichés and meaningless charts.

- **Screen A, Organization dashboard:** organization/team selector; KPI strip for active teams, vacancies, briefs, candidates under review; team cards; recent decisions; empty-state actions.
- **Screen B, Brief builder:** stepper Team → Role → Priorities → Data → Review; game, role, playstyle, target level, optional budget category, weights; total weight and validation summary.
- **Screen C, Ranked shortlist:** brief summary; table with rank, candidate, fit, R/T/S/B, data coverage, source; synthetic/incomplete-data warning; row opens detail.
- **Screen D, Candidate comparison:** side-by-side component scores, relevant metrics, evidence, coverage, trade-offs; “Fit to this brief” label.
- **Screen E, Candidate detail:** score and coverage separately; dimension evidence; missing-data panel; assessment provenance; optional explanation with fallback.
- **Screen F, Roster/vacancy:** roster grouped by role, vacancy card, role coverage, linked shortlist; no unsupported synergy prediction.

## 10. System architecture

### 10.1 Proposed stack

| Layer | Proposed technology | Purpose | Status |
|---|---|---|---|
| Frontend | React | Dashboard and workflows | Proposed |
| Backend | Python + FastAPI | API, validation, scoring, reports | Proposed |
| Database | PostgreSQL | Teams, candidates, briefs, metrics, evaluations | Proposed |
| Data processing | Pandas / NumPy or equivalent | Import and metric calculation | Proposed |
| Scoring engine | Deterministic Python module | Reproducible weighted scoring | Proposed |
| Explanation | Optional LLM | Explain structured results | Provider not selected |
| Charts | Recharts or equivalent | Score breakdown and trends | Proposed |
| Hosting | Not selected | Demo deployment | Open decision |

### 10.2 Architecture principles
- Keep scoring separate from API routes and UI.
- Store metric definitions and configuration versions.
- Preserve data provenance and transformations.
- Keep game-specific adapters separate from shared entities.
- Make explanation optional and non-blocking.
- Never use an LLM to calculate the score.
- Treat every external integration as dependent on verified access and permitted use.

### Figure 1. Data-processing workflow

See `diagrams/data-processing-workflow.mmd`. It shows the brief, dataset validation, game-specific feature engineering, deterministic scoring, shortlist, explanation, and coach decision.

### Figure 2. Proposed system architecture

See `diagrams/architecture.mmd`. It shows the React UI, FastAPI backend, validation boundary, PostgreSQL, import pipeline, scoring engine, and optional explanation service.

### Trust boundaries
- Browser-to-API: validate all user inputs.
- API-to-database: use parameterized operations or ORM protections.
- Backend-to-LLM: send only minimum necessary structured data.
- Import boundary: treat CSVs and external payloads as untrusted.
- External data boundary: record source, permission notes, import time, and transformations.

## 11. Database ERD

### Proposed entities

| Entity | Purpose |
|---|---|
| organizations | Organization identity |
| users | Account or demo user |
| organization_memberships | User/organization roles |
| games | Supported game registry |
| teams | Organization teams/rosters |
| players | Player/candidate identity |
| roster_memberships | Historical team membership and role |
| recruitment_briefs | Vacancy, priorities, status |
| datasets | Source/provenance/license notes/import time |
| player_match_stats | Game-specific metric records |
| assessments | Structured coach/task assessments |
| scoring_configs | Versioned weights and missing-data policy |
| evaluations | Score run, component scores, total, coverage |
| evidence_items | Traceable input evidence per evaluation |
| decisions | Human review outcome and rationale |

### Figure 3. Database ERD

Editable source is `diagrams/database-erd.mmd`. JSON payloads are proposed for flexible game-specific metrics/configuration; final schema, constraints, and indexing require engineering review.

## 12. API contracts and request sequences

All endpoints are **proposed**, not deployed. Prefix: `/api/v1`.

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/recruitment-briefs` | Create brief |
| GET | `/recruitment-briefs/{brief_id}` | Read brief/config |
| POST | `/datasets/validate` | Validate upload |
| POST | `/datasets` | Import dataset |
| POST | `/recruitment-briefs/{brief_id}/evaluations` | Run scoring |
| GET | `/recruitment-briefs/{brief_id}/shortlist` | Ranked candidates |
| GET | `/evaluations/{evaluation_id}` | Score/evidence detail |
| POST | `/decisions` | Record human decision |
| GET | `/teams/{team_id}/roster` | Read roster |
| GET | `/health` | Health check |
| GET | `/reports/shortlists/{brief_id}` | Export report |

### Example create-brief request

```json
{
  "team_id": "team_demo_01",
  "game_slug": "cs2",
  "target_role": "igl",
  "playstyle": "tactical_controlled",
  "priorities": ["decision_making", "role_coverage", "consistency"],
  "weights": {
    "role_performance": 0.35,
    "tactical_fit": 0.25,
    "roster_synergy": 0.20,
    "behavioral_assessment": 0.20
  }
}
```

`cs2` and the values are illustrative only; the initial game is not yet selected.

### Example evaluation response

```json
{
  "brief_id": "brief_demo_01",
  "scoring_config_version": 1,
  "provenance_type": "synthetic",
  "results": [
    {
      "player_id": "player_demo_01",
      "total_score": 86.3,
      "component_scores": {
        "role_performance": 82,
        "tactical_fit": 92,
        "roster_synergy": 88,
        "behavioral_assessment": 80
      },
      "data_coverage": 1.0,
      "warnings": ["Synthetic demonstration record"]
    }
  ]
}
```

This is illustrative, not a real evaluation or proof of implementation.

### Error envelope

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "The scoring weights do not satisfy the configured policy.",
    "details": [{"field": "weights", "issue": "Invalid sum"}],
    "request_id": "req_demo_01"
  }
}
```

Proposed status codes: 400 malformed input; 401 unauthenticated if auth is enabled; 403 unauthorized; 404 not found; 409 conflict; 413 upload too large; 422 semantic validation error; 429 rate limited if implemented; 500 unexpected failure.

### Figure 4. Evaluation sequence

Editable source is `diagrams/evaluation-sequence.mmd`. It shows brief creation, data/config retrieval, deterministic scoring, persistence, optional explanation, and shortlist response.

## 13. Security, privacy, and failure handling

### Security requirements
- SEC-001: Keep API keys, database credentials, and LLM secrets server-side.
- SEC-002: Validate all inputs, query parameters, files, and imported rows.
- SEC-003: Use parameterized database operations or ORM protections.
- SEC-004: Enforce organization/role authorization if multi-user auth is enabled.
- SEC-005: Limit upload size and accepted file types.
- SEC-006: Minimize personal data.
- SEC-007: Avoid sending unnecessary identifiers or sensitive assessments to an LLM.
- SEC-008: Log operational events without secrets or unnecessary personal data.
- SEC-009: Record dataset provenance and use notes.
- SEC-010: Distinguish seeded demo from production-secured deployment.

### Privacy
Player profiles and coach/behavioral assessments may be commercially sensitive or personal data. Before using real records, establish permission, purpose, retention, access, and deletion rules. Synthetic identities and assessments are the lower-risk demo default when no approved data source is confirmed.

### Failure handling

| Failure | Required behavior |
|---|---|
| Schema mismatch | Reject/quarantine invalid rows and show details. |
| Missing metric | Show missing evidence; apply approved policy or mark insufficient. |
| Invalid weights | Reject scoring request. |
| Duplicate import | Detect where feasible and report/resolve safely. |
| Database unavailable | Return error; never claim save succeeded. |
| LLM unavailable | Preserve deterministic scores and show explanation unavailable. |
| Source unavailable | Use permitted cached/demo data only with provenance visible. |
| Unsupported game/role | Block scoring with explicit message. |
| Export failure | Preserve shortlist and allow retry. |

### Risk register

| ID | Risk | Severity | Mitigation |
|---|---|---|---|
| R-01 | Data terms disallow scouting use | Critical | Verify terms/access; use synthetic data until resolved. |
| R-02 | Metrics cannot be measured consistently | High | Define metric dictionary and missing-data policy. |
| R-03 | Coaches do not value workflow | High | Interview and test prototype. |
| R-04 | AI invents evidence | High | Ground prompt; test; retain fallback. |
| R-05 | Synthetic scores are mistaken for real | High | Label UI, reports, and slides. |
| R-06 | Three-game scope exceeds deadline | High | Build one adapter; defer others. |
| R-07 | Missing data distorts ranking | High | Show coverage and test policy. |
| R-08 | Personal/assessment data exposed | High | Minimize data, restrict access, protect secrets. |

## 14. Testing and measurable success metrics

### Test plan

| ID | Area | Test | Expected result |
|---|---|---|---|
| T-001 | Scoring | Repeat identical inputs/config | Identical scores and order |
| T-002 | Weights | Invalid weight policy | Actionable validation error |
| T-003 | Missing data | Required dimension missing | Approved insufficient-evidence behavior |
| T-004 | Metrics | Out-of-range value | Rejected or explicitly handled |
| T-005 | Import | Required column missing | Schema error details |
| T-006 | Import | Duplicate records | Deterministic handling and report |
| T-007 | Ranking | Tied scores | Stable documented tie-break |
| T-008 | Explanation | Unsupported claim in output | Test catches it; fallback works |
| T-009 | Security | Unauthorized write | Denied when auth enabled |
| T-010 | UX | First-time core journey | User completes without developer help |
| T-011 | Provenance | Synthetic export | Clearly labelled synthetic |
| T-012 | Failure | DB/LLM unavailable | Clear error; no false success |

### Proposed metrics (targets, not results)

| Metric | Proposed target | Measurement |
|---|---|---|
| Demo completion | 4 of 5 test runs complete core journey | Observe brief through decision |
| Score reproducibility | 100% identical for same test inputs | Automated regression tests |
| P0 test coverage | All P0 requirements tested or blocker documented | Traceability matrix |
| Provenance visibility | 100% demo records appropriately labelled | UI/export inspection |
| Explanation grounding | No unsupported factual claims in fixed test set | Human review against evidence |
| Response time | Under 2 seconds for agreed demo dataset | Measure on target environment |
| User comprehension | 4 of 5 test users explain why top candidate ranked first | Moderated usability test |

These are proposed targets. Do not report them as achieved until measured. A small usability sample is diagnostic, not representative of the market.

### Traceability matrix

| Goal | Requirements | Tests |
|---|---|---|
| G-01 brief creation | FR-001 | T-002 |
| G-02 valid data | FR-002–FR-004 | T-005, T-006, T-011 |
| G-03 reproducible ranking | FR-005, FR-006, NFR-001 | T-001–T-004, T-007 |
| G-04 evidence explanation | FR-007, FR-008, NFR-002 | T-008 |
| G-05 roster context | FR-009 | T-010 |
| G-06 grounded explanations | FR-011 | T-008 |
| G-07 human decision | FR-010 | T-010 |
| G-08 future game adapters | FR-016, NFR-010 | Architecture review |

## 15. Implementation roadmap, dependencies, and ownership

Timeline and owners were not supplied. This is a sequence, not a committed calendar.

### Phase 0: Resolve blockers
- Select one game and one or two roles.
- Verify dataset terms, permitted use, and available fields.
- Agree schema, metric definitions, and missing-data policy.
- Decide authentication/deployment mode and assign owners.

**Exit:** approved data/demo fixture, schema, and scope.

### Phase 1: Data foundation
- Define schema and migrations.
- Implement dataset validation and provenance.
- Prepare a small labelled dataset.
- Define the game-specific metric dictionary.

**Exit:** imports are repeatable and invalid data is reported.

### Phase 2: Scoring engine
- Implement normalization and weighted scoring.
- Implement missing-data policy and coverage.
- Version scoring configurations.
- Add deterministic tests.

**Exit:** outputs can be reproduced from stored inputs/config.

### Phase 3: Recruitment UI
- Build brief builder, shortlist, candidate detail, comparison, and roster context.
- Add loading, empty, error, and missing-data states.

**Exit:** core journey works on demo data.

### Phase 4: Explanation and decisions
- Add optional evidence-grounded explanation.
- Implement human decision recording and fallback behavior.

**Exit:** scores work without the LLM and decisions persist.

### Phase 5: QA and demo
- Run P0 acceptance tests.
- Verify provenance and citations.
- Rehearse on target device/network.
- Prepare a permitted fallback dataset and scope freeze.

**Exit:** demo can be completed reliably and limitations are disclosed.

### Ownership template

| Workstream | Owner | Output |
|---|---|---|
| Product/research | To assign | Brief, validation, requirements, evidence register |
| Data/scoring | To assign | Schema, metrics, import, scoring, tests |
| Backend | To assign | API, persistence, validation, security |
| Frontend/UX | To assign | Brief, shortlist, comparison, roster screens |
| QA/demo | To assign | Acceptance report, fallback, demo script |

### Critical path
Permitted data source → game/role and metric dictionary → missing-data policy → schema/API → scoring engine → UI integration → tests and demo rehearsal.

If data access remains unresolved, use synthetic data to demonstrate workflow feasibility and disclose that it does not validate real-world ranking quality.

## 16. Assumptions, open questions, and future roadmap

### Assumptions register

| ID | Assumption | Status |
|---|---|---|
| A-01 | Coaches want brief-driven ranking | Unvalidated |
| A-02 | Roster context changes preferences | Unvalidated |
| A-03 | Data can be lawfully used for chosen workflow | Must verify |
| A-04 | Four dimensions can be measured consistently | Unvalidated |
| A-05 | AI explanations improve understanding | Must test |
| A-06 | Multi-roster management is valuable | Must validate |
| A-07 | Initial weights are useful | Prototype assumption only |

### Open questions

**Blocking**
- Which game and roles are in the MVP?
- Which data source is available, and what use is permitted?
- What are the exact dataset schema and sample size?
- What is the missing-data policy?
- Is authentication required?
- What is the deadline and team capacity?

**Important**
- What method defines each role metric?
- Is behavioral assessment omitted from MVP or entered as documented coach assessment?
- Which LLM provider, if any, will be used?
- Is budget only a categorical filter, or is verified market data available?
- How will coaches validate score usefulness?

### Future roadmap

- **Now:** one game adapter, one or two roles, brief builder, scoring, comparison, roster context, decision record.
- **Next:** coach interviews, usability testing, better metric definitions, export/report, evaluation history.
- **Later:** additional game adapters, approved licensed integrations, player development tracking, structured assessments, expert/outcome validation, stronger access controls.
- **Research-dependent:** synergy prediction, match outcome prediction, and automated behavioral evaluation. Do not claim these without suitable data and validation.

## 17. References and technical appendices

### 17.1 Reference register
1. HLTV Rating 2.1: https://www.hltv.org/news/40051/introducing-rating-21
2. GRID data/game coverage: https://grid.gg/data/games/
3. GRID plans: https://grid.gg/plans/
4. Oracle's Elixir downloads: https://oracleselixir.com/tools/downloads
5. Awpy documentation: https://awpy.readthedocs.io/en/stable/
6. Awpy repository: https://github.com/pnxenopoulos/awpy
7. Riot VALORANT developer policy: https://developer.riotgames.com/docs/valorant
8. Riot LoL developer policy: https://developer.riotgames.com/docs/lol
9. VLR.gg statistics: https://www.vlr.gg/stats
10. FOKUS reference: https://fokus.gg/

Re-check current policy, data availability, license/terms, and product capabilities immediately before implementation or publication. Customer interview evidence and a completed legal review were not provided.

### 17.2 Minimum prototype dataset schema

| Field | Required | Description |
|---|---|---|
| player_id | Yes | Stable pseudonymous ID |
| display_name | Optional | Synthetic alias or permitted public name |
| game_slug | Yes | Supported game |
| role | Yes | Selected game's role taxonomy |
| competitive_level | Yes | Defined tier/level |
| match_count | Yes | Number of observations |
| metric_* | Depends | Game-specific numeric features |
| source_type | Yes | synthetic, public_dataset, licensed, or manual_assessment |
| source_reference | Yes | Dataset/file/source identifier |
| collected_at | Yes | Import/collection timestamp |
| patch_or_context | If available | Patch/map/mode or comparable context |

Do not assume this schema fits all games unchanged.

### 17.3 Scoring pseudocode

```python
def calculate_fit_score(component_scores, weights):
    # Proposed policy: required dimensions must be present.
    # Final missing-data policy requires product approval.
    if any(value is None for value in component_scores.values()):
        return {
            "score": None,
            "status": "insufficient_evidence"
        }

    if any(weight < 0 for weight in weights.values()):
        raise ValueError("Weights must be non-negative")

    if abs(sum(weights.values()) - 1.0) > 1e-6:
        raise ValueError("Weights must sum to 1.0")

    for name, value in component_scores.items():
        if not 0 <= value <= 100:
            raise ValueError(f"Score out of range: {name}")

    score = sum(component_scores[name] * weights[name]
                for name in weights)

    return {
        "score": round(score, 2),
        "status": "calculated"
    }
```

This is illustrative pseudocode, not production code. Adapt and test it against the final schema and approved missing-data policy.

### 17.4 Diagram source files

Editable Mermaid sources are delivered in `diagrams/`:
- `architecture.mmd`
- `data-processing-workflow.mmd`
- `database-erd.mmd`
- `evaluation-sequence.mmd`
- `user-journey.mmd`

Render to SVG/PNG with a Mermaid-compatible renderer, then inspect readability after placement in the final document.

---

## Publication checklist

- [ ] Confirm product name, owner, version, deadline, and team capacity.
- [ ] Approve `product-decisions.md`; it was not supplied separately for this draft.
- [ ] Choose initial game and role(s).
- [ ] Verify dataset access, license/terms, and intended use.
- [ ] Validate user need with coaches/managers or label demand as unvalidated.
- [ ] Approve metric definitions and missing-data policy.
- [ ] Confirm whether behavioral assessment is supported by actual inputs.
- [ ] Verify API and schema against the selected MVP.
- [ ] Ensure every P0 requirement has testable acceptance criteria.
- [ ] Run scoring, import, failure, and authorization tests.
- [ ] Verify AI explanations against structured evidence.
- [ ] Label synthetic/illustrative examples in screens, reports, and slides.
- [ ] Render Mermaid diagrams and check readability.
- [ ] Add figure numbers, captions, contents, page numbers, and working links.
- [ ] Check page breaks, tables, headers/footers, and PDF text.
- [ ] Remove unsupported claims and verify citations.
- [ ] Record unresolved risks and assumptions.
- [ ] Rehearse the demo and prepare a permitted fallback dataset.

# Engineering design
## Implemented prototype
CSV archive → Python standard-library loader → local SQLite → deterministic SQL aggregates → JSON → static HTML/CSS/JS. No runtime dependency, external tracking, or outbound customer contact. Browser filters current snapshot; cohort downloads are local. Customer details are pseudonymous source records. Source data stays outside the published repository except the intentionally included product JSON; private hosting is required.

Run `python3 scripts/analyze.py` from repository root. This recreates data/analytics.sqlite, docs/data-audit.json and product/dist/data.json. Do not hand-edit computed numbers. Serve product/dist on port 8080 with Python http.server.

## Production architecture proposal
Ingest CRM, billing, support and consent into immutable bronze tables. Silver resolves account/service-point identity and validates event dates; gold builds daily customer_snapshot, customer_month, experiment_assignment and intervention_outcome. Databricks/Delta is a proposed deployment target, not implemented here. Use service principals, RBAC and catalog lineage; DE owns pipeline SLAs.

| Entity | Grain | Contract |
|---|---|---|
| customer_snapshot | customer_id + snapshot_date | Unique, snapshot timestamp required; versioned risk provenance |
| billing_monthly | customer_id + month | Unique; currency explicit; preserve event month |
| churn | account + departure event | Reason, event date and eligibility denominator |
| tickets | ticket_id | Customer FK; nullable CSAT; resolved enum |
| experiment_assignment | experiment_id + account_id | Immutable arm, assigned_at, eligibility version |
| activation | intervention_id + account_id | Consent checked_at, idempotency key, delivery status |

Do not join facts directly and multiply revenue by ticket or program counts. Aggregate each fact to intended grain first. Historical features require as-of joins using information available before assignment. Current snapshot fields cannot retrospectively train a churn model without leakage.

## Model lifecycle
Start with transparent rules and existing supplied score. Before any predictive deployment, define 90-day outcome, time-based training/validation split and intervention censoring; compare simple baseline. Evaluate PR-AUC, calibration and precision at operational capacity, plus error by segment. Run shadow scoring, monitor score/feature drift weekly, recalibrate on matured labels and retain rollback to previous version. Do not treat risk prediction as treatment responsiveness; estimate uplift only with appropriate randomized evidence.

## Reliability and security
Validate input schema, key uniqueness, timestamps and referential coverage. Quarantine malformed records; atomically publish last-known-good snapshots. Production freshness >24h warns, >48h blocks activation. Apply encryption, least privilege, retention limits and audited exports. Consent and suppression fail closed. A static private prototype is not a production access-control or customer-data platform implementation.

## API proposal
GET /v1/cohorts?segment=&city=&min_score= with snapshot_version and cursor; GET /v1/customers/:id; POST /v1/cohorts/preview; POST /v1/activations with idempotency key and approval reference. Server enforces authorization and suppression; pagination avoids shipping the full customer dataset in production. Prototype uses local JSON instead.

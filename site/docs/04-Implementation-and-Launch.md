# Implementation specs, deployment and iteration
## Implemented surfaces
Overview: scoped current population, high-score count, supplied historical margin, churn reasons and billing trend. Global historical charts explicitly keep their source scope.
Customers: segment/city/min-score filters, searchable IDs, customer detail dialog, descending score order, full filtered CSV export.
Experiment: arm counts, retention, observed lift and interval; illustrative contribution scenario with adjustable eligible population, retention lift, retained contribution and per-person cost.
Data trust: eight source counts, null cell counts, key checks, missing production metadata.
Strategy: decision, scope and stage map with downloadable Markdown documents.

## Metric contracts
High score = supplied risk_score >=70, a planning threshold without validated calibration. Historical margin = sum(lifetime_margin) of selected current customers. Billed revenue = sum(bill_amount) by source month, not cash collected. Churn-reason mix = reason count / all recorded churn events. Experiment retention = retained_90d sum / all rows in arm. Difference = treatment minus control; normal interval = difference ±1.96 × sqrt(pt(1−pt)/nt + pc(1−pc)/nc).
Scenario net value = population × (lift percentage points /100) × assumed contribution per incremental retained customer − population × assumed contact/offer cost. This assumes cost for every targeted person and does not infer lift from risk scores.

## Build and acceptance
Run scripts/analyze.py, then scripts/verify.py; JavaScript syntax checked with node --check. Browser review covers navigation, filters, dialog, scenario recalculation, export and narrow viewport. Automated checks test source reconciliation and experiment arithmetic; completed test evidence belongs in final handoff.

## Deployment
Static output: product/dist. Private Sites hosting; .openai/hosting.json records identity. Source helper packages exact pushed source and then deployment uses that archive. Keep original archive, SQLite and raw CSVs outside product checkout. No environment secrets are required. Local fallback: `python3 -m http.server 8080 --directory product/dist`. Rollback in a production deployment should redeploy previous verified artifact; retain source version IDs.

## Pilot experiment spec
Unit: eligible account, one assignment across linked customers; target cohort and suppression criteria frozen before randomization. Stratify by segment and risk band. Compare new intervention to usual care, not no service. Log delivery but analyze intention to treat. Primary outcome: active service at day 90 with explicit move-out handling pre-registered. Treat move-outs consistently in both arms; do not drop post-treatment outcomes to improve lift. Require complete observation windows, inspect allocation balance and baseline balance, record missing outcomes and bound sensitivity. Pre-register one primary comparison; segment results exploratory with multiplicity caution. Review safety weekly without repeatedly testing efficacy.

## Iteration rules
Day 7: investigate workflow friction and data defects. Day 30: adoption, delivery and complaint review; no mature 90-day claim. Day 90 after last assignment: retention and contribution analysis. Scale if positive incremental value and retention evidence satisfy guardrails; revise message/cohort if inconclusive; stop for harm or negative economics. Record owner, evidence, decision, change and next review in a decision log.

## Honest portfolio narrative
“I built a customer-data decision product around a supplied energy dataset, chose retention as the first wedge, made metric and identity gaps visible, and specified how to validate commercial impact. The prototype demonstrates the workflow; it does not claim a production launch or realized business improvement.”

# TestEnergy — Customer intelligence that earns its next action
Product requirements • v1.0 • 14 October 2026 • Independent portfolio concept

## Decision
Build a retention decision workspace first, supported by reusable customer identity and metric definitions. Help an Operations lead select a transparent customer cohort, inspect why it was selected, and prepare a measurable intervention with Marketing. Expand into acquisition quality and commercial value only after reliable outcomes are available.

This is a portfolio analysis of the supplied archive, not a claim about Rhythm's actual customer base. The user confirmed this dataset is synthetic and approved for public sharing. All business targets below are proposed, not achieved.

## Idea → Research → PRD
The opportunity is the gap between knowing a customer may leave and choosing an intervention that is helpful, affordable, and testable. A common customer foundation should serve multiple teams without turning v1 into an unfocused company dashboard.

Evidence: 24,467 current customer rows; 5,533 historical churn events; 283,619 customer-month bills; 4,000 experiment participants. Bill shock represents 34.9% of recorded departures. Historical experiment retention is 95.50% treatment versus 93.55% control. These findings favor a retention workflow, but do not establish causal drivers or forecast commercial impact.

Public context: Rhythm already offers usage insights, Smart Alerts, and renewal paths. TestEnergy proposes an internal coordination and measurement layer around those touchpoints. See 02-Research.md for sources and validation gaps.

## Users and jobs
| User | Decision | Required evidence |
|---|---|---|
| Operations lead, primary | Which customers need a useful intervention this week? | Cohort size, explainable signal, recommended play, capacity |
| Marketing lead | Which message should be tested against usual care? | Cohort definition, consent eligibility, assignment, outcome |
| Commercial partner | Is the intervention economically worthwhile? | Incremental contribution after offer and contact cost |
| Sales lead | Which channels acquire durable customer relationships? | Weighted CAC now; matched cohort retention later |
| Data Engineering / Science | Can teams trust and improve the decision? | Grain, lineage, freshness, coverage, validation, drift |

## Scope and product choices
P0: customer overview, segment/city/risk filtering, customer inspection, local cohort CSV export, historical churn-reason mix, experiment readout, source-quality evidence. Provide an editable scenario calculator with explicit assumptions, never labeled realized savings.

P1 production: consent and suppression integration, immutable experiment assignment, activation log, outcome monitoring, dated customer snapshots. P2: validated uplift models, customer-facing bill explanation, acquisition payback cohorts.

Defer automated discounts, autonomous outreach, CLV predictions, pricing optimization and production churn probabilities. The data lacks costs, contract end dates, consent, full event history, model metadata and treatment timing. Discounting every high-score customer could reward customers who would stay anyway.

## Primary workflow
1. Read the decision brief and evidence caveats.
2. Filter current customers by segment, city and minimum supplied risk score.
3. Inspect customer plan, tenure, historical margin and supplied driver/play.
4. Export a planning cohort; no message is sent. In production, consent and suppression checks precede activation.
5. Design an experiment and compare incremental retention with net contribution.
6. Review data quality before approving a production pilot.

## Success metrics
| Metric | Definition | Proposed threshold | Owner / timing |
|---|---|---|---|
| Primary: incremental 90-day retention | Retained / all randomized eligible accounts, treatment minus control; intention to treat | +1.5 percentage points with CI excluding zero | DS, after complete 90-day follow-up |
| Economic gate | Incremental retained accounts × forward contribution − all offer/contact costs | Positive; uncertainty range disclosed | Commercial, end of pilot |
| Adoption | Weekly active eligible decision-makers / onboarded decision-makers | ≥70% after 4 weeks | PM |
| Workflow efficiency | Median time from cohort question to approved brief | <10 minutes; establish baseline first | Operations |
| Reliability | Accepted unique current customer IDs / incoming IDs | 100% unique; invalid records quarantined | Data Engineering, each refresh |
| Freshness | Time since latest successful production snapshot | <24 hours; warn after 24h, block after 48h | Data Engineering |
| Guardrails | Complaint rate and contact frequency | No >0.5pp complaint increase; ≤1 unsolicited contact / 14 days | CX / Marketing |

Historical result is supporting evidence, not a production baseline for a new cohort. Power the pilot using prospective cohort retention. Illustratively, detecting a change from 93.55% to 95.05% at two-sided 5% alpha and 80% power requires approximately 3,750 accounts per arm before attrition; confirm with DS and eligibility volume.

## Acceptance criteria
| ID | Given / When / Then | Verification |
|---|---|---|
| AC1 | Given archive inputs, when pipeline runs, then counts reconcile to all eight source CSVs | Automated count assertions |
| AC2 | Given current customer filters, when any filter changes, then queue, count and export use identical predicates | Browser + export check |
| AC3 | Given risk threshold 70, when a customer is selected, then risk is explicitly a supplied score, never probability | Copy review |
| AC4 | Given no matching customers, then a helpful empty state and zero count appear | Browser check |
| AC5 | Given experiment source, then treatment 1910/2000 and control 1871/2000 produce 1.95pp lift | Arithmetic assertion |
| AC6 | Given a scenario input change, then net value updates and is labeled hypothetical | Formula check |
| AC7 | Given absent metadata, then freshness, causality and model validation are disclosed as unknown | Trust review |
| AC8 | Given customer inspection, then source plan, driver, tenure and historical margin match the source row | Spot check |
| AC9 | Given mobile or keyboard navigation, then views remain reachable, filters labeled, and focus visible | Responsive / interaction review |
| AC10 | Given deployment, then private audience is retained and local source reproduces the site | Deployment status + runbook |

## Roadmap and stakeholder alignment
Weeks 1–2: PM + Operations validate decision workflow; DE agrees entity contract; Commercial defines contribution. Exit: signed metric definitions and baseline.
Weeks 3–4: DE publishes daily snapshot; Marketing integrates consent; DS audits historical experiment. Exit: quality and suppression checks pass.
Weeks 5–6: launch prospective randomized pilot with CX capacity cap. Exit: balanced assignment and monitoring live.
Weeks 7–18: observe full 90-day outcomes; no early success claims. Scale only after economic and customer guardrails pass.

Resolve Marketing reach versus Operations capacity with a capped weekly cohort; Commercial owns economic veto, CX owns customer harm stop, PM records tradeoffs. Review weekly with named functional owners before real launch.

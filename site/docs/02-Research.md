# Research and opportunity assessment
## Evidence hierarchy
Observed supplied data → external product context → hypotheses → future validation. No stakeholder interviews have been conducted. The user confirmed the archive is synthetic and safe for public sharing.

## Findings
- 24,467 current IDs, no duplicates. No overlap with churn IDs; historical churn cannot be joined to current scores to evaluate model accuracy.
- 5,533 churn events across October 2024–September 2026. Bill shock: 1,932 (34.9%); cheaper rate: 1,437 (26.0%); moving: 738; nonrenewal: 715; service: 711. Reason shares are not churn rates or causal effects.
- Latest billing month has 24,886 billed accounts, while current customer snapshot has 24,467. Different populations and absent snapshot timestamps make substituting denominators unsafe.
- 4,000 experiment rows, unique IDs, equally sized arms. Control 1,871 retained, treatment 1,910. Difference 1.95pp; approximate unpooled normal 95% CI 0.54–3.36pp. A balanced sample does not prove randomization, valid follow-up or lack of contamination.
- 3,638 empty cells in tickets require column-level interpretation before using satisfaction denominators. Missing satisfaction must not be converted to zero.
- Acquisition CAC must be sum(spend) / sum(new customers), not mean(cac). Move-in $24.93; Referral $45.33; Online $90.88; Partner $122.31; Door-to-door $179.91. Low CAC alone does not establish best channel or payback.
- Current customer 'lifetime_margin' is historical contribution supplied in the archive. It is not modeled lifetime value or forward margin at risk.

## External context, reviewed 14 October 2026
[Rhythm Smart Alerts](https://www.gotrhythm.com/blog/what-are-rhythm-smart-alerts) describes weekly projected usage/bill communication. Inference: retention interventions should build on existing communications rather than duplicate an alert feature.
[Rhythm FAQ](https://www.gotrhythm.com/faq) describes renewal options and usage insights. Inference: customer-data activation can coordinate existing account journeys.
[How to read a Rhythm bill](https://support.gotrhythm.com/hc/en-us/articles/360052389271-How-do-I-read-my-Rhythm-Bill) distinguishes account and service-location identifiers. Production identity should distinguish person, account and service point; archive customer_id alone cannot model all three.

## Prioritization
| Opportunity | Evidence | Delivery confidence | Decision |
|---|---|---|---|
| Retention planning workspace | Churn reasons, current signals, experiment | High for prototype; medium for activation | Build first |
| Acquisition budget optimization | Spend and volume; no matched lifetime outcomes | Medium descriptive, low causal | Show weighted CAC; defer allocation |
| Automated pricing | No wholesale cost, elasticity, contract detail | Low | Defer |
| Program impact / demand response | Enrollment and events, no counterfactual | Medium descriptive | Follow after measurement foundation |

## Research plan and falsification
Interview 3 Operations leads, 2 lifecycle marketers, Commercial and DE. Ask for a recent retention decision, handoff failure, capacity limit and evidence that changed action; avoid asking whether they want a dashboard. Test five task-based sessions: select a cohort, explain inclusion, inspect customer, interpret experiment, identify trust issue. Target four of five independently completing in ten minutes.

Disprove the wedge if operational teams cannot act on supplied signals, incremental contribution is negative, or existing tooling already supports the full workflow. Pivot to data contracts / measurement first if reconciliation or consent quality is inadequate.

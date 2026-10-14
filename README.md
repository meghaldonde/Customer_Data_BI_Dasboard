# TestEnergy — Customer intelligence
An independent customer-data product portfolio for an energy PM role.

Start with [the PRD](docs/01-PRD.md), then [research](docs/02-Research.md), [engineering](docs/03-Engineering.md), and [implementation, deployment and iteration](docs/04-Implementation-and-Launch.md).

Open `product/dist/index.html` directly in your browser; no server is required.

## Reproduce
```
python3 scripts/analyze.py
python3 scripts/verify.py
node --check product/dist/app.js
node scripts/verify-ui.js
python3 -m http.server 8080 --directory product/dist
```
Open http://localhost:8080. Python uses only the standard library. Runtime uses vanilla JavaScript. Optional Google Fonts gracefully fall back to system fonts.

## Interview walkthrough
1. Open Decision overview: explain why retention is the first wedge.
2. Open Customer explorer: filter a cohort, inspect a customer, export its planning list.
3. Open Experiment lab: distinguish observed lift from causal impact; change scenario costs.
4. Open Data trust: explain incompatible denominators and missing production metadata.
5. Open Product strategy: connect the PRD to engineering and staged rollout.

The user confirmed the supplied dataset is synthetic and approved for public sharing. No synthetic augmentation was used. This prototype does not send messages, validate model performance, or claim realized retention improvement. The production architecture and prospective pilot are proposals.

## Delivery status
Local product and documentation complete. Automated data and UI-logic checks pass. Browser visual QA is unverified because no browser is connected. Local HTTP binding was denied; private Sites publication was blocked by DNS/network access to the source host. A Site ID is retained in the hosting manifest for a later deployment; no live URL is claimed.

## GitHub Pages
The deployable website is in `site/`. GitHub Actions publishes it on pushes to main. Enable Settings → Pages → GitHub Actions. The original local product folder is excluded because it contains separate Git metadata. Data is user-confirmed synthetic and approved for public sharing.

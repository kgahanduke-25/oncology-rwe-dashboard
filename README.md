# Oncology RWE Dashboard

**🔗 Live dashboard: https://kgahanduke-25.github.io/oncology-rwe-dashboard/**

An interactive dashboard of the oncology clinical-trial landscape, pulled **live
from the ClinicalTrials.gov API (NIH/NLM)** and framed around where **real-world
evidence (RWE)** is most needed. A single self-contained HTML file — it opens in a
browser and deploys on GitHub Pages with no build step.

---

## What it does

- **Live data.** On load and on every filter change, it queries the
  ClinicalTrials.gov v2 API (`/api/v2/studies`, CORS-enabled) with `countTotal`
  across phase, study-type, and status slices. A status badge shows **LIVE** when
  the fetch succeeds.
- **Offline fallback.** If the API is unreachable (offline, blocked, rate-limited),
  it falls back to an **embedded real snapshot** retrieved 4 Jul 2026, and the
  badge switches to **SNAPSHOT** so the source is never ambiguous.
- **Filter.** A cancer-type selector (All / Breast / Lung / Colorectal / Prostate)
  re-slices every KPI and chart.
- **KPI cards.** Total trials, observational studies, Phase 4 (post-approval), and
  a derived **RWE evidence share** = (observational + Phase 4) ÷ total.
- **Charts (Chart.js).** Trials by phase; interventional vs observational;
  recruitment status; early- vs late-stage balance.
- **RWE framework panel.** The five drug-class RWE gaps (accelerated approval,
  single-arm, checkpoint inhibitors, CAR-T, underrepresented populations), with
  severity encoded by fill **and** label for colorblind accessibility.

---

## Honest reading

- KPI counts are **live registration counts** — they measure trial activity, not
  evidence quality or gap size, and shift as the registry updates.
- The **RWE evidence share** is a derived approximation; observational studies and
  Phase 4 trials are largely disjoint but the bucket is a proxy, not a strict
  taxonomy.
- The **five-gap severity ranking is a qualitative expert framework**, not a
  measured quantity.
- Broad condition matching (e.g. `cancer`, `breast cancer`) includes registry
  synonyms — counts are indicative, not exact denominators.

---

## Data source

ClinicalTrials.gov API v2 — `https://clinicaltrials.gov/api/v2/studies`
Public domain (NIH / U.S. National Library of Medicine). No key required.

Snapshot embedded as fallback (retrieved 4 Jul 2026):

| Type | Total | Observational | Phase 4 |
|---|---|---|---|
| All cancers | 121,426 | 25,251 | 2,566 |
| Breast | 16,567 | 3,612 | 340 |
| Lung | 14,309 | 3,090 | 237 |
| Colorectal | 10,126 | 2,405 | 169 |
| Prostate | 7,463 | 1,412 | 147 |

---

## Run locally

Just open `index.html` in any browser — there is no build step and no dependencies
to install. The live fetch works from `file://`, GitHub Pages, or any static host.

---

## Deployed with GitHub Pages

This repo is published via **Settings → Pages → Deploy from a branch → `main` / root**.
The live fetch works from GitHub Pages because the API sends
`access-control-allow-origin: *`.

---

## License

MIT for the code (see [`LICENSE`](LICENSE)). Trial data © ClinicalTrials.gov
(NIH/NLM), public domain.

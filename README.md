# WellGuard | DATA TITANS — DSMLC Datathon 2026

**Predict risk · Prioritize inspections · Support better production decisions**

**Research question:** How can predictive maintenance and production optimization analytics help Strathcona Resources identify high-priority wells, prioritize inspections, and support data-driven decisions to reduce operational losses?

| Submission item | Link / location |
|---|---|
| **Live interactive WellGuard dashboard** | **Add deployed Streamlit Community Cloud URL** |
| **Five-minute summary video** | **Add publicly accessible video URL** |
| **Presentation slides** | **Add accessible slide URL or slides file** |
| **Registered team members** | **Insert exact registered members before submission** |

## Overview

WellGuard examines whether weekly risk rankings built from historical operating measurements can prioritize which wells to inspect when weekly review capacity is constrained. The research predicts a **recorded failure in the following 1–14 days**, evaluates rankings on chronologically later observations, and compares with a failure-recency baseline. This is **a retrospective research prototype**, not a live operational model or a demonstrated preventive-maintenance intervention.

## Open the full public interactive dashboard

The public Streamlit deployment contains the **10 major WellGuard sections**, with working filters and interactive charts:

| Page | What can be explored |
|---|---|
| **Executive Overview** | Saved historical research performance, 25/50/100 review-capacity comparisons, simulated fleet KPIs |
| **Fleet Map** | Fictional well footprint, sector and relative-risk filters; coordinates are not geographic |
| **Equipment Health** | Synthetic per-well pump, pressure, efficiency, downtime and oil-rate history |
| **Failure Records** | Example event explorer using synthetic records, plus actual dataset-level source counts |
| **Inspection Scheduler** | Rank fictional wells; change 25/50/100 slots, week, sector and repeat-review cooldown; download demo queue |
| **Model Validation Lab** | Saved reference ROC-AUC, average precision, monthly comparison, ablation / capacity evidence |
| **Maintenance Effectiveness** | Simulated service-job trends with clearly labelled non-causal pre/post comparisons |
| **Production & Downtime** | Simulated production, downtime and loss charts with date-range selection |
| **Data Reliability** | Dataset-level source coverage and synthetic demo telemetry completeness |
| **Well Investigator** | Explainable, deterministic investigation of fictional scores, sensor changes, jobs and losses |

### Crucial distinction: research benchmark vs. public demo

**Saved retrospective research aggregates** come from the competition analysis and are reproduced in `public_data/benchmark.json` and `public_data/monthly_summary.csv` as published summary metrics, **subject to organizer approval**. The original private source records are not included, so those aggregates are displayed, not recalculated online.

**All individual well identifiers (`DEMO-####`), positions, scores, sensor readings, maintenance records, failure examples and loss charts are entirely synthetic**, generated from a fixed seed in [`demo_data.py`](demo_data.py). They are fictional UI examples, not anonymized or reconstructed Strathcona data; they do **not** demonstrate real-world model accuracy or field savings. The app visibly identifies these sections as simulated. Its well investigator uses transparent rules, not autonomous diagnosis.

## Saved historical performance

Source datasets have **5,075,590** daily operating records, **15,610** maintenance jobs, and **2,873** reported failure rows. The reference model used three separate chronological periods:

| Period | Dates | Well-weeks |
|---|---|---:|
| Training | June 1, 2025 – March 1, 2026 | 48,865 |
| Validation | March 22 – May 17, 2026 | 11,149 |
| Test | June 7 – October 4, 2026 | 22,580 |

| Historical test metric | WellGuard reference | Failure-recency baseline |
|---|---:|---:|
| ROC-AUC | **0.8055** | 0.7243 |
| Average precision | **0.1637** | 0.1030 |
| Distinct eligible events flagged, 25 reviews/week | **116 / 643** | 75 / 643 |
| Distinct eligible events flagged, 50 reviews/week | **180 / 643** | 114 / 643 |
| Distinct eligible events flagged, 100 reviews/week | **289 / 643** | 188 / 643 |

At 25 weekly reviews, the historical benchmark identified **41 additional recorded events** relative to the same-capacity baseline. **This does not mean 41 failures were prevented**. The denominator 643 refers to the eligible test-event subset, not all reported failures. Rankings are not calibrated probabilities, and interventions were not prospectively tested.

## Deploy or run

**Streamlit Community Cloud:** Publish the **contents** of this folder to your GitHub repository root; select branch `main` and application entrypoint **`streamlit_app.py`**. No competition Parquet files, model binaries, or cloud secrets are needed for the public demo.

**Local:**

```bash
python -m pip install -r requirements.txt
python -m streamlit run streamlit_app.py
```

If the deployment fails, check Streamlit logs and confirm `streamlit_app.py`, `demo_data.py`, `requirements.txt`, `public_data/` and `.streamlit/config.toml` are all at the expected relative locations.

## Folder guide

| Path | Purpose |
|---|---|
| `streamlit_app.py` | Full ten-page **public-safe** Streamlit application |
| `demo_data.py` | Reproducible, explicitly **synthetic** example well-level data generator |
| `public_data/` | Saved real research **aggregate** metrics, not well-level source observations |
| `research_source/` | Research scripts and original private application **source code**, not the public entrypoint; requires separately authorized source data |
| `databricks/` | Optional reproducibility notebook / SQL (not evidence of an executed Databricks model run) |
| `docs/` | Evaluation methodology, source restrictions and references |
| `scripts/publication_preflight.py` | Static file and notebook-output release checks |
| `AI_USE_DISCLOSURE.md` | Competition-required assistance disclosure; verify details before final submission |
| `slides/`, `media/` | Optional location for slide and video references; video/slides can be hosted separately, with links above |

## Limitations and responsible data handling

Historical failure reporting changes over time. Key sensors are incompletely recorded. Source cost fields are generally estimates rather than actual costs. Observation changes before/after maintenance do not identify causal maintenance impact. No real well-level data, identifier, coordinate, historical score, job, private model artifact, credential or protected competition file is included in this GitHub release.

**Do not upload raw competition `.parquet` files, derived private CSV exports, location data or restricted screenshots**, even to an app repository. Follow [`docs/PRIVACY_AND_PUBLICATION.md`](docs/PRIVACY_AND_PUBLICATION.md). Saved aggregates may also require approval before public posting.

Only registered team members should contribute under the competition rules. The team must truthfully complete the organizer-required disclosure in [`AI_USE_DISCLOSURE.md`](AI_USE_DISCLOSURE.md). See [`docs/METHODOLOGY_AND_VALIDATION.md`](docs/METHODOLOGY_AND_VALIDATION.md) for performance provenance and uncertainty.

## Submission

Add exact registered team names, an accessible **five-minute video link**, the final presentation/slides link, and the live Streamlit URL above. The official submission requests a **public repository URL** in the Discord **`#submissions`** channel before **Sunday, November 22, 2026, 12:00 PM Calgary time**. Review [`SUBMISSION_CHECKLIST.md`](SUBMISSION_CHECKLIST.md) immediately before posting.

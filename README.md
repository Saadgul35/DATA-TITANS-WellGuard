# WellGuard | DATA TITANS — DSMLC Datathon 2026

**Predict Risk · Prioritize Inspections · Support Better Production Decisions**

### Team DATA TITANS

- **Saad Gul**
- **Dia Toredi**
- **Syed Ali**
- **Elnaz Ebrahimi**

### Research Question

How can predictive maintenance and production optimization analytics help Strathcona Resources identify high-priority wells, prioritize inspections, and support data-driven decisions to reduce operational losses?

## Project Resources

| Resource | Link |
|---|---|
| **Live Interactive Dashboard** | Coming soon — Streamlit deployment |
| **Five-Minute Demonstration Video** | [Watch Video](https://drive.google.com/file/d/1k9JjCHW6yomQqg_amaE4EvXxowXeUAj9/view?usp=drive_link) |
| **Final Competition Presentation** | [View Presentation](https://docs.google.com/presentation/d/1iyn9YzzsCQj7LIBIeJg3cTDimuVDbJBs/edit?usp=drive_link&ouid=117368338465875849058&rtpof=true&sd=true) |

## 1. Project Overview

**WellGuard** is a predictive maintenance and operational decision-support platform designed to help prioritize oil and gas well inspections using historical operating data, equipment performance indicators, and recorded failures.

The project addresses a practical operational challenge: **When inspection resources are limited, which wells should receive attention first?**

WellGuard combines historical failure-risk rankings, inspection scheduling, production monitoring, maintenance analysis, and explainable evidence to support engineering decisions.

The predictive research focuses on identifying wells at elevated risk of a recorded equipment failure within the following **1–14 days**.

The solution is a retrospective research prototype, not a live production system.

## 2. Interactive Dashboard

The public Streamlit application includes 10 major sections.

| Dashboard Section | Key Functionality |
|---|---|
| **Executive Overview** | Historical performance, inspection scenarios, fleet indicators |
| **Fleet Map** | Interactive fictional asset visualization and risk filters |
| **Equipment Health** | Pump performance, pressure, efficiency, production and downtime trends |
| **Failure Records** | Example failure events and historical dataset summary |
| **Inspection Scheduler** | Prioritized inspection queues with 25, 50 and 100 weekly review capacities |
| **Model Validation Lab** | ROC-AUC, average precision, chronological testing and baseline comparisons |
| **Maintenance Effectiveness** | Maintenance activity and pre/post operating comparisons |
| **Production & Downtime** | Production trends, recorded downtime and estimated loss analysis |
| **Data Reliability** | Data completeness, sensor availability and quality indicators |
| **Well Investigator** | Evidence-based explanations of well rankings and operating changes |

### Inspection Capacity Optimization

The Inspection Scheduler allows users to explore three operational scenarios:

- **25 reviews per week:** Highest-priority shortlist under constrained inspection capacity.
- **50 reviews per week:** Expanded inspection coverage.
- **100 reviews per week:** Broader coverage of the eligible fleet.

Users can explore inspection rankings, filtering criteria, historical capacity comparisons and supporting operating indicators.

## 3. Dataset Overview

The project analyzes three primary datasets provided for the competition.

| Dataset | Records |
|---|---:|
| Daily Production | 5,075,590 |
| Maintenance Jobs | 15,610 |
| Recorded Equipment Failures | 2,873 |

The analytical workflow includes data cleaning, date alignment, historical feature engineering, chronological validation, and failure-risk ranking.

## 4. Predictive Modeling and Validation

WellGuard evaluates historical operating measurements to rank wells by their relative risk of a recorded failure within the next 14 days.

The research uses a chronological training, validation and testing framework to reduce future-information leakage.

### Historical Data Splits

| Dataset | Period | Well-Week Observations |
|---|---|---:|
| Training | June 1, 2025 – March 1, 2026 | 48,865 |
| Validation | March 22 – May 17, 2026 | 11,149 |
| Testing | June 7 – October 4, 2026 | 22,580 |

### Model Performance

| Metric | WellGuard Reference Model | Failure-Recency Baseline |
|---|---:|---:|
| ROC-AUC | **0.8055** | 0.7243 |
| Average Precision | **0.1637** | 0.1030 |
| Events Flagged — 25 Reviews/Week | **116 / 643** | 75 / 643 |
| Events Flagged — 50 Reviews/Week | **180 / 643** | 114 / 643 |
| Events Flagged — 100 Reviews/Week | **289 / 643** | 188 / 643 |

### Key Finding

At a weekly review capacity of 25 wells, WellGuard's historical ranking flagged **116 eligible recorded failure events**, compared with **75 events** using the failure-recency baseline.

This represents **41 additional historical events identified** at the same inspection capacity.

These results demonstrate retrospective prioritization performance. They do not establish that failures were prevented or that production losses were recovered.

## 5. Research Methodology

The project follows an evidence-driven analytical workflow:

1. **Data Preparation:** Clean and align daily production, maintenance and failure records.
2. **Feature Engineering:** Develop historical operating indicators, sensor trends, variability measures and past failure context.
3. **Predictive Modeling:** Evaluate a LightGBM-based reference model using chronological data splits.
4. **Model Validation:** Assess classification performance and compare inspection rankings against a failure-recency baseline.
5. **Inspection Prioritization:** Generate capacity-aware inspection scenarios.
6. **Operational Investigation:** Examine production, downtime, maintenance and equipment indicators to support review decisions.

Additional methodology and validation details are provided in [docs/METHODOLOGY_AND_VALIDATION.md](docs/METHODOLOGY_AND_VALIDATION.md).

## 6. Public Dashboard and Data Handling

The public dashboard uses two clearly distinguished data sources.

**Historical Research Results**

Saved aggregate model-performance results and retrospective comparisons are stored in `public_data/`. They summarize earlier competition analyses and are not recalculated from private source records in the deployed application. Public release of these aggregates remains subject to applicable organizer permissions.

**Interactive Demonstration Data**

Individual demonstration wells, equipment measurements, rankings, coordinates, maintenance records and example events are synthetic.

The synthetic data is generated reproducibly through `demo_data.py` and supports interactive exploration without exposing restricted competition information.

The public demonstration does not represent a live operational deployment or independently validate field-level predictions.

## 7. Technology Stack

| Technology | Application |
|---|---|
| Python | Data processing and application development |
| Pandas / NumPy | Data analysis and transformation |
| LightGBM | Historical failure-risk modeling |
| Scikit-learn | Model evaluation and validation |
| Streamlit | Interactive dashboard development |
| Plotly | Interactive data visualization |
| Databricks / SQL | Analytical workflow and reproducibility materials |
| GitHub | Source-code management and project documentation |

## 8. Running the Dashboard

The public application can be deployed through Streamlit Community Cloud or executed locally.

**Streamlit Cloud Configuration**

- Repository: `DATA-TITANS-WellGuard`
- Branch: `main`
- Main file: `streamlit_app.py`
- Dependencies: `requirements.txt`

**Local Execution**

```bash
python -m pip install -r requirements.txt
python -m streamlit run streamlit_app.py
```

## 9. Repository Structure

| File / Directory | Description |
|---|---|
| `streamlit_app.py` | Main interactive WellGuard dashboard |
| `demo_data.py` | Synthetic demonstration data generator |
| `requirements.txt` | Python dependencies |
| `public_data/` | Saved aggregate research results |
| `research_source/` | Research scripts and private-data application source |
| `databricks/` | Databricks notebook and SQL files |
| `docs/` | Research methodology and supporting documentation |
| `tests/` | Application and data-validation tests |
| `.streamlit/` | Streamlit application configuration |
| `AI_USE_DISCLOSURE.md` | AI-use disclosure |

## 10. Limitations and Future Development

Historical failure reporting varies over time, and some sensor measurements are incomplete. Source cost figures are generally estimates rather than actual expenditures.

Model scores support relative prioritization rather than calibrated failure probabilities. Observed changes after maintenance do not establish causal effects.

Future development could include prospective validation, integration with operational data systems, field inspection feedback, improved model monitoring and evaluation of realized operational outcomes.

Restricted competition datasets and individual well-level source records are not distributed in this repository. Public demonstrations use synthetic well-level examples.

## AI-Use Disclosure

The project's AI-use disclosure is provided in [AI_USE_DISCLOSURE.md](AI_USE_DISCLOSURE.md).

---

**DATA TITANS | DSMLC Datathon 2026**

*WellGuard — Predict Risk. Prioritize Reviews. Verify Evidence.*

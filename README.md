# Applied Bioinformatics Case Study

This repository contains the code, data processing pipeline, and
exploratory analysis for the Applied Bioinformatics coursework case
study (2026).

The project is structured as a small Python package using a `src/`
layout, with data loading and preprocessing logic separated from
notebooks and analysis code.

---

## Objective

The dataset reflects the operational state of a large-scale
biotechnological process as it was 5 years ago. Product yield across
batches is variable, and **the aim of this case study is to identify
the process variables that contribute to this loss of productivity
across the highest-yielding batches**.

Sensor data are captured every 5–15 minutes across 17 process
parameters for 22 batches (the "4000 series operating data"), and
laboratory data are captured at ~4-hour intervals for 21 of those
batches.

The goal is to use the 21 "training" batches to identify
the key process variables that influence product yield, and to build
a purely data-driven model to predict the yield of the 22nd
("held-out") batch.

A video describing the approach and findings is available
[here](https://drive.google.com/file/d/1V2SJLrhUw0qJgARJ5uQvjEYWt_mJh2-d/view?usp=drive_link).

An infographic of the project is available in
[Infographic Applied ML.pdf](Infographic%20Applied%20ML.pdf).

---

## Results

Several ML models were evaluated using two feature representations:
aggregated batch statistics (B) and time-series-derived features (D).
Models were ranked by RMSE (lower is better):

| Model        | Feature Set          | RMSE     |
| ------------ | -------------------- | -------- |
| HistGB       | Batch Statistics     | 26.01    |
| Ridge        | Time-Series          | 23.56    |
| Ridge        | Batch Statistics     | 22.23    |
| ElasticNet   | Time-Series          | 22.21    |
| Lasso        | Time-Series          | 22.11    |
| RandomForest | Time-Series          | 17.48    |
| RandomForest | Batch Statistics     | 16.29    |
| XGBoost      | Batch Statistics     | 13.72    |
| XGBoost      | Time-Series          | 9.54     |
| ElasticNet   | Batch Statistics     | 8.93     |
| HistGB       | Time-Series          | 8.89     |
| **Lasso**    | **Batch Statistics** | **7.49** |

**Lasso regression on batch statistics performed best**, achieving the
lowest RMSE of **7.49**. Using this model, the predicted yield for the
held-out 22nd batch was **539.13 kg/hr**.

---

## Setup Instructions

### 1. Create and activate a virtual environment

```bash
python -m venv .venv
```

On Windows:

```bash
.venv\Scripts\activate
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

---

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

---

### 3. Install the project package (editable mode)

```bash
pip install -e .
```

This makes the `applied` package importable in notebooks and scripts.

---

## Usage

After installation, project modules can be imported as:

```python
from applied.data_processing import build_features_and_target
```

Raw data are loaded from the `data/` directory, and notebooks are
intended to be run from the `notebooks/` folder.

---

## Notes

- Tested with Python 3.10+
- The `src/` layout is used to avoid import ambiguity and ensure clean
  separation between source code and analysis notebooks.
- Parallel sensor channels (e.g. liquid inflow streams) are aggregated
  based on physical interpretation, as described in the accompanying
  analysis.

---

```

```

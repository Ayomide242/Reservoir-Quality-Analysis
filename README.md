# Reservoir Quality Analysis — GCA Capstone Project

A data-driven petrophysical analysis of well log data to identify and quantify the best-quality reservoir intervals in a Niger Delta well.

---

## Project Objective

This project focuses on identifying the best quality rock (reservoir) using data logic applied to wireline log data from **Well A** (a Niger Delta well). By combining statistical facies discrimination, feature engineering, and boolean filtering, the analysis delivers a quantified Net Pay result that can directly inform field development decisions.

---

## Workflow

1. **Import Libraries** — `lasio`, `numpy`, `pandas`, `matplotlib`, `seaborn`
2. **Dataset Loading & Cleaning** — Load `.LAS` file, handle null values, inspect well metadata and curve information
3. **Statistical Facies Discrimination** — Gamma Ray histogram analysis to justify and select GR cutoffs
4. **Feature Engineering** — Compute the Reservoir Quality Index (RQI)
5. **Net Pay Quantification** — Apply pay sand criteria and calculate gross thickness, net pay, and NTG

---

## Key Results

| Metric | Value |
|---|---|
| Reservoir Gross Thickness | ~941.98 m |
| Net Pay Thickness | ~379.02 m |
| Net-to-Gross (NTG) | **40.24%** |

---

## Methods & Techniques

### GR Cutoffs (Niger Delta Context)
The Gamma Ray histogram reveals a **bimodal distribution** consistent with interbedded sand-shale sequences of the **Agbada Formation**. Two cutoffs were evaluated:
- **60 API** (industry standard) — conservative cutoff for clean sand discrimination
- **75 API** (high-side) — captures marginal sands in the transition zone

### Reservoir Quality Index (RQI)
A custom feature engineered to move beyond simple lithology identification:

```
RQI = Porosity × (1 − GR_norm)
```

GR values are normalised to a 0–1 range (0 = cleanest sand, 1 = purest shale), making RQI a dimensionless index that highlights intervals that are **both clean and porous** — the most productive sands.

### Net Pay Criteria
Pay sands are defined by simultaneous satisfaction of:
- **GR ≤ 60 API** (clean sand)
- **Porosity ≥ 0.15** (sufficient storage capacity)

---

## Visualisations

- **4-track well log plot** — GR (with cutoff), RT, RHOB, NPHI
- **Correlation heatmap** — relationships between all log curves
- **GR distribution histogram** — with 60 API and 75 API cutoff lines annotated
- **2-track RQI plot** — GR vs Reservoir Quality Index (gold fill = good reservoir)
- **3-track Net Pay plot** — Lithology filter | Porosity filter | Pay flags (gold)

---

## Technologies Used

| Library | Purpose |
|---|---|
| `lasio` | Read and parse `.LAS` well log files |
| `pandas` | Dataframe manipulation and filtering |
| `numpy` | Numerical operations and null value handling |
| `matplotlib` | Well log track plots and visualisations |
| `seaborn` | Correlation heatmap |

---

## Getting Started

### Prerequisites
```bash
pip install lasio numpy pandas matplotlib seaborn
```

### Run the Notebook
1. Clone this repository
2. Place `Well_A.las` in the same directory (or update the file path in the notebook)
3. Open and run `GCA_Capstone_Project.ipynb` in Jupyter Notebook or JupyterLab

---

## Dataset

The input dataset is a **LAS (Log ASCII Standard)** file (`Well_A.las`) containing the following curves:

| Curve | Unit | Description |
|---|---|---|
| DEPT | ft | Depth (~4,800 – 8,000 ft) |
| GR_NM | API | Gamma Ray |
| RT | ohm·m | True Resistivity |
| RHOB / FDC | g/cc | Bulk Density |
| NPHI / POR | v/v | Neutron Porosity |
| CALF | in | Caliper |

> **Note:** The LAS file is not included in this repository. Please provide your own dataset or contact the author.

---

## Author

Developed as a capstone project for the **Geoscience & Computing Analytics (GCA)** programme.

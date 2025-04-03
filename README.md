# 🏗️ JaamSim Simulation Data Prep – Dereks Paints

This repository contains the full workflow for preparing real-world process data from **Dereks Paints** for use in a **Discrete Event Simulation** using **JaamSim**.

---

## 📁 Repository Contents

### 🧪 Notebooks
- `data_exploration.ipynb`  
  → Initial EDA: Machine usage, duration distributions, right-skew, and log-transforms.
  
- `data_notebook_summary.ipynb`  
  → Full pipeline for aggregating batch durations, fitting distributions, and preparing JaamSim-ready input parameters.

### 📂 Data
- `filtered_data.csv`  
  → Cleaned dataset used across notebooks, includes:
  - `batch_no`, `machine`, `step_name`, `duration_min`, `machine_group`, and `log_duration`
  - 720 total rows after preprocessing

---

## 📊 Workflow Summary

### 1. **Initial Data Cleaning**
- Selected relevant columns: `Product Code`, `Step Name`, `Machine`, `Duration (min)`
- Renamed for readability
- Extracted `machine_group`, `machine_prefix`, and `machine_num`

### 2. **Exploratory Analysis**
- Performed frequency counts of machines
- Visualised duration distributions by machine and step
- Applied log-transformation to address skew
- Conducted normality tests

### 3. **Batch-Level Aggregation**
Grouped total duration per `batch_no` per machine:
```python
summary_by_machine = (
    filtered_data
    .groupby(['batch_no', 'machine'])['duration_min']
    .sum()
    .reset_index()
)
```

### 4. **Distribution Fitting**
- Fitted multiple distributions (`lognorm`, `norm`, `gamma`, `triang`, `expon`) to each machine's batch durations
- Used **Kolmogorov-Smirnov test** to identify best-fitting distribution
- Extracted parameters from `scipy.stats.fit()`

### 5. **JaamSim Parameter Extraction**
Mapped results to JaamSim input format:
- `LogNormalDistribution`: Location, Scale, NormalMean (log(scale)), NormalStandardDeviation
- `NormalDistribution`: Mean, StdDev
- `Gamma`, `Exponential`: Shape, Location, Scale

---

## ✅ Example Output

| Machine | Distribution | Location | Scale | NormalMean | NormalSD |
|---------|--------------|----------|-------|------------|----------|
| PMX-2   | LogNormal    | 86.84    | 81.01 | 4.39       | 0.53     |
| BKM-5   | Exponential  | 240.0    | 315.27| —          | —        |

---

## 🚀 How to Use

1. Load your production log into `filtered_data.csv`
2. Run `data_notebook_summary.ipynb` to:
   - Fit distributions
   - Output JaamSim-ready table
3. Paste the parameters into your JaamSim `Server` or `EntityGenerator` blocks

---

## 📌 Notes

- All durations are in **minutes**
- LogNormal fits dominate due to right-skew
- Re-fitting or fixed values suggested for machines with invalid parameters or low counts

---

## 👨‍💻 Author
Prepared by Isaiah 
For Simulation Modeling Analysis Project – Engineering Systems & Design


# 🧪 Data Analysis for Dereks Paints

This repository contains a Jupyter Notebook developed as part of a **Simulation Modelling & Analysis** course project. The notebook documents a full data cleaning and exploratory analysis pipeline applied to **real-world production data** provided by an **industry mentor**. The analysis focuses on process durations and machine usage across batches in a paint manufacturing context.

---

## 📁 Dataset Overview

The dataset, `data_sma.csv`, contains real sample data from a production environment. Each row represents a single step in a batch production process.

### 📊 Columns Included:

| Column                  | Description                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| `Key`                  | Unique identifier for each process record                                   |
| `Batch No.`            | Identifier for each production batch                                        |
| `Product Code`         | Code for the specific product manufactured                                  |
| `Description`          | Description of the product or batch                                         |
| `Process/Step Name`    | Name of the process or production step                                      |
| `Machine`              | Identifier of the machine used for the step                                 |
| `Start Datetime`       | Start timestamp of the process                                              |
| `End Datetime`         | End timestamp of the process                                                |
| `Process Duration (min)` | Total duration of the process in minutes                                  |

---

## 🔍 Analysis Objectives

1. **Understand batch and machine-level process durations**
2. **Clean and standardise the data**
3. **Filter representative data using IQR**
4. **Manually analyse quantiles per machine**
5. **Fit machine performance to normal distributions**
6. **Identify variability and operational inefficiencies**

---

## 🛠️ Methods Used

### 🧹 Data Cleaning & Transformation

- Renamed columns for code readability
- Converted datetime fields to pandas datetime format
- Summarised batch-level processing times
- Removed extreme outliers using IQR filtering

### 📐 Grouping & Aggregation

- Grouped data by batch number and machine
- Calculated total process durations per batch and per machine
- Selected “representative” batches based on IQR

### 📊 Exploratory Data Analysis

- Visualised batch durations using histograms and box plots
- Computed descriptive statistics (mean, quartiles, std dev)

### 📈 Manual Quantile Analysis (per machine)

- Analysed 5th and 95th percentiles for each machine group (e.g., “BKM”)
- Fitted processing durations to normal distributions to assess performance stability

---

## 📌 Key Takeaways

- **Production process durations showed high variability**
- **Outlier filtering helped focus the analysis on representative batches**
- **Distinct performance differences were identified across machines**
- **Normal distribution fitting validated our modelling assumptions**

---

## 📚 Technologies

- Python 3
- pandas, numpy
- matplotlib, seaborn
- scipy.stats

---

## 🧑‍🎓 Developed For

**Simulation Modelling & Analysis**  
Singapore University of Technology and Design (SUTD)  
Academic term project — 2025

---

## 📄 Authors

This analysis was completed as a collaborative team project.  
Please refer to the final report and Jupyter Notebook for full documentation of our methods and insights.


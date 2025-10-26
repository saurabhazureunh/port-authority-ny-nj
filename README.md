# Port Authority NY & NJ
The Port Authority Tunnels and Bridges

This repository contains Jupyter notebooks and datasets designed to clean, merge, analyze, and engineer features for transportation-related data — including Port Authority Bus Terminal (PABT) Bus & Passenger records and traffic mobility data.

---

## 📓 Notebooks Overview

### **1. data_ingestion_bus_passenger.ipynb**
Merges the **PABT Bus** and **Passenger** datasets on `Carrier`, `StartDate`, and `EndDate`.

**Key Features**
- Aggressively cleans carrier names (case, spaces, punctuation) to maximize merge success.  
- Normalizes data types — parses Bus dates as day-first and extracts date parts from passenger records.  
- Performs a comprehensive **outer join**, filling unmatched carrier-date combinations with zeros.  

**Outputs**
- Full raw merged dataset (for auditing).  
- Reduced dataset with essential columns:  
  `StartDate`, `EndDate`, `Carrierclean`, `VolumeBus`, `VolumePassenger`.  
- *(Advanced)* Adds log-transformed counts, outlier capping, carrier-specific normalization, zero-inflation flags, and zero-inflated Poisson features for predictive analytics.

---

### **2. exploratory_data_analysis.ipynb**
Provides a **generic EDA (Exploratory Data Analysis)** function applicable to all main datasets.

**Key Features**
- Checks for nulls, duplicates, leading/trailing spaces, zero-length strings, and distinct values per column.  
- Performs data validation and summary statistics.  
- Auto-generates visualizations: histograms, boxplots, scatterplots, and correlation matrices.  
- Modular design — just pass your `DataFrame` and dataset name.  
- Includes progress tracking for large dataset processing.

---

### **3. feature_engineering_traffic.ipynb**
Cleans and enriches the **All Recorded Traffic** dataset, optimized for scalability.

**Key Features**
- Reads data in chunks for efficiency.  
- Standardizes time/date columns, handles missing values, and converts categorical fields to numeric.  
- Validates total class sums and detects mismatches.  
- Engineers advanced features:
  - Temporal flags: `IsWeekend`, `IsHoliday`, `Season`, `WeekOfYear`, `Hour`, `TimeOfDay`.  
  - Lagged and rolling statistics for trend capture.  
  - Violation rates, class totals, and stratified sampling.  
- Outputs:
  - Fully engineered dataset (ready for analysis).  
  - Sample version for rapid dashboarding and prototyping.  

---

## 📁 Data Files

### **Merged_PABT_Bus_Passenger_For_PowerBI.csv**
**Description:**  
Merged, cleaned, and standardized records from the PABT Bus and Passenger datasets.  

**Features**
- Essential columns: `StartDate`, `EndDate`, `Carrierclean`, `VolumeBus`, `VolumePassenger`.  
- Missing values replaced with zero for consistency.  
- Fully standardized carrier names.  
- Ready for Power BI or similar visualization tools.

---

### **Merged_PABT_Bus_Passenger_For_Predictive.csv**
**Description:**  
Enhanced version of the merged bus-passenger dataset, enriched for predictive modeling.

**Features**
- Includes log-transformed counts, capped outliers, zero-inflation flags, and carrier-normalized metrics.  
- Suitable for regression or ML models (e.g., demand forecasting).  
- Includes probability-like engineered features (flag rates, z-scores).

---

### **Merged_Traffic_Mobility_Data_Full.csv**
**Description:**  
Comprehensive outer join of traffic volume and mobility speed data by facility and month.

**Features**
- Includes all possible Facility–Month combinations.  
- Fills missing values with zeros for full coverage.  
- Ideal for historical trend and gap analysis.

---

### **Merged_Traffic_Mobility_Data_FILTERED.csv**
**Description:**  
Filtered subset of the above, including only months/facilities where both traffic and speed are non-zero.

**Features**
- Clean dataset for comparative studies and dashboards.  
- Excludes incomplete or estimated records.  
- Ensures higher accuracy and analytical consistency.

---

### **Traffic_PowerBI_Sample.csv.zip**
**Description:**  
Zipped, stratified sample (≈5%) of the All Recorded Traffic dataset for fast exploration.

**Features**
- Representative sampling by facility and month.  
- Includes all engineered columns.  
- Lightweight, ideal for demos, experimentation, or quick BI integration.

---

## 🧩 Project Purpose
This project streamlines the ingestion, validation, feature engineering, and visualization preparation of multi-source transportation datasets — enabling faster analytics, cleaner modeling inputs, and seamless integration with BI tools like Power BI.

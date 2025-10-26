# Port Authority NY & NJ
The Port Authority Tunnels and Bridges

This repository contains Jupyter notebooks and datasets designed to clean, merge, analyze, and engineer features for transportation-related data — including Port Authority Bus Terminal (PABT) Bus & Passenger records and traffic mobility data.

---

# Project Overview

### data_ingestion_bus_passenger.ipynb
This script merges the PABT Bus and Passenger datasets on Carrier, StartDate, and EndDate.

Carrier names are aggressively cleaned (case, spaces, punctuation) to maximize merge success.

Handles data type normalization: Bus date fields are parsed as day-first; passenger fields are standardized to extract only the date part.

After merging, unmatched carriers or date combinations are filled with zeros, ensuring a comprehensive outer join.

**Outputs:**

- The full, raw merged dataset for audit.
- A reduced dataset with essential columns (StartDate, EndDate, Carrierclean, VolumeBus, VolumePassenger).

---

### exploratory_data_analysis.ipynb
Contains a generic EDA function, designed to quickly analyze any of the four main datasets.

Performs checks for nulls, zero-length strings, distinct values per column, leading/trailing spaces, as well as duplicate detection and numeric summaries.

Includes data validation (type checks and summary statistics).

Automatically generates key plots: histograms, boxplots, scatterplots, and correlation matrices for numeric columns.

Built for modularity—just pass your DataFrame and name, and the EDA runs on any compatible dataset.

Makes use of progress tracking for loading and processing (useful for large datasets).


---

### feature_engineering_traffic.ipynb
Reads and cleans the All Recorded Traffic dataset, processing in efficient chunks for scalability.

Standardizes time and date columns, handles missing values, converts class columns to numeric, and fills as appropriate.

Computes total class sums and checks for mismatches with total.

**Feature engineering:**

- Adds flags: IsWeekend, IsHoliday, season, week-of-year, hour, and time-of-day.
- Calculates violation rates and class totals.
- Generates lagged and rolling statistical features to capture trends, improving downstream analysis or model inputs.
- Creates stratified samples for representative data subsetting.

Outputs both the fully-engineered, ready-to-analyze dataset and a sample version for rapid prototyping or dashboarding.

Supports downstream tools by preparing ready-to-load, analysis-friendly files; reduces need for repeated preprocessing in BI tools.


---

### Merged_PABT_Bus_Passenger_For_PowerBI.csv
**Description:**
This file contains the merged, cleaned, and standardized records from both the PABT Bus and Passenger datasets. It retains only essential columns (StartDate, EndDate, Carrierclean, VolumeBus, VolumePassenger) for straightforward analysis and seamless import into Power BI or other visualization tools.

**Features:**

- Each row corresponds to a unique combination of date, carrier, and passenger/bus counts.
- Missing values from unmatched merges are replaced with zero for consistency.
- All carrier names are standardized.


---

### Merged_PABT_Bus_Passenger_For_Predictive.csv
**Description:**
This version of the merged bus and passenger data includes advanced engineered features to support predictive modeling.

**Features:**

- Contains the original numeric counts plus log-transformed counts, capped outlier features, zero-inflation flags, and carrier-normalized values.
- Designed for machine learning or regression-based approaches (e.g., demand modeling, forecasting).
- Includes probability-like features such as flag rates and z-scores for each carrier.


---

### Merged_Traffic_Mobility_Data_Full.csv
**Description:**
The complete, outer-joined dataset linking all available traffic volumes (by facility and month) to the corresponding mobility speed data.

**Features:**

- Contains all combinations of Facility and Month found in either the traffic or speed records.
- Missing values for metrics not present in both datasets are filled with zero to ensure every combination is represented.
- Useful for full-coverage analysis (historical trends, gap analysis, facility-level reporting).


---

### Merged_Traffic_Mobility_Data_FILTERED.csv
**Description:**
A filtered subset of the above, including only those months and facilities where both traffic and speed data are non-zero.

**Features:**

- Ideal for comparative studies or dashboards requiring only valid, observed data points.
- Removes records with incomplete or estimated values for more focused, accurate analysis.


---

### Traffic_PowerBI_Sample.csv.zip
**Description:**
A zipped, sampled version of the All Recording Traffic dataset built for rapid testing and fast prototyping in tools like Power BI.

**Features:**

- Contains a stratified 5% sample by facility and month, capturing representative usage patterns and anomalies.
- Includes all feature-engineered columns used for deep-dive visual or statistical work.
- Quick to load; suitable for demos, experimentation, and initial model-building.


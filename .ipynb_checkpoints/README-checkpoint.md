# 🌍 Earthquake Insurance Risk Analysis in California

> County-level geospatial risk model for earthquake insurance in California.  
> Combines seismic data, housing vulnerability, and insurance coverage to highlight underinsured regions.

## 📌 Project Objective

This project analyzes earthquake activity and insurance-relevant risk factors across California counties. The primary goal is to identify high-risk regions and provide actionable insights to support insurance pricing models, underwriting, and risk assessment — with particular relevance for companies like **AAA Insurance**.

---

## 🔍 Key Questions

* Which counties in California are most vulnerable to earthquakes?
* Where do high-magnitude earthquakes most frequently occur?
* How does seismic risk align with regional demographics or housing data?
* Which regions may warrant premium adjustments or expanded coverage?
* Is it possible to develop a predictive model for estimating earthquake damage risk or potential insurance claims?

---

<details>
<summary>🧰 <strong>Tools & Technologies</strong> (click to expand)</summary>

* **Python**: pandas, geopandas, matplotlib, seaborn, folium, scikit-learn
* **Jupyter Notebooks**
* **Power BI / Tableau** (for future dashboards)
* **USGS Earthquake API**, **USGS Quaternary Fault Database**, and **U.S. Census TIGER/Line Shapefiles**

</details>

---

<details>
<summary>📂 <strong>Project Structure</strong> (click to expand)</summary>

```
earthquake_insurance_project/
├── data/                   # Raw input files (shapefiles, CSVs, exports)
├── notebooks/              # Jupyter notebooks organized by stage
│   ├── 01_data_collection.ipynb
│   ├── 02a_demographics_and_housing_data.ipynb
│   ├── 02b_insurance_variables.ipynb
│   ├── 02c_data_cleaning_and_preparation.ipynb
│   ├── 03a_fault_lines_integration.ipynb
│   ├── 03b_eda_and_underinsured_score.ipynb
│   └── 04_predictive_modeling.ipynb
├── output/                 # Processed data, charts, summaries
│   ├── gdf_ca_cleaned.parquet         # Full GeoDataFrame for analysis
│   ├── gdf_ca_cleaned.geojson         # Simplified for GIS tools
│   ├── gdf_ca_scored_v4.parquet       # Final version with risk scores
│   └── gdf_ca_scored_v4.geojson
├── maps/                   # 📍 Folium interactive maps (hosted on GitHub Pages)
├── scripts/                # Python helper scripts (optional)
├── dashboards/             # Power BI / Tableau dashboards (future)
├── README.md               # 📘 Project overview and insights
└── requirements.txt        # Python dependencies
```

</details>

---

## 🌍 Geospatial Accuracy Note

Early analysis used a simplified GeoJSON file that **missed historic events** (e.g. the 1906 San Francisco earthquake). This was caused by incomplete polygon boundaries.

To fix this, the project was upgraded to **official 2023 TIGER/Line shapefiles** from the U.S. Census. These high-resolution county geometries enabled accurate spatial joins and reliable historic analysis.

---

## 🔍 Data Filtering Notes

* Earthquakes **below Magnitude 4.0** were excluded, as they rarely cause damage or trigger insurance claims.
* The cleaned dataset includes **5,109 events** from **1769 to 2025** with `Mag ≥ 4.0`, focused exclusively on **California**.
* Data was collected from the **USGS Earthquake API** and processed with Python.

---

## 🚧 Project Status

* ✅ **Phase 0** – [Folder and structure initialized](https://github.com/annapiter/earthquake-insurance-analysis)
* ✅ **Phase 1** – [TIGER shapefiles loaded and mapped](https://github.com/annapiter/earthquake-insurance-analysis/blob/main/notebooks/01_data_collection.ipynb)
* ✅ **Phase 1** – [Earthquake data collected and filtered](https://github.com/annapiter/earthquake-insurance-analysis/blob/main/notebooks/01_data_collection.ipynb)
* ✅ **Phase 1** – [Spatial join of quakes to counties](https://github.com/annapiter/earthquake-insurance-analysis/blob/main/notebooks/01_data_collection.ipynb)
* ✅ **Phase 1** – [Exploratory Data Analysis (EDA): maps & time series](https://github.com/annapiter/earthquake-insurance-analysis/blob/main/notebooks/01_data_collection.ipynb)
* ✅ **Phase 2** – [Demographic & housing data collected and merged](https://github.com/annapiter/earthquake-insurance-analysis/blob/main/notebooks/02a_demographics_and_housing_data.ipynb)
* ✅ **Phase 2** – [Insurance variables merged (EQ coverage, homeowners policies, FEMA, loss ratios)](https://github.com/annapiter/earthquake-insurance-analysis/blob/main/notebooks/02b_insurance_variables.ipynb)
* ✅ **Phase 2.5** – [Data cleaning and formatting completed](https://github.com/annapiter/earthquake-insurance-analysis/blob/main/notebooks/02c_data_cleaning_and_preparation.ipynb)
* ✅ **Phase 3** – [Fault line features added: intersections, distance, length, azimuth](https://github.com/annapiter/earthquake-insurance-analysis/blob/main/notebooks/03a_fault_lines_integration.ipynb)
* ✅ **Phase 3** – [Exploratory Data Analysis & Derived Risk Score (e.g. underinsured regions)](https://github.com/annapiter/earthquake-insurance-analysis/blob/main/notebooks/03b_eda_and_underinsured_score.ipynb)
* 🕒 **Phase 4** – Predictive modeling
* 🕒 **Phase 4** – Dashboard visualization (Power BI or Tableau)

---

## 🧮 New Variables Added in Phase 2

The following indicators were loaded and merged into the extended GeoDataFrame:

| Variable                      | Source         | Description                                                             |
| ----------------------------- | -------------- | ----------------------------------------------------------------------- |
| `eq_takeup_pct`               | CDI (2023)     | % of residential units with earthquake insurance policies               |
| `homeowners_coverage_pct`     | CDI (2023)     | % of total housing units covered by homeowners insurance                |
| `modeled_loss_ratio_2018_pct` | CDI Risk Zones | Ratio of insured loss (PML) to total liability by EQ zone               |
| `fema_funding_earthquake`     | FEMA API       | Total public assistance obligated to each county (EQ-related disasters) |

✅ These variables enable comparative analysis of **risk vs coverage**, helping identify counties that may be **underinsured**, **highly exposed**, or both.

---

## 🌋 New Variables Added in Phase 3

The following variables were engineered during exploratory analysis and scoring. Only the final selected variables were retained in the exported dataset (`gdf_ca_scored_v4.parquet`).

### 🧱 Seismic Exposure (from fault lines)
| Variable                 | Description                                                       |
|--------------------------|-------------------------------------------------------------------|
| `intersects_fault`       | Whether a fault line intersects the county                        |
| `n_faults_intersecting`  | Number of named fault zones intersecting the county               |
| `faults_list`            | List of intersecting fault names                                  |
| `centroid_to_fault_km`   | Distance (km) from county centroid to nearest fault line          |
| `nearest_fault_km`       | Distance (km) from county boundary to nearest fault line          |
| `fault_length_km`        | Total length of fault segments within county boundary (km)        |
| `mean_fault_azimuth_deg` | Average orientation angle (azimuth) of faults in county           |
| `fault_orientation`      | Categorized fault direction (N–S, NE–SW, E–W, NW–SE, No Faults)    |

### 🌎 Earthquake History (from USGS API)
| Variable            | Description                                         |
|---------------------|-----------------------------------------------------|
| `eq_count`          | Total number of earthquakes (Mag ≥ 4.0)             |
| `eq_mean_mag`       | Mean earthquake magnitude per county                |
| `eq_max_mag`        | Strongest recorded earthquake per county            |

### ⚠️ Composite Risk & Vulnerability Scores

| Variable                   | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| `seismic_risk_score`       | Composite score based on fault proximity, fault length, and earthquake history |
| `vulnerability_score`      | Socioeconomic vulnerability based on poverty, renters, housing age, etc.   |
| `insurance_gap_score`      | Relative gap between risk level and insurance coverage                     |
| `underinsurance_risk_score`| Final combined score: seismic + vulnerability + insurance gap              |

✅ These variables power the final **Underinsured Risk Score**, identifying counties where **earthquake hazard meets social vulnerability and insurance gaps**.

---

## 💾 Output Formats & Data Fidelity

The project saves both intermediate and final cleaned datasets in **two formats**:

| Format       | Purpose                                       | File                             | Notes                                                                 |
|--------------|-----------------------------------------------|----------------------------------|-----------------------------------------------------------------------|
| `.parquet`   | ✅ Primary format for analysis and modeling    | `gdf_ca_scored_v4.parquet`       | Includes full feature set and native Python types (e.g., lists)       |
| `.geojson`   | ✅ For mapping, GIS tools, and GitHub Pages    | `gdf_ca_scored_v4.geojson`       | Flattened structure for compatibility (e.g., `faults_list` as string) |

> ⚠️ **Note:** GeoJSON is ideal for lightweight visualization but does not support nested structures. For modeling and full variable access, use the **Parquet** file.

---
## 📊 Key Deliverables

### ✅ Completed (Phases 1–3)
* 📍 **Interactive maps**: Strong, average, and maximum magnitude by county (Folium)
* 🗺️ **Choropleth maps**: Fault exposure, FEMA aid, insurance take-up, and risk scores
* 📈 **Timelines**: Decade-by-decade earthquake frequency and intensity
* 🧪 **EDA insights**: High-risk but underinsured regions highlighted using composite scores
* 💾 **Final dataset exports**: `gdf_ca_scored_v4.parquet` and `.geojson` with risk metrics

### 🕒 In Progress / Coming Next (Phase 4)
* 🤖 **Predictive modeling**: Estimate insurance take-up, loss probability, or composite risk
* 📊 **Dashboards**: Power BI / Tableau visualizations for stakeholders (e.g. AAA Insurance)
* 📍 **Strategic recommendations**: Pricing signals, coverage prioritization, and policy gaps

---

<details>
<summary>📈 <strong>Key Insights from EDA (click to expand)</strong></summary>

🧨 **Earthquake Activity**
- **San Bernardino**, **Humboldt**, and **Santa Clara** recorded the **highest number** of strong earthquakes (`Mag ≥ 6.0`)
- **San Luis Obispo (7.93)** and **San Francisco (7.90)** experienced the **strongest recorded magnitudes**
- Seismic activity is **geographically concentrated** — inland basins and coastal fault zones are most active
- Decade-level trends reveal **spikes in activity in the early and mid-20th century**

🗺️ **Geospatial Accuracy**
- Initial boundary errors were fixed using **2023 TIGER/Line shapefiles**, enabling recovery of key events (e.g. **1906 San Francisco earthquake**)
- Fault-line proximity and intersection metrics enabled precise **county-level hazard exposure scoring**

🏚️ **Socioeconomic Vulnerability**
- Several counties with **high seismic exposure** also score high in:
  - **Poverty rate**
  - **Pre-1980 housing**
  - **Renter share** and **vacant units**
  - **High age-dependency gaps** (more seniors, fewer children)

💸 **Insurance & Coverage Gaps**
- Earthquake **insurance take-up rates remain low** in many high-risk regions
- Counties with high modeled loss ratios (CDI) but low policy coverage were flagged
- FEMA funding shows **historical disaster relief patterns**, often concentrated in coastal and seismic hotspots

⚠️ **Underinsurance Hotspots**
- A composite **Underinsured Risk Score** was developed using:
  - Seismic Risk Score
  - Social Vulnerability Score
  - Insurance Gap Score
- Several counties were identified as **high-risk and underinsured**, including:
  - **Los Angeles**
  - **San Bernardino**
  - **Imperial**
  - **San Francisco**
  - **Humboldt**
  - **Inyo**

✅ These insights support **insurance pricing**, **underwriting**, and **public policy planning**.
</details>

---

## 🌐 Interactive Maps (Hosted via GitHub Pages)

Explore California's earthquake risk and insurance coverage interactively:

### 🧨 Earthquake Activity (1769–2025)
* [Strong Earthquakes by County (Folium)](https://annapiter.github.io/earthquake-insurance-analysis/strong_quakes_map.html)
* [Maximum Magnitude by County](https://annapiter.github.io/earthquake-insurance-analysis/max_magnitude_map.html)
* [Average Magnitude by County](https://annapiter.github.io/earthquake-insurance-analysis/avg_magnitude_map.html)
* [All Earthquakes – Clustered Timeline View](https://annapiter.github.io/earthquake-insurance-analysis/all_earthquakes_clustered.html)

### 🗺️ Fault Line Exposure
* [Counties Intersecting Fault Lines](https://annapiter.github.io/earthquake-insurance-analysis/map_fault_intersection.html)
* [Total Fault Line Length by County](https://annapiter.github.io/earthquake-insurance-analysis/map_fault_length_by_county.html)

### 💡 Social Vulnerability & Insurance Coverage
* [Seasonal Vacancy Rates (ACS)](https://annapiter.github.io/earthquake-insurance-analysis/map_seasonal_vacancy.html)
* [EQ Take-up Rate vs Seasonal Housing](https://annapiter.github.io/earthquake-insurance-analysis/map_seasonal_plus_eq_takeup.html)

### ⚠️ Underinsured Risk Hotspots
* [Underinsured Risk Score in Fault-Exposed Counties](https://annapiter.github.io/earthquake-insurance-analysis/map_underinsured_fault_zone.html)
* [Underinsured Risk Score in High-Quake Counties](https://annapiter.github.io/earthquake-insurance-analysis/map_underinsured_quake_zone.html)

These interactive maps combine **earthquake history**, **fault line geometry**, **housing and insurance data**, and **derived risk scores** to highlight vulnerable and underinsured counties across California.

---

## ✍️ Author

**Anna Piterskaya**
Aspiring Data Scientist | Based in California
🎯 Career Goal: Data Science role in the Insurance industry — especially at **AAA Insurance**
📧 GitHub: [annapiter](https://github.com/annapiter)

---

## 🚀 Next Steps

> ✅ Completed: Exploratory analysis of fault exposure, insurance coverage, and social vulnerability  
> ✅ Engineered composite scores: `seismic_risk_score`, `vulnerability_score`, `insurance_gap_score`, and `underinsurance_risk_score`  
> 🧠 Next: Develop predictive models to estimate earthquake insurance take-up, risk tiers, and expected loss  
> 📊 Visualize results in dashboards to support underwriting and strategic planning

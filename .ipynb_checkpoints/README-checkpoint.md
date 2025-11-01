# 🌍 Earthquake Insurance Risk Analysis in California

## 📌 Project Objective

This project analyzes earthquake activity and risk-relevant property indicators across California counties. The goal is to identify high-risk, underinsured regions and deliver actionable insights for **real estate analytics**, **insurance modeling**, and **PropTech applications** — supporting pricing strategy, risk communication, and public resilience planning.

It is especially relevant for organizations working in:
- **PropTech** and real estate investment platforms  
- **Insurance and catastrophe modeling firms** (e.g., AAA, CoreLogic, Hippo)  
- **Public sector** and resilience-focused data initiatives

---

## 🔍 Key Questions

* Which California counties face the greatest earthquake hazard?
* Where do strong earthquakes occur most frequently?
* How does seismic risk intersect with regional demographics and housing?
* Which counties may warrant premium adjustments or coverage expansion?
* Can we predict take-up gaps and quantify underinsurance exposure?

---

<details>
<summary>🧰 <strong>Tools & Technologies</strong> (click to expand)</summary>

* **Python**: pandas, geopandas, matplotlib, seaborn, folium, scikit-learn
* **Jupyter Notebooks**
* **Power BI / Tableau** (dashboard visualizations in progress)
* **USGS Earthquake API**, **USGS Quaternary Fault Database**
* **U.S. Census TIGER/Line Shapefiles**

</details>

---

<details>
<summary>📂 <strong>Project Structure</strong> (click to expand)</summary>

```
earthquake_insurance_project/
├── data/                          # Raw input files (shapefiles, CSVs, exports)
├── notebooks/                     # Jupyter notebooks by phase
│   ├── 01_data_collection.ipynb
│   ├── 02a_demographics_and_housing_data.ipynb
│   ├── 02b_insurance_variables.ipynb
│   ├── 02c_data_cleaning_and_preparation.ipynb
│   ├── 03a_fault_lines_integration.ipynb
│   ├── 03b_eda_and_underinsured_score.ipynb       # Clean version (no outputs)
│   ├── 03b1_preview.ipynb                          # Parts 1–2: Overview & Thematic EDA
│   ├── 03b2_preview.ipynb                          # Part 3a: Seismic Risk – Fault Exposure
│   ├── 03b3_preview.ipynb                          # Part 3b–4: Earthquake History & Scoring
│   ├── 04_predictive_modeling.ipynb
│   └── 04a_model_experiments.ipynb
├── output/                       # Processed data and summaries
│   ├── gdf_ca_cleaned.parquet
│   ├── gdf_ca_cleaned.geojson
│   ├── gdf_ca_scored_v4.parquet
│   ├── gdf_ca_scored_v4.geojson
│   ├── gdf_ca_predicted_v5.parquet
│   ├── gdf_ca_predicted_v5.geojson
│   └── predictions_eq_takeup.csv
├── maps/                         # 📍 Folium interactive maps (GitHub Pages)
├── scripts/                      # Helper Python scripts (optional)
├── dashboards/                   # Tableau / Power BI dashboards (WIP)
├── README.md                     # 📘 Project overview and insights
└── requirements.txt              # Python dependencies

```

</details>

---

## 🌍 Geospatial Accuracy Note

Early analysis used simplified GeoJSON boundaries that omitted key historic events (e.g. 1906 San Francisco quake). The project was upgraded to **2023 TIGER/Line shapefiles**, enabling accurate joins and correct event recovery.

---

## 🔍 Data Filtering Notes

* Only **earthquakes ≥ Magnitude 4.0** were retained to focus on impactful events
* Final dataset includes **5,109 earthquakes** from **1769 to 2025**, filtered to **California only**
* Data sourced via the **USGS Earthquake API**

---

## 🚧 Project Status

* ✅ **Phase 0** – Repo initialized, folder structure and planning scaffolded
* ✅ **Phase 1** – Earthquake data collected, filtered, and spatially joined to counties
* ✅ **Phase 2** – Demographic, housing, and insurance data merged (CDI, FEMA, ACS)
* ✅ **Phase 2.5** – Data cleaning, formatting, and feature engineering
* ✅ **Phase 3** – Fault lines integrated; composite risk and underinsurance scores developed
* ✅ **Phase 4** – Predictive modeling, feature interpretation, and residual analysis  
🕒 **Next** – Interactive dashboards (Tableau, Power BI) and portfolio presentation

---

## 🧮 Phase 2: Insurance Variables

| Variable                      | Source         | Description                                                             |
| ----------------------------- | -------------- | ----------------------------------------------------------------------- |
| `eq_takeup_pct`               | CDI (2023)     | % of residential units with earthquake insurance policies               |
| `homeowners_coverage_pct`     | CDI (2023)     | % of housing units covered by homeowners insurance                      |
| `modeled_loss_ratio_2018_pct` | CDI Risk Zones | Ratio of insured loss (PML) to total liability                          |
| `fema_funding_earthquake`     | FEMA API       | Public assistance (EQ-related disasters) obligated per county           |

✅ Enables comparisons of **coverage levels vs. risk exposure**

---

## 🌋 Phase 3: Fault Exposure & Composite Scores

### 🧱 Seismic Variables (from USGS Quaternary Faults)
| Variable                 | Description                                                       |
|--------------------------|-------------------------------------------------------------------|
| `intersects_fault`       | Fault line intersects county (True/False)                         |
| `n_faults_intersecting`  | Count of intersecting named fault zones                           |
| `faults_list`            | Names of intersecting faults                                      |
| `centroid_to_fault_km`   | Distance from county centroid to nearest fault                    |
| `nearest_fault_km`       | Distance from county boundary to nearest fault                    |
| `fault_length_km`        | Total fault length within county boundary                         |
| `mean_fault_azimuth_deg` | Mean orientation angle of fault segments                          |
| `fault_orientation`      | Categorized direction: N–S, NE–SW, E–W, NW–SE, or No Faults        |

### 🌎 Earthquake History (from USGS API)
| Variable       | Description                                |
|----------------|--------------------------------------------|
| `eq_count`     | Total earthquakes (Mag ≥ 4.0) per county   |
| `eq_mean_mag`  | Mean magnitude                             |
| `eq_max_mag`   | Strongest recorded earthquake per county   |

### ⚠️ Composite Scores
| Variable                   | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| `seismic_risk_score`       | Combines fault proximity, fault length, and earthquake activity             |
| `vulnerability_score`      | Socioeconomic risk: poverty, renters, pre-1980 housing, age dependency, etc.|
| `insurance_gap_score`      | Difference between modeled risk and actual insurance coverage               |
| `underinsurance_risk_score`| Final score: seismic + social vulnerability + insurance gap                 |

✅ Helps identify **counties where hazard, vulnerability, and low coverage align**

---

## 🤖 Phase 4: Predictive Modeling & Gap Estimation

Modeling was performed using **XGBoost Regression** and a **correlation-pruned feature set**, producing:

| Variable | Description |
|-----------|-------------|
| `predicted_eq_takeup_pct` | Modeled earthquake insurance take-up rate |
| `takeup_gap`              | Difference between predicted and actual coverage (in % points) |
| `gap_households`          | Estimated number of uncovered households |
| `gap_cost_usd`            | Approximate financial impact (households × $800/policy) |
| `underinsurance_tier`     | County classification: *High Gap & High Cost*, *High Cost*, *High Gap*, *Low Impact* |

✅ Enables **county-level gap quantification**, **cost estimation**, and **dashboard-ready outputs**

---

## 💾 Output Formats & Data Fidelity

| Format       | Purpose                                       | File                             |
|--------------|-----------------------------------------------|----------------------------------|
| `.parquet`   | Full-feature dataset with model predictions   | `gdf_ca_predicted_v5.parquet`    |
| `.geojson`   | Interactive mapping (Tableau / Folium)        | `gdf_ca_predicted_v5.geojson`    |
| `.csv`       | Tabular summary (actual vs predicted)         | `predictions_eq_takeup.csv`      |

> ⚠️ **Note:** Use `.parquet` for full model input/output; `.geojson` for visualization

---

## 📊 Key Deliverables

### ✅ Phases 1–3
* 📍 Interactive maps: earthquake activity, fault lines, social vulnerability
* 🗺️ Choropleths: FEMA funding, insurance take-up, risk scores
* 📈 Time-series: quake frequency and intensity by decade
* 🧪 Composite scores: `seismic_risk_score`, `vulnerability_score`, `insurance_gap_score`
* 💾 Final exports: `gdf_ca_scored_v4.parquet`, `.geojson`

### ✅ Phase 4
* 🤖 Predictive modeling: XGBoost (R² = 0.865), correlation-pruned features
* 🔍 Model interpretation: SHAP values, permutation importance, PDPs
* 💸 Gap analysis: $64M total shortfall; 16 counties = 93% of statewide risk
* 🗺 Residual maps: over- and underinsured counties
* 📤 Exports: `gdf_ca_predicted_v5.parquet`, `.geojson`, `predictions_eq_takeup.csv`
* 📊 Dashboards: Tableau / Power BI (in development)
* 📌 Strategy insights: region-specific pricing, coverage expansion recommendations

---

<details>
<summary>📈 <strong>Key EDA Insights</strong> (click to expand)</summary>

🧨 **Earthquake Activity**
- Highest quake counts: **San Bernardino**, **Humboldt**, **Santa Clara**
- Strongest magnitudes: **San Luis Obispo (7.93)**, **San Francisco (7.90)**
- Coastal faults and inland basins show highest activity
- Decade-level spikes in early and mid-20th century

🏚️ **Social Vulnerability**
- High-risk counties often show:
  - High **poverty**
  - Old (**pre-1980**) housing stock
  - High **renter** and **vacancy** rates
  - Large **age-dependency** gaps

💸 **Insurance Coverage Gaps**
- Many at-risk counties show **low take-up**
- High CDI loss ratios + low coverage = red flags
- FEMA funding follows seismic and coastal patterns

⚠️ **Underinsurance Hotspots**
- Top flagged counties: **Los Angeles**, **San Bernardino**, **Imperial**, **San Francisco**, **Humboldt**, **Inyo**
- Composite scoring reveals regions of **high exposure and low protection**

</details>

---

<details>
<summary>🤖 <strong>Key Modeling Insights (Phase 4)</strong> (click to expand)</summary>

📈 **Performance**
- Final model: XGBoost Regressor  
- R² = **0.865**, MAE = **1.69%**

🧠 **Top Features**
- Insurance: `homeowners_coverage_pct`, `modeled_loss_ratio_2018_pct`
- Seismic: `eq_max_mag`, `fault_length_km`, `centroid_to_fault_km`
- Demographics: `median_income`, `poverty_pct`, `age_0_17_pct`, `migrant_pct`
- Housing: `pre_1980_pct`, `for_sale_pct`, `seasonal_pct`

🗺 **Residuals**
- Underpredicted: **Mono**, **Inyo**, **San Luis Obispo**
- Overpredicted: **Imperial**, **Glenn**, **Tehama**

💸 **Gap Estimates**

The total estimated underinsurance gap is **$64 million statewide**, based on:

- Predicted vs. actual earthquake insurance take-up rates  
- An assumed per-household policy cost of **$800**

Counties were grouped into four underinsurance risk tiers based on % take-up gap and estimated financial cost:

- **High Gap & High Cost** – **$31.19M** (9 counties)  
  *Santa Clara, Contra Costa, Alameda, Fresno, Stanislaus, Imperial, Tulare, Merced, Tehama*

- **High Cost Only** – **$28.61M** (7 counties)  
  *Los Angeles, San Bernardino, San Joaquin, San Francisco, Sacramento, Riverside, Butte*

- **High Gap Only** – **$2.07M** (9 counties)  
- **Low Impact** – **$2.32M** (33 counties)

> 🧭 Together, the **top 16 counties in Tiers 1 and 2 account for $59.8 million**, or **93% of the total statewide underinsurance burden** — a priority for **insurance outreach, pricing optimization, and disaster mitigation**.

💸 **Gap Estimates**

The total estimated underinsurance gap is **$59.8 million statewide**, based on:

- Predicted vs. actual earthquake insurance take-up rates  
- An average per-household policy cost of **$800**

Counties were classified into two high-priority tiers:

- **High Gap & High Cost** *(Tier 1)*:  
  *Santa Clara, Contra Costa, Alameda, Fresno, Stanislaus, Imperial, Tulare, Merced, Tehama*

- **High Cost Only** *(Tier 2)*:  
  *Los Angeles, San Bernardino, San Joaquin, San Francisco, Sacramento, Riverside, Butte*

> 🧭 These **16 counties account for 93%** of the statewide underinsurance burden — a clear priority for **insurance outreach, pricing optimization, and disaster risk mitigation**.


🧪 **Interpretability**
- SHAP and PDP show nonlinear impact of risk and vacancy features
- Social vulnerability (poverty, migrant %, vacancy) → lower take-up

</details>

---

## 🌐 Interactive Maps (GitHub Pages)

### 📍 Gallery
👉 [View Full Map Gallery](https://annapiter.github.io/earthquake-insurance-analysis/maps/)

### 🧨 Earthquake Activity
- [Strong Earthquakes by County](https://annapiter.github.io/earthquake-insurance-analysis/maps/strong_quakes_map.html)
- [Max Magnitude by County](https://annapiter.github.io/earthquake-insurance-analysis/maps/max_magnitude_map.html)
- [Average Magnitude by County](https://annapiter.github.io/earthquake-insurance-analysis/maps/avg_magnitude_map.html)
- [All Quakes: Clustered View](https://annapiter.github.io/earthquake-insurance-analysis/maps/all_earthquakes_clustered.html)

### 🗺️ Fault Line Exposure
- [Counties Intersecting Faults](https://annapiter.github.io/earthquake-insurance-analysis/maps/map_fault_intersection.html)
- [Fault Line Length by County](https://annapiter.github.io/earthquake-insurance-analysis/maps/map_fault_length_by_county.html)

### 💡 Social Vulnerability & Insurance
- [Seasonal Vacancy Rates (ACS)](https://annapiter.github.io/earthquake-insurance-analysis/maps/map_seasonal_vacancy.html)
- [EQ Take-up vs. Seasonal Housing](https://annapiter.github.io/earthquake-insurance-analysis/maps/map_seasonal_plus_eq_takeup.html)

### ⚠️ Underinsurance Hotspots
- [Risk Score – Fault Zone Counties](https://annapiter.github.io/earthquake-insurance-analysis/maps/map_underinsured_fault_zone.html)
- [Risk Score – High Quake Counties](https://annapiter.github.io/earthquake-insurance-analysis/maps/map_underinsured_quake_zone.html)
- [Top 16 Underinsured Counties](https://annapiter.github.io/earthquake-insurance-analysis/maps/map_underinsured_top16.html)
- [Model Residuals](https://annapiter.github.io/earthquake-insurance-analysis/maps/map_residuals_folium.html)

---

## ✍️ Author

**Anna Piterskaya**  
Data Scientist | Based in California  
🎯 Career Goal: Data Science role in **PropTech**, Real Estate Analytics, or Risk Modeling — with interest in companies like **CoreLogic**, **Hippo**, **Zillow**, **AAA Insurance**, or **JMA Ventures**  
GitHub: [annapiter](https://github.com/annapiter)

This project was built independently with support from **AI tools** (including **ChatGPT**) for code review, markdown editing, and **iterative ideation**.

---

## 🚀 Next Steps

> ✅ Completed: Fault analysis, demographic scoring, insurance coverage modeling  
> ✅ Engineered composite scores: `seismic_risk_score`, `vulnerability_score`, `underinsurance_risk_score`  
> ✅ Trained predictive models, explained predictions, and estimated cost of underinsurance  
> 📊 **Next**: Build interactive Tableau dashboards and a presentation-ready PDF for portfolio/stakeholder use
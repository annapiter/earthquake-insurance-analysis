# 🌍 Earthquake Insurance Risk Analysis in California

## 📌 Project Objective
This project analyzes earthquake activity, seismic exposure, housing vulnerability, and insurance coverage across California counties. The goal is to identify high-risk, underinsured regions and produce actionable insights for **real estate analytics**, **insurance modeling**, and **risk-focused decision-making** — supporting pricing strategy, coverage planning, and resilience initiatives.

Relevant domains include:
- **PropTech** and investment platforms  
- **Insurance & catastrophe modeling** (AAA, CoreLogic, Hippo, Swiss Re)  
- **Public-sector resilience & emergency management**  

## 🔍 Key Questions
- Which regions face the highest seismic exposure?  
- Where are strong earthquakes concentrated historically?  
- How does seismic activity intersect with demographics and housing vulnerability?  
- Where are earthquake insurance coverage gaps most pronounced?  
- Can we predict take-up rates and quantify underinsurance exposure?  

## 🧰 Tools & Technologies
* Python (pandas, geopandas, scikit-learn, XGBoost, seaborn, matplotlib, folium)  
* Jupyter Notebooks  
* Tableau (interactive dashboards)  
* USGS Earthquake API  
* USGS Quaternary Fault Database  
* U.S. Census TIGER/Line Shapefiles  
* FEMA API, NAIC, CDI data  

## 📂 Project Structure

```
earthquake_insurance_analysis/
├── data/ # Raw input files
├── notebooks/ # Jupyter notebooks by phase
├── output/ # Processed datasets & model predictions
├── maps/ # Folium interactive maps (GitHub Pages)
├── dashboards/ # Tableau dashboards
├── README.md # Project overview
└── requirements.txt # Dependencies
```

## 🌍 Geospatial Accuracy
Boundary alignment was standardized using **2023 TIGER/Line county shapefiles**, enabling accurate joins and correct historical earthquake recovery — including the 1906 San Francisco event.

## 🔍 Data Scope
* **Magnitude ≥ 4.0** earthquakes  
* **5,109 events** from **1769–2025**  
* Processed via the **USGS Earthquake API**  
* Enriched with demographic, housing, and insurance variables  

## 🧱 Seismic Exposure Variables
### From USGS Quaternary Faults:
- Fault intersections  
- Count of fault zones  
- Fault length within county  
- Distance from centroid to nearest fault  
- Distance from boundary to nearest fault  
- Fault orientation metrics  

### From USGS Earthquake API:
- Earthquake count (Mag ≥ 4.0)  
- Maximum magnitude  
- Mean magnitude  
- Decade trends  

## 🧩 Composite Risk & Vulnerability Scores
Three composite indices were engineered:

| Score | Purpose |
|--------|---------|
| **Seismic Risk Score** | Fault proximity, fault length, earthquake history |
| **Vulnerability Score** | Poverty, age dependency, pre-1980 housing, renters, vacancy |
| **Insurance Gap Score** | Coverage misalignment vs. predicted need |
| **Underinsurance Risk Score** | Final combined index |

These scores highlight counties where hazard, vulnerability, and low coverage converge.

## 🤖 Predictive Modeling
A correlation-pruned feature set was used with **XGBoost Regression** to model earthquake insurance take-up rates.

### Model Outputs
| Output Variable | Meaning |
|------------------|---------|
| `predicted_eq_takeup_pct` | Modeled take-up rate |
| `takeup_gap` | Predicted – actual (percentage points) |
| `gap_households` | Number of households lacking coverage |
| `gap_cost_usd` | Estimated financial exposure |
| `underinsurance_tier` | Classification of counties |


## 💸 Underinsurance Findings
- **Total statewide underinsurance gap:** **~$64 million**  
- **16 counties** account for **93%** of the financial exposure  
- High-cost counties include:  
  *Los Angeles, San Bernardino, San Francisco, Sacramento, Riverside, Butte*  
- High gap + high cost counties include:  
  *Santa Clara, Alameda, Contra Costa, Fresno, Stanislaus, Tulare, Merced, Imperial, Tehama*  

These counties represent the greatest opportunity for **insurance outreach, mitigation funding, and pricing strategy optimization.**


## 💾 Outputs
| Format       | Purpose                          |
|--------------|----------------------------------|
| `.parquet`   | Full ML-ready dataset            |
| `.geojson`   | Interactive map visualization    |
| `.csv`       | Summary predictions              |

Key files include:
- `gdf_ca_scored_v4.parquet`  
- `gdf_ca_predicted_v5.parquet`  
- `predictions_eq_takeup.csv`  


## 🗺️ Interactive Maps (GitHub Pages)
Explore interactive Folium maps here:

👉 **https://annapiter.github.io/earthquake-insurance-analysis/maps/**

Includes:
- Earthquake clustering and intensity maps  
- Fault line exposure  
- Social vulnerability layers  
- Underinsurance tiers  
- Residual maps  


## 📊 Key Deliverables
- Comprehensive county-level risk, vulnerability, and insurance gap dataset  
- Feature-engineered ML-ready dataset with predictions  
- SHAP explainability and model interpretation  
- Interactive geospatial maps (Folium + GitHub Pages)  
- Tableau dashboards (completed)  
- Documentation and narrative insights  


## ✍️ Author
**Anna Piterskaya** — Data Scientist  
GitHub: https://github.com/annapiter  
LinkedIn: https://www.linkedin.com/in/annapiter  
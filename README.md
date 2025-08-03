# Earthquake Insurance Risk Analysis in California

## 📌 Project Objective

To analyze earthquake activity, demographics, and insurance-related factors in California at the county level. The goal is to identify high-risk regions and provide actionable insights that could support insurance pricing models and risk assessment strategies — particularly for companies like AAA Insurance.

## 🔍 Key Questions

- Which counties in California are most vulnerable to earthquakes?
- How does seismic risk relate to demographics like income, housing type, or population density?
- Where might insurers consider adjusting premiums or expanding earthquake insurance offerings?
- Can we build a predictive model to estimate potential risk or claims?

## 🧰 Tools & Technologies

- **Python**: pandas, geopandas, matplotlib, seaborn, folium, scikit-learn
- **Jupyter Notebooks**
- **Power BI / Tableau** (for future dashboarding)
- (Optional) USGS API, Census API, or scraped CSVs

## 📂 Project Structure

earthquake_insurance_project/
├── data/ # All raw input files (GeoJSON, CSVs, API exports)
├── notebooks/ # Jupyter notebooks organized by stage
├── output/ # Processed data, charts, maps, model outputs
├── scripts/ # Python scripts for cleaning, modeling (optional)
├── dashboards/ # Future visual dashboards (Power BI / Tableau)
├── README.md # Project overview and structure
└── requirements.txt # List of required Python packages

## 🗺️ Geospatial Accuracy Note

Initial versions of the project used a public GeoJSON file for California counties, which caused critical spatial join issues — notably, it failed to match the 1906 San Francisco earthquake (Magnitude 7.9) to San Francisco County. This was due to incomplete or oversimplified polygon data.

To ensure precise matching, the project was updated to use official U.S. Census Bureau **TIGER/Line shapefiles (2023)**. These high-resolution boundaries allowed accurate spatial joins for both modern and historic earthquake events, improving the reliability of county-level analysis.

## 🔍 Data Filtering Notes

To ensure the analysis focuses on meaningful, insurance-relevant events, earthquakes with magnitudes below 4.0 were excluded. Lower-magnitude quakes (3.5–3.9) are typically too minor to cause damage or result in insurance claims.

The dataset spans from 1769 (first recorded quake in California) through 2025, including 5,109 earthquake events of magnitude 4.0 or higher.

## 🚧 Project Status

- [x] Project folder and structure initialized
- [ ] Geographic map loaded and validated
- [ ] Earthquake data collected and cleaned (USGS or similar)
- [ ] Demographic and insurance data merged
- [ ] Exploratory Data Analysis (EDA) and visualization
- [ ] Machine learning risk modeling
- [ ] Dashboard or summary visualization (Power BI / Tableau)

## 📊 Potential Deliverables

- Interactive map of earthquake activity by county
- Clusters of high-risk / low-coverage regions
- Predictive model estimating earthquake damage risk or potential claims
- Dashboard summarizing key findings for stakeholders

## ✍️ Author

Anna Piterskaya — Aspiring Data Scientist based in California  
Working toward a data science role in the insurance industry (goal: AAA Insurance)


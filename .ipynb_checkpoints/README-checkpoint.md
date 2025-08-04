# 🌍 Earthquake Insurance Risk Analysis in California

## 📌 Project Objective

This project analyzes earthquake activity and insurance-relevant risk factors across California counties. The primary goal is to identify high-risk regions and provide actionable insights to support insurance pricing models, underwriting, and risk assessment — with particular relevance for companies like **AAA Insurance**.

---

## 🔍 Key Questions

- Which counties in California are most vulnerable to earthquakes?
- Where do high-magnitude earthquakes most frequently occur?
- How does seismic risk align with regional demographics or housing data?
- Which regions may warrant premium adjustments or expanded coverage?
- Is it possible to develop a predictive model for estimating earthquake damage risk or potential insurance claims?

---

<details>
<summary>🧰 <strong>Tools & Technologies</strong> (click to expand)</summary>

- **Python**: pandas, geopandas, matplotlib, seaborn, folium, scikit-learn  
- **Jupyter Notebooks**  
- **Power BI / Tableau** (for future dashboards)  
- **USGS Earthquake API** and **U.S. Census TIGER/Line Shapefiles**

</details>

---

<details>
<summary>📂 <strong>Project Structure</strong> (click to expand)</summary>
    
earthquake_insurance_project/
├── data/ # Raw input files (shapefiles, CSVs, exports)
├── notebooks/ # Jupyter notebooks organized by stage
├── output/ # Processed data, maps, charts, summaries
├── scripts/ # Python scripts (optional)
├── dashboards/ # Power BI / Tableau dashboards (future)
├── README.md # Project overview and insights
└── requirements.txt

</details>

---

## 🗺️ Geospatial Accuracy Note

Early analysis used a simplified GeoJSON file that **missed historic events** (e.g. the 1906 San Francisco earthquake). This was caused by incomplete polygon boundaries.

To fix this, the project was upgraded to **official 2023 TIGER/Line shapefiles** from the U.S. Census. These high-resolution county geometries enabled accurate spatial joins and reliable historic analysis.

---

## 🔍 Data Filtering Notes

- Earthquakes **below Magnitude 4.0** were excluded, as they rarely cause damage or trigger insurance claims.
- The cleaned dataset includes **5,109 events** from **1769 to 2025** with `Mag ≥ 4.0`, focused exclusively on **California**.
- Data was collected from the **USGS Earthquake API** and processed with Python.

---

## 🚧 Project Status

- ✅ Folder and structure initialized
- ✅ TIGER shapefiles loaded and mapped
- ✅ Earthquake data collected and filtered
- ✅ Spatial join of quakes to counties
- ✅ Exploratory Data Analysis (EDA): maps & time series
- 🔜 Merge demographic & housing data
- 🔜 Predictive modeling
- 🔜 Dashboard visualization (Power BI or Tableau)

---

## 📊 Potential Deliverables

- Static and interactive county-level maps (strong, average, max magnitude)
- Choropleth maps for rapid risk assessment
- Timeline plots of strong earthquake frequency by year & decade
- Cluster analysis to highlight high-risk, underserved regions
- Predictive model estimating county-level risk or expected claims
- Dashboard to visualize findings for business stakeholders

---

<details>
<summary>📈 <strong>Key Insights from EDA (click to expand)</strong></summary>

- **San Bernardino**, **Humboldt**, and **Santa Clara** recorded the **highest number** of strong earthquakes (`Mag ≥ 6.0`)
- **San Luis Obispo (7.93)** and **San Francisco (7.90)** experienced the **strongest recorded earthquakes**
- Strong earthquakes are **rare but geographically concentrated**, mostly affecting inland and coastal fault zones
- Seismic activity shows **notable spikes in early & mid 20th century**
- Using **official TIGER/Line boundaries** corrected spatial errors — e.g. recovering the historic 1906 San Francisco event
- Counties with frequent or extreme events may warrant **premium adjustments** or **enhanced coverage**
- Visualizations (choropleths, timelines, folium maps) offer valuable insights for **underwriting and strategic planning**

</details>

## 🌐 Interactive Maps (Hosted via GitHub Pages)

Preview key maps directly from your browser:

- [Strong Earthquakes by County (Folium)](https://annapiter.github.io/earthquake-insurance-analysis/strong_quakes_map.html)
- [Maximum Magnitude by County](https://annapiter.github.io/earthquake-insurance-analysis/max_magnitude_map.html)
- [Average Magnitude by County](https://annapiter.github.io/earthquake-insurance-analysis/avg_magnitude_map.html)

These interactive maps allow you to explore county-level earthquake risk with hoverable tooltips and zooming features.


---

## ✍️ Author

**Anna Piterskaya**  
Aspiring Data Scientist | Based in California  
🎯 Career Goal: Data Science role in the Insurance industry — especially at **AAA Insurance**  
📫 GitHub: [annapiter](https://github.com/annapiter)

---

## 🚀 Next Steps

> Integration of **demographic and insurance data** is planned to enhance risk modeling and build interactive **dashboards** for business users.
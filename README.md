# 🚗 Market Size Analysis on Electric Vehicles Industries

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Scikit--learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)](https://scikit-learn.org/)
[![Status](https://img.shields.io/badge/Status-Completed-1D9E75?style=for-the-badge)]()

An end-to-end Python market research project analyzing **177,861 electric vehicle registrations** from Washington State's DOL dataset — covering data cleaning, descriptive statistics, time-series growth trends, geographic hotspot detection, manufacturer/model popularity, EV technology evolution, and forecasting (Linear Regression + ARIMA).

---

## 📖 Project Overview

> *8-phase analytical pipeline, from raw registration data to a market-size forecast*

| Phase | Focus Area |
|---|---|
| **Phase 1** | Data Cleaning and Preparation |
| **Phase 2** | Descriptive Analysis (summary statistics, distributions) |
| **Phase 3** | Time-Series Analysis (growth trend, YoY %, cumulative market size) |
| **Phase 4** | Geographical Distribution Analysis (county/city breakdown, KMeans clustering, heatmap) |
| **Phase 5** | Make and Model Popularity |
| **Phase 6** | EV Types and Technology Analysis (BEV vs. PHEV, range progression) |
| **Phase 7** | Forecasting (Linear Regression + ARIMA) |
| **Phase 8** | Correlation and Trend Analysis |

---

## 📁 Project Structure

```
ev-market-size-analysis/
│
├── 📂 data/
│   └── Electric_Vehicle_Population_Data.csv     # Raw source data (177,866 rows) Currently I can't upload a file
│
├── 📂 notebooks/
│   └── ev_market_size_analysis.py               # Full analysis script, phase by phase
│
├── 📂 outputs/
│   ├── ev_data_cleaned.csv                       # Cleaned dataset (post Phase 1)
│   ├── ev_data_wa_only.csv                       # WA-only subset (post Phase 4)
│   ├── ev_heatmap_washington.html                # Interactive Folium heatmap
│   └── charts/                                   # All exported visualizations
│
├── 📂 report/
│   └── EV_Market_Size_Analysis_Report.docx       # Full project documentation
│
└── README.md
```

---

## 📌 Problem Statement

The electric vehicle market is expanding rapidly, but stakeholders — manufacturers, infrastructure planners, and policymakers — often lack a single, data-driven view of:

- How fast EV adoption is actually growing, year over year
- Where adoption is concentrated geographically
- Which manufacturers and models dominate the market, and how their strategies differ (BEV vs. PHEV)
- How EV technology (electric range) has evolved over time
- What future registration volumes are likely to look like

This project answers all of the above using a single reproducible Python pipeline, built entirely from public vehicle registration data.

---

## 🗂️ Dataset Overview

| Property | Detail |
|---|---|
| **Source** | Washington State Dept. of Licensing — Electric Vehicle Population Data |
| **Rows** | 177,866 (raw) → 177,861 (cleaned) |
| **Columns** | 17 (raw) → 20 (after feature engineering) |
| **Model Year Range** | 1997 – 2024 |
| **Geographic Scope** | Washington State (99.8% of records); WA-only subset used from Phase 4 onward |
| **Vehicle Types** | Battery Electric Vehicle (BEV), Plug-in Hybrid Electric Vehicle (PHEV) |

### Key Fields

`VIN (1-10)` · `County` · `City` · `State` · `Postal Code` · `Model Year` · `Make` · `Model` · `Electric Vehicle Type` · `CAFV Eligibility` · `Electric Range` · `Base MSRP` · `Legislative District` · `Vehicle Location` · `Electric Utility` · `2020 Census Tract`

---

## ⚙️ Tech Stack

| Tool | Purpose |
|---|---|
| **Python** | Core language for the entire pipeline |
| **Pandas / NumPy** | Data cleaning, transformation, aggregation |
| **Matplotlib / Seaborn** | Static visualizations (histograms, box plots, bar charts, heatmaps) |
| **Folium** | Interactive geospatial heatmap of EV registrations |
| **Scikit-learn** | KMeans clustering (geographic hotspots), Linear Regression forecasting |
| **Statsmodels** | ARIMA time-series forecasting |

---

## 🧹 Data Cleaning Highlights

Key decisions made during Phase 1, each documented with reasoning rather than applied blindly:

- Dropped **5 rows** with fully missing County/City/Postal Code/Utility/Census Tract data
- Filled **389 missing** `Legislative District` values as `"Unknown"` rather than dropping rows
- Flagged **91,950 rows (~51.7%)** where `Electric Range = 0` as `"Unknown"` via a new `Range Reported` column, since zero almost certainly means unrecorded rather than a true 0-mile range
- Identified **`Base MSRP` as ~98% zero/unreported** — excluded from statistical conclusions rather than imputed, to avoid fabricating price data
- Parsed the raw `Vehicle Location` string into clean `Latitude` / `Longitude` columns for geospatial analysis

---

## 📊 Key Insights

| # | Insight |
|---|---|
| 1 | **EV registrations grew ~74× between 2011 and 2023** (775 → 57,587), with growth accelerating sharply post-2021 |
| 2 | **King County (Seattle metro) accounts for 52%+ of all WA EV registrations** — confirmed independently via county counts, city counts, and KMeans clustering (Seattle cluster = ~67% of mapped vehicles) |
| 3 | **Tesla holds a 44.78% market share** — more than the next four makes (Nissan, Chevrolet, Ford, BMW) combined |
| 4 | **Model Y + Model 3 alone represent ~37% of all registered EVs** in Washington State |
| 5 | **Manufacturer strategies split sharply**: Tesla, Nissan, and Volkswagen are 100% BEV, while Jeep is 100% PHEV and Toyota is 94.6% PHEV |
| 6 | **Electric Range is multimodal** (peaks near 25, 80, and 215 miles) — explained by blending PHEV and two distinct eras of BEV technology |
| 7 | **BEV range reporting collapsed after model year 2020** (99.4% → 3.7% → 0% reported by 2022), a data-quality artifact rather than a real technology plateau |
| 8 | **Electric Range and Base MSRP show a moderate positive correlation (r = 0.52)** after excluding a Porsche 918 Spyder outlier, based on the ~1.9% of records with usable price data |
| 9 | **Linear Regression underestimates future growth** — its 2026 forecast falls below the already-observed 2023 actual, motivating the use of ARIMA |
| 10 | **ARIMA(1,1,1) projects 72,745–100,787 registrations for 2024**, better capturing market acceleration, though with wide uncertainty due to the limited 13-year training window |

---

## 🚀 How to Use

1. **Clone the repository**

```bash
git clone https://github.com/<your-username>/ev-market-size-analysis.git
cd ev-market-size-analysis
```

2. **Install dependencies**

```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels folium
```

3. **Add the dataset**

  - Place `Electric_Vehicle_Population_Data.csv` inside the `data/` folder
  - (Sourced from Washington State's open EV Population dataset)

4. **Run the analysis**

```bash
python notebooks/ev_market_size_analysis.py
```

5. **Explore the outputs**

  - Open `outputs/ev_heatmap_washington.html` in a browser for the interactive geographic heatmap
  - Review exported charts in `outputs/charts/`
  - Read the full write-up in `report/EV_Market_Size_Analysis_Report.docx`

---

## 📋 Project Objectives Coverage

| Objective | Status |
|---|---|
| Historical Growth Trend Assessment | ✅ Complete |
| Future Growth Forecasting (Linear Regression + ARIMA) | ✅ Complete |
| Geographical Distribution Analysis (county/city/clustering) | ✅ Complete |
| Make and Model Popularity | ✅ Complete |
| EV Types and Technology Analysis | ✅ Complete |
| Market Size Estimation | ✅ Complete |
| Full Documentation Report | ✅ Complete |

---

## 👩‍💻 Author

**Vaibhavi Hambire**
 
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/vaibhavi-hambire)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:hambirevaibhavi21@gmail.com)

---

## 📄 License

This project is open source under the [MIT License](LICENSE).

---

⭐ **If you found this project useful, consider giving it a star!**

# SpaceY

# SpaceY: Predictive Stock & Launch Analysis

A machine learning project that analyzes historical SpaceX launch data to predict the success of Stage 1 landings. Developed for SpaceY—a hypothetical competitor looking to bid strategically in the commercial space market.

## Overview

The goal of this project is to help **SpaceY** predict whether **Stage 1 of a rocket will successfully land after launch**, enabling the company to make informed, cost-saving decisions (~$100 million savings per successful reuse).

The project combines:
- Real-time SpaceX API data
- Web scraping from Wikipedia
- SQL-based structured querying
- Machine learning classification models
- Interactive data dashboards

---

## Tools & Technologies

- **Languages:** Python, SQL  
- **Data Acquisition:** SpaceX API, BeautifulSoup  
- **EDA & Visualization:** Pandas, NumPy, Matplotlib, Seaborn, Folium  
- **ML Models:** Logistic Regression, SVM, Decision Tree, KNN (via Scikit-learn)  
- **Dashboards:** Plotly Dash  
- **Database:** IBM DB2 with SQLAlchemy

---

## Problem Statement

> Predict whether a rocket's first-stage booster will land successfully after launch using historical SpaceX data.

---


## Methodology

1. **Data Collection**
   - Used the SpaceX REST API to collect JSON flight data.
   - Scraped additional booster info from Wikipedia using BeautifulSoup.
   - Stored in DB2 SQL using SQLAlchemy.

2. **Exploratory Data Analysis (EDA)**
   - Analyzed trends in success rate across years, payload mass, orbit type, and launch site.
   - Geospatial analysis using **Folium** to map launch/landing sites and proximity to coast, cities, and transportation hubs.

3. **Feature Engineering**
   - Payload mass, orbit type, booster version, launch site, customer, etc.
   - Encoded categorical variables and normalized payload mass.

4. **Model Training**
   - Applied 4 classifiers with 10-fold **GridSearchCV**:
     - Logistic Regression
     - Support Vector Machine (SVM)
     - Decision Tree
     - K-Nearest Neighbors
   - Each model achieved ~**83.33% accuracy** on test set (sample size = 18).

5. **Evaluation**
   - Evaluated with **Confusion Matrix**.
   - Found slight tendency to overpredict successful landings.

6. **Dashboard Development**
   - Created a **Plotly Dash** dashboard for real-time exploration of:
     - Launch sites
     - Payload vs. success
     - Booster versions
     - Time-series success trends

---

## Key Insights

- Success rate has increased steadily since 2013.
- KSC LC-39A has the **highest landing success rate**.
- **Payload mass** and **booster version** heavily influence landing outcome.
- SpaceX performs better in **lower orbits (LEO, VLEO, SSO)**.
- Most **landing failures** occurred in early years or at high payloads.

---

## Example Queries

- Total payload mass sent by NASA:
```sql
SELECT SUM(payload_mass_kg) FROM launches WHERE customer='NASA';

First successful ground pad landing date:
SELECT MIN(date) FROM landings WHERE outcome='Success (Ground Pad)';

Booster versions with max payloads:
SELECT booster_version, MAX(payload_mass_kg) FROM launches GROUP BY booster_version;


| Model               | Accuracy |
| ------------------- | -------- |
| Logistic Regression | 83.33%   |
| SVM                 | 83.33%   |
| Decision Tree       | 83.33%   |
| KNN                 | 83.33%   |





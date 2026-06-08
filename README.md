# NYC-Taxi-Fare-Analysis-Automatidata
An Interactive data analytics and business solution built for the NYC Taxi &amp; Limousine Commission Using Excel &amp; Tableau

# NYC Taxi & Limousine Commission: Operational Intelligence & Fare Analytics
**Data Analytics Portfolio Project | Workplace Scenario: Automatidata**

---

## 📋 Project Overview & Business Scenario
In this workplace scenario, the New York City Taxi and Limousine Commission (TLC) partnered with the data consulting firm **Automatidata** to develop a predictive solution for riders. The ultimate goal of the multi-stage project is to build a regression model that enables TLC riders to estimate taxi fares in advance of their rides.

As a data professional on this team, my first milestone was to inspect, organize, clean, and prepare the large-scale historical trip logs for exploratory data analysis (EDA) and future machine learning modeling.

---

## 🗃️ About the Dataset
The analysis utilizes historical trip data gathered by the NYC Taxi & Limousine Commission (`2017_Yellow_Taxi_Trip_Data.csv`). The original dataset contains **22,699 records** and **18 columns**, capturing explicit details of individual taxi trips:
* **Timestamps:** Meter engagement pickup and drop-off datetimes.
* **Trip Characteristics:** Total passenger counts, elapsed trip distances (miles), and specific TLC Taxi Zone location IDs (`PULocationID`/`DOLocationID`).
* **Financial Breakdowns:** Base fare amounts, toll expenses, credit card tips, surcharges, and grand total amounts charged to passengers.

---

## 🛠️ Data Cleaning & Quality Control
Before conducting analysis, the raw dataset was systematically audited to remove structural anomalies and errors that would distort predictive pricing models:
* **Initial Volume:** 22,699 rows.
* **Passenger Filtering:** Isolated and removed 33 rows registering 0 passengers.
* **Distance Validation:** Removed 148 rows registering 0.00 trip distances.
* **Fare Correction:** Removed 14 anomalous rows displaying negative or $0.00 baseline fare amounts (including an isolated 40-minute cash ride with a total transaction value of $0.00).
* **Daylight Savings Anomaly:** Handled a timestamp irregularity on November 5, 2017, where a trip departure occurred at 1:23 AM and drop-off occurred at 1:06 AM, producing a negative elapsed duration due to the regional clock setback.
* **Final Pristine Dataset:** **22,504 records** successfully retained for analysis.

---

## 📈 Feature Engineering (Data Transformation)
To unlock deeper insights for TLC operations, several high-value columns were engineered from the raw data:
1. `trip_duration_mins`: Computed as `([@tpep_dropoff_datetime] - [@tpep_pickup_datetime]) * 1440` to evaluate trip speed and efficiency.
2. `pickup_hour`: Extracted via `=HOUR()` to identify high-congestion timeframes.
3. `day_of_week`: Extracted via `=TEXT([..., "dddd")` to monitor weekly cycle patterns.
4. `month_name`: Extracted via `=TEXT([..., "mmmm")` to look for broader seasonal variations.
5. `tip_percentage`: Created to isolate customer tipping choices on digital payments.

---

## 📊 Key Insights & Business Discoveries

### 1. Temporal Demand (The "When")
* **Daily Peaks:** Fleet traffic demonstrates severe volume concentration during weekday evening commute windows, peaking between **5:00 PM and 7:00 PM** (over 1,440+ rides per hour). **Friday** represents the single most active day of the week.
* **Revenue Spikes:** While evening hours command the highest volume, early morning hours (**5:00 AM**) yield the highest average trip cost—signaling longer, high-value commutes (e.g., airport transfers).

### 2. Operational Metrics
* **Short-Hop Dominance:** The highest distribution of trip distances occurs heavily between **1 and 2 miles (32.8%)**, followed closely by trips under 1 mile (26.9%). Nearly 60% of NYC taxi usage is for short-distance urban travel.
* **Fixed-Pricing Structures:** Analysis verified that **RatecodeID 2 (JFK Airport)** enforces a flat-rate base fare of exactly **$52.00**, heavily overriding standard distance/duration pricing variables.

### 3. Tipping Dynamics & Data Limitations
* **Payment Preference:** Credit cards are the dominant payment choice, accounting for **67.4%** of transactions, while cash accounts for **32.0%**.
* **The "Cash Blindspot":** Credit card tips average a stable **$2.73 per ride**. However, cash transactions show a baseline tip value of **$0.00** because cash tips are not logged by the physical taximeter. 
* *Strategic recommendation for the model:* Future tipping prediction algorithms must be trained exclusively on credit card transactions to prevent massive downward bias.

---

## 🖥️ The Interactive Dashboards

### Excel Implementation
Built a fully interactive business dashboard utilizing Pivot Tables, synchronized multi-slicers, and dynamic, text-nested KPI boxes using the "Bridge Cell" method (`INDEX/MATCH` lookup strings). This enables non-technical stakeholders to filter metrics by Vendor or Weekday instantly.

### Tableau Implementation
Advanced the exploratory analysis by publishing a cloud-based dashboard on Tableau Public. Key additions include a dual-axis line graph mapping **Demand vs. Revenue**, a high-density scatter plot isolating tipping clouds, and geographic distribution profiles.

👉 **[Click Here to View the Interactive Tableau Dashboard] https://public.tableau.com/app/profile/bhavana.bajjuri/viz/Automatidataanalysis/Dashboard1**

---

## 🚀 Next Steps: Predictive Modeling Prep
To transition this project into a Python machine learning phase, the insights from this EDA recommend:
1. Encoding categorical inputs (`day_of_week`, `pickup_hour`) into dummy variables.
2. Applying spatial override logic to automatically handle flat-rate airport codes (`RatecodeID 2`).
3. Dropping cash transaction rows if predicting tip behavior, or utilizing distance and duration as the primary continuous drivers for predicting the base `fare_amount`.

---
*Project completed as part of the Google Advanced Data Analytics Professional Certificate.*

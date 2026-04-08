# ⚡ Smart Energy Consumption & Billing Analytics Dashboard  
### Real-World Smart Utility, Smart Meter & Energy Analytics Use Case

This project is an end-to-end **Data Analytics & Business Intelligence case study** built using **Python, MySQL, and Power BI**.

The project focuses on **smart meter data analysis, slab-based electricity billing, anomaly detection, and city-wise business insights** for utility decision-making.

---

## 📌 Problem Statement

Utility and energy infrastructure companies require data-driven systems to:

- monitor electricity consumption
- estimate billing revenue
- detect abnormal meter behavior
- compare city-wise usage trends
- support smart utility operations

This project simulates a **real-world smart meter analytics and energy management use case** relevant to utility and power infrastructure companies.

---

## 🎯 Business Objective

- Analyze smart meter data from multiple cities
- Implement slab-based billing logic
- Detect abnormal consumption patterns
- Compare yearly and city-wise trends
- Generate actionable business insights

---

## 🛠️ Tech Stack

- Python
- Pandas
- MySQL
- SQLAlchemy
- Power BI
- GitHub

---

## 📂 Dataset Details

The project uses smart meter aggregated datasets from two cities in Uttar Pradesh:

- Bareilly
- Mathura

### Columns
- `meter`
- `date`
- `units_consumed`

---

## 🔄 Project Workflow

### 1️⃣ Data Collection
Collected two smart meter datasets from different cities.

---

### 2️⃣ Data Preprocessing in Python

```python
Mathura['city'] = "Mathura"
Bareilly["city"] = "Bareilly"

df = pd.concat([Mathura, Bareilly])
df.rename(columns={"t_kWh": "units_consumed"}, inplace=True)
```

Performed:
- data cleaning
- schema standardization
- city tagging
- dataset merging

---

### 3️⃣ Billing Logic

Implemented slab-based electricity billing:

- 0–100 → ₹3/unit
- 101–200 → ₹5/unit
- 200+ → ₹8/unit

```python
def calculate_bill(units):
    if units <= 100:
        return units * 3
    elif units <= 200:
        return (100 * 3) + (units - 100) * 5
    else:
        return (100 * 3) + (100 * 5) + (units - 200) * 8
```

---

### 4️⃣ Monthly Aggregation

```python
monthly_df = df1.groupby(
    ["meter", "city", "month"]
)["units_consumed"].sum().reset_index()
```

Converted daily readings into monthly consumption trends.

---

### 5️⃣ Anomaly Detection

Flagged abnormal consumption if monthly usage exceeded **1.5× meter average**

```python
def detect_anomaly(row):
    avg = meter_avg[row["meter"]]
    if row["units_consumed"] > avg * 1.5:
        return "High"
    return "Normal"
```

---

### 6️⃣ SQL Storage

Stored processed data into MySQL

```python
monthly_df.to_sql(
    "monthly_energy_data",
    con=engine,
    if_exists="replace",
    index=False
)
```

---

### 7️⃣ Power BI Dashboard

Connected MySQL with Power BI and created interactive dashboards for:

- KPI cards
- anomaly alerts
- city comparison
- revenue trends
- yearly analysis

---

## 📊 Key Insights

### ⚡ Overall KPIs
- **Total Units:** 365.31K
- **Revenue:** ₹1.96M
- **High Anomalies:** 427

---

### 🏙️ City-wise Comparison

| City | Units | Revenue | Anomalies |
|---|---:|---:|---:|
| Bareilly | 230.79K | ₹1.25M | 218 |
| Mathura | 134.52K | ₹0.71M | 210 |

---

### 📈 Key Business Findings

- Bareilly recorded the highest total consumption
- Mathura showed higher anomaly density
- 2020 was the peak consumption year
- repeated high anomaly meters identified
- supports theft/fault detection use cases

---

## 💼 Business Value

This project can support **smart utility, smart metering, and energy infrastructure companies** in:

- billing intelligence
- meter monitoring
- anomaly alerts
- revenue assurance
- smart city utility analytics

---

## 📷 Dashboard Screenshot

Below is the interactive Power BI dashboard built for smart meter consumption, billing analytics, and anomaly detection.

![Smart Energy Dashboard](./Screenshot%202026-04-05%20174334.png)

---

## 🚀 Future Enhancements

- ML-based anomaly detection
- consumption forecasting
- real-time smart meter monitoring
- alert notification system

---

## 👨‍💻 Author

**Sai Abhilash**  
Aspiring Data Analyst | Business Intelligence | Data Science

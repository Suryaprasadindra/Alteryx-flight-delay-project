# ✈️ Alteryx Flight Delay Analytics Project (2018–2024)

This project analyzes historical U.S. domestic flight data (2018–2024) to detect SLA breaches, categorize delays, and identify underperforming airlines. Built entirely in **Alteryx Designer**, it demonstrates real-world ETL logic, KPI generation, and dashboard prep — ready for business operations or executive reporting.

---

## 📁 Project Structure

Alteryx-flight-delay-project/ ├── raw/ # Original CSV dataset ├── alteryx/ # All .yxmd workflows and .yxdb output │ ├── WF_01_ingest_clean.yxmd │ ├── WF_02_kpi_summary.yxmd │ ├── WF_03_dashboard.yxmd │ └── clean_flights_2018_2024.yxdb ├── screenshots/ # Optional (no visuals included) └── README.md #


---


---

## 🎯 Objective

To build a clean, modular Alteryx workflow that:

- Filters and enriches U.S. flight delay data  
- Flags **SLA breaches** (delays >15 minutes)  
- Categorizes delays by severity  
- Summarizes **airline-level KPIs**  
- Prepares insights for Tableau or Power BI dashboards  

---

## 🔧 Tools & Technologies

- **Alteryx Designer** (AMP Engine)
- Tools used:
  - Input Data, Select, Filter, Formula  
  - Summarize, Sort, Sample, Browse  
  - Interactive Chart Tool (for in-tool previews)

---

## 🔄 Workflow Breakdown

### 🧩 1. Ingestion & Cleaning  
📄 **Workflow**: `WF_01_ingest_clean.yxmd`

- Ingested raw CSV dataset (2018–2024)
- Removed:
  - Cancelled flights (`Cancelled = 1`)
  - Diverted flights (`Diverted = 1`)
- Selected ~18 relevant fields (date, delays, carrier, etc.)
- Created:
  - `SLA_Breach`: `1` if `ArrDel15 = 1`
  - `DelayCategory`:
    - Severe: `ArrDelayMinutes > 60`
    - Moderate: `16–60`
    - Minor: `1–15`
    - On Time: `0`
- Output:  
  `clean_flights_2018_2024.yxdb`

---

### 📊 2. KPI Summary by Airline  
📄 **Workflow**: `WF_02_kpi_summary.yxmd`

- Loaded cleaned `.yxdb` file
- Grouped by `Operating_Airline`
- Aggregated:
  - `Total_Flights` = `Count([Flight Number])`
  - `SLA_Breaches` = `Sum([SLA_Breach])`
- Calculated:
  - `SLA_Breach_Rate = SLA_Breaches / Total_Flights * 100`
- Sorted airlines by highest breach rates

---

### 📈 3. Dashboard Layer Prep  
📄 **Workflow**: `WF_03_dashboard.yxmd`

- Re-used `.yxdb` as input source
- Extracted:
  - Top 10 worst-performing airlines by breach rate
  - Total KPI metrics
  - Delay category breakdowns
- Created components for:
  - Bar charts (Airline vs SLA Rate)
  - Delay severity summaries
  - Region-wise summaries *(optional)*
- Final data exported for Tableau/Power BI

---

## 📊 Key Metrics Tracked

| Metric              | Description                                      |
|---------------------|--------------------------------------------------|
| `SLA_Breach`        | 1 if flight delayed >15 mins, else 0             |
| `SLA_Breach_Rate`   | SLA breach % by airline                          |
| `DelayCategory`     | On Time, Minor, Moderate, or Severe              |
| `Total_Flights`     | Count of valid (non-cancelled, non-diverted) flights |

---

## 📤 Outputs

- ✅ Cleaned `.yxdb` file: `clean_flights_2018_2024.yxdb`
- 📊 KPI summary tables by airline
- 📈 Top 10 airline breach summary
- 📦 Dashboard-ready metrics for Tableau

---

## 🙋‍♂️ Author

**Indra Prasad Chevva**  
📍 Master’s in Management Science & Supply Chain  
📍 Wichita State University  
📧 ixchevva@shockers.wichita.edu  
🔗 [LinkedIn](https://www.linkedin.com/in/YOUR-LINK) *(update this!)*

---

## 🧠 Future Enhancements

- 📅 Delay trend analysis by weekday or month  
- 🗺️ Geo heatmaps (e.g., SLA breach by Origin State)  
- 📈 Publish final dashboard via Tableau Public  
- 🔍 SLA root cause attribution by delay type (Carrier, NAS, Weather)

---

## 📜 License

This project is open-source and intended for educational and portfolio use.  
Released under the **MIT License**.

---


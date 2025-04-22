# ✈️ Alteryx Flight Delay Analytics Project (2018–2024)

This project analyzes historical U.S. domestic flight data (2018–2024) to detect SLA breaches, categorize delays, and identify underperforming airlines. Built entirely in **Alteryx Designer**, it demonstrates real-world ETL logic, KPI generation, and dashboard prep — ready for business operations or executive reporting.

---

## 📁 Project Structure

Alteryx-flight-delay-project/ ├── raw/ # Original CSV dataset ├── alteryx/ # All .yxmd workflows and .yxdb output │ ├── WF_01_ingest_clean.yxmd │ ├── WF_02_kpi_summary.yxmd │ ├── WF_03_dashboard.yxmd │ └── clean_flights_2018_2024.yxdb ├── screenshots/ # Optional (no visuals included) └── README.md #


---

## 🎯 Objective

To build a clean, modular workflow in Alteryx that:
- Filters and enriches flight delay data
- Flags SLA breaches (delays >15 mins)
- Classifies delay severity into categories
- Summarizes KPIs at the airline level
- Prepares insights for future visualization

---

## 🔧 Tools & Technologies

- **Alteryx Designer** (AMP Engine)
- Tools used:
  - Input Data, Select, Filter, Formula
  - Summarize, Sort, Sample, Browse
  - Interactive Chart Tool (for local preview)

---

## 🔄 Workflow Breakdown

### 🧩 1. Ingestion & Cleaning (`WF_01_ingest_clean.yxmd`)
- Ingested raw CSV data (2018–2024)
- Removed:
  - Cancelled flights (`Cancelled = 1`)
  - Diverted flights (`Diverted = 1`)
- Selected ~15–20 relevant fields only
- Engineered new fields:
  - `SLA_Breach`: 1 if `ArrDel15 = 1`
  - `DelayCategory`:
    - `Severe` if `ArrDelayMinutes > 60`
    - `Moderate` if `>15`
    - `Minor` if `>0`
    - `On Time` if `= 0`
- Saved cleaned data to `.yxdb`:
  - `clean_flights_2018_2024.yxdb`

---

### 📊 2. KPI Summary by Airline (`WF_02_kpi_summary.yxmd`)
- Loaded cleaned `.yxdb` file
- Grouped by `Operating_Airline`
- Aggregated:
  - `Total_Flights`: Count of flights
  - `SLA_Breaches`: Sum of `SLA_Breach`
- Calculated:
  - `SLA_Breach_Rate` = `(SLA_Breaches / Total_Flights) * 100`
- Sorted airlines by highest breach rate for review

---

### 📈 3. Dashboard Layer Prep (`WF_03_dashboard.yxmd`)
- Re-used cleaned `.yxdb` as source
- Extracted:
  - Total KPI metrics
  - Top 10 worst-performing airlines
- Built bar chart using:
  - `Operating_Airline` (X-axis)
  - `SLA_Breach_Rate` (Y-axis)
- Additional prep for:
  - Delay category summaries
  - Region-wise summaries (optional)
- Cleaned and labeled all components for future export

---

## 📊 Key Metrics Tracked

| Metric             | Description                               |
|--------------------|-------------------------------------------|
| SLA_Breach         | 1 if delay >15 mins, else 0               |
| SLA_Breach_Rate    | % of flights delayed >15 mins per airline |
| DelayCategory      | Severity label (On Time, Minor, etc.)     |
| Total_Flights      | Total valid flights analyzed              |

---

## 📤 Outputs

- Final cleaned `.yxdb` file
- Aggregated breach data
- Top 10 airline summaries
- Dashboard-ready summaries for future reporting

---

## 🙋‍♂️ Author

**Indra Prasad Chevva**  
📍 Wichita State University  
📧 ixchevva@shockers.wichita.edu  
💼 [LinkedIn](https://www.linkedin.com/in/indra-prasad-chevva/)

---

## 🧠 Future Enhancements (Optional)

- Delay trends by month or weekday
- Geographic heatmaps (OriginState vs SLA rate)
- Export-ready Tableau or Power BI dashboards
- SLA root cause breakdown (Carrier, NAS, Weather)

---

## 📜 License

Open-source for educational and portfolio use.  
You may use this project under the MIT License.


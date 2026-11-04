# E-Commerce Delivery & Operations Analytics

![Project Banner](images/dashboard_preview.png)

## 1. Executive Summary & Overview
This operational analytics project models logistics fulfillment performance, delivery Turnaround Time (TAT), carrier Service Level Agreement (SLA) compliance, and warehouse dispatch bottlenecks across **3,000+ shipment records**. By identifying root causes for delivery exceptions, this repository provides supply chain teams with actionable insight to reduce shipping delays and optimize logistics vendor allocations.

---

## 2. Business Problem Statement
Delivery delays lead to increased order cancellations, customer support tickets, and reduced customer lifetime value. Logistics teams struggle with:
- **Lack of Carrier Accountability:** Difficulty tracking on-time delivery percentages (OTD%) across multiple logistics partners.
- **Fulfillment Bottlenecks:** Identifying whether delivery delays originate during warehouse dispatch or carrier transit.
- **High Exception Costs:** Managing operational losses caused by failed delivery attempts and customer return processing.

---

## 3. Project Objectives & Business Use Cases
- **Fulfillment Metrics:** Calculate Dispatch TAT, Transit Days, and Total End-to-End Delivery Time.
- **Carrier SLA Tracking:** Measure carrier On-Time Delivery (OTD%) and contract SLA compliance rates.
- **Root Cause Analysis:** Categorize delay factors (e.g., weather disruptions, address errors, routing bottlenecks).
- **Operational Dashboarding:** Deliver interactive specifications for supply chain monitoring.

---

## 4. Tech Stack & Tools
| Tier | Technologies / Libraries |
| :--- | :--- |
| **Language** | Python 3.10+ |
| **Data Analytics** | Pandas, NumPy |
| **SQL Engine** | SQLite3, Window Aggregations, Conditional Filtering |
| **Data Visualization** | Matplotlib, Seaborn |
| **Dashboarding** | Power BI / Tableau JSON Specification |

---

## 5. End-to-End Logistics Pipeline Workflow
```
+-------------------+     +--------------------+     +-------------------+
| Orders &          |     | Fulfillment        |     | Exception &       |
| Shipments Data    | --> | Milestone Analysis | --> | Carrier SLA       |
| Ingestion         |     | (Dispatch vs Transit)|   | Evaluation        |
+-------------------+     +--------------------+     +---------+---------+
                                                               |
                                                               v
+-------------------+     +--------------------+     +---------+---------+
| Supply Chain      |     | Root Cause Delay   |     | SLA Benchmark     |
| Recommendations   | <-- | Categorization     | <-- | Scoring Matrix    |
| & Dashboards      |     | Analysis           |     | Generation        |
+-------------------+     +--------------------+     +-------------------+
```

---

## 6. Directory Structure
```
project3_delivery_operations/
├── config/
│   └── settings.ini
├── data/
│   ├── raw/
│   │   └── shipments.csv
│   └── logistics.db
├── dashboards/
│   └── ops_dashboard_spec.json
├── images/
│   ├── dashboard_preview.png
│   ├── carrier_sla_breakdown.png
│   └── delivery_tat_distribution.png
├── outputs/
│   ├── carrier_performance_summary.csv
│   └── delivery_operations_overview.png
├── src/
│   └── pipeline.py
├── sql/
│   └── operational_queries.sql
├── tests/
│   └── test_pipeline.py
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

---

## 7. Step-by-Step Setup & Execution
```bash
# 1. Clone repository
git clone https://github.com/your-username/project3_delivery_operations.git
cd project3_delivery_operations

# 2. Setup Virtual Environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install requirements
pip install -r requirements.txt

# 4. Execute Operational Analytics Pipeline
python src/pipeline.py

# 5. Execute Test Suite
python -m unittest tests/test_pipeline.py
```

---

## 8. Analytical Operational Formulas

$$\text{Dispatch TAT} = \text{Dispatch Timestamp} - \text{Order Timestamp}$$

$$\text{Transit Time} = \text{Actual Delivery Timestamp} - \text{Dispatch Timestamp}$$

$$\text{On-Time Delivery Rate (OTD\%)} = \left( \frac{\text{Shipments Delivered On or Before SLA Date}}{\text{Total Shipments Delivered}} \right) \times 100$$

---

## 9. Analytical SQL Queries

### Carrier SLA Benchmark Query
```sql
SELECT 
    carrier,
    COUNT(shipment_id) AS total_shipments,
    SUM(CASE WHEN is_late = 1 THEN 1 ELSE 0 END) AS late_shipments,
    ROUND(100.0 * SUM(CASE WHEN is_late = 0 THEN 1 ELSE 0 END) / COUNT(shipment_id), 2) AS on_time_delivery_pct,
    ROUND(AVG(actual_tat_days), 2) AS avg_tat_days,
    ROUND(AVG(promised_tat_days), 2) AS target_tat_days
FROM shipments
WHERE status = 'Delivered'
GROUP BY carrier
ORDER BY on_time_delivery_pct DESC;
```

---

## 10. Operational Output Dashboards & Charts

### Operational Overview Preview
![Logistics Overview Preview](images/dashboard_preview.png)

---

## 11. Actual Output Results Summary

### Carrier Performance Comparison
| Carrier Partner | Total Volume | On-Time Deliveries | Late Deliveries | OTD Rate (%) | Avg TAT (Days) | SLA Status |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **ExpressLog** | 1,050 | 987 | 63 | **94.00%** | 2.1 | Compliant |
| **SwiftShip** | 1,120 | 996 | 124 | **88.93%** | 2.8 | At Risk |
| **National Freight**| 830 | 680 | 150 | **81.93%** | 4.2 | Non-Compliant |

---

## 12. Strategic Supply Chain Recommendations
1. **Volume Reallocation:** Reallocate 15% of shipping volume from *National Freight* to *ExpressLog* in regional hubs to boost on-time rates.
2. **Warehouse Dispatch SLA:** Institute a strict 24-hour cutoff rule for warehouse order processing to prevent transit delays.
3. **Automated Notification Triggers:** Implement real-time SMS alerts for customer addresses marked as high-risk delivery exceptions.

---

## 13. Verification & Testing Results
- **Pipeline Processing Test:** `PASSED` (100% of shipment records correctly ingested without syntax errors).
- **Date Arithmetic Test:** `PASSED` (Zero negative TAT values generated during processing).

---

## 14. GitHub Upload Instructions
```bash
git init
git add .
git commit -m "Initial commit - E-Commerce Delivery & Operations Analytics"
git branch -M main
git remote add origin https://github.com/your-username/project3_delivery_operations.git
git push -u origin main
```

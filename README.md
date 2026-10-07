#  AeroGlow E-Commerce Supply Chain Optimization & OTIF Control Tower

![Power BI] https://app.powerbi.com/groups/me/reports/a2efca03-a4bb-4542-a2da-a38459cc7932?ctid=222fdcbc-d8fd-45ec-a507-5999b5c5a72f&pbi_source=linkShare 
![Microsoft Excel] 
![Supply Chain Analytics](https://img.shields.io/badge/Supply_Chain-Analytics-0078D4?style=for-the-badge)


##  Executive Summary

### 1. Operational Diagnostic & OTIF Bottleneck Analysis
An end-to-end audit of AeroGlow’s 2026 Q1–Q2 fulfillment pipeline revealed severe supply chain degradation, driven by an overall On-Time In-Full (OTIF) rate of under 25%. While total logistics spend reached $81.1K across 30 shipments, supply network performance exhibited sharp regional polarization. German supplier EuroTech Manufacturing (S003) demonstrated world-class operational precision with 100% quantity fulfillment and an average lead time of 11.2 days. Conversely, Asian supply routes suffered from systemic lead-time slippage, with Indian supplier Apex Electronics (S001) averaging 2-to-3-day delays across 80% of its order volume, severely compromising inventory replenishment predictability.

### 2. Vendor Vulnerability & Financial Risk Exposure
Shenzhen Global Components (S002 / China) was identified as AeroGlow's primary operational bottleneck and single largest margin risk. S002 accounted for 100% of the network’s total inventory shortfalls—failing to deliver 614 ordered units across key shipments (e.g., `SHM1013`, `SHM1023`) for the fast-moving Quantum Wireless Mouse (`P102`). Compounding these stockouts, S002 exhibited an unpredictable lead time averaging 24.8 days (with spikes exceeding 30 days) while consuming over 55% of the total logistics budget due to elevated freight costs ($5.80+/unit). Reorder Point (ROP) modeling confirms that current safety stock buffers (200 units) are insufficient to absorb S002's volatility, placing `P102` at immediate risk of recurring stockouts.

### 3. Strategic Recommendations & Mitigation Roadmap
To restore supply chain resiliency and protect gross margins, AeroGlow must execute a three-pronged mitigation strategy:
1. **SLA Renegotiation & Safety Stock Adjustment:** Renegotiate S002’s Service Level Agreement (SLA) to enforce financial penalty clauses for short-shipments, while dynamically recalibrating `P102` Safety Stock targets from 200 to 350 units.
2. **Calendarized Logistics Cadence:** Transition Apex Electronics (S001) to a structured fixed-calendar shipping cadence to eliminate minor 2-to-3-day lead time variance.
3. **Nearshoring & Dual-Sourcing:** Initiate dual-sourcing procurement for high-turnover peripheral components within European or nearshore markets to reduce reliance on vulnerable transpacific lanes, thereby slashing average lead times by 35% and elevating aggregate network OTIF performance to above 85%.


##  Business Problem & Core Objectives

AeroGlow, a fast-growing consumer electronics brand, experienced significant fulfillment challenges during Q1–Q2 2026:
* **Unmonitored Stockouts & Shortages:** Unexplained unit shortages in high-demand SKU lines.
* **Logistics Cost Creep:** Freight costs scaling without a proportional increase in lead-time reliability.
* **Supplier SLA Variance:** Lack of visibility into which vendors drove customer delivery delays.

### Project Goals
* Establish an **OTIF (On-Time In-Full) Control Tower** to evaluate supplier performance.
* Conduct **Reorder Point (ROP)** and **Safety Stock Analysis** to mitigate stockout risks.
* Build an **Interactive Power BI Dashboard** to enable real-time operational monitoring for leadership.


##  Data Architecture & Analytical Workflow
[ Raw Shipment Logs ] ➔ [ Excel Data Modeling & ROP Calc ] ➔ [ Power BI DAX & Visual Control Tower ]

### Phase 1: Excel Modeling & Data Transformation
* **Metric Engineering:** Calculated actual vs. expected lead times, delay days, and shortage quantities.
* **Fulfillment Metrics:** Standardized boolean checks for `On-Time?` (delay $\le$ 0) and `In-Full?` (shortage = 0).
* **Inventory Modeling:** Derived Reorder Points (ROP) using:
  $$\text{ROP} = (\text{Average Daily Demand} \times \text{Lead Time}) + \text{Safety Stock}$$

### Phase 2: Power BI Dashboard & DAX Measures
* **Data Ingestion:** Loaded structured tables into Power BI Desktop and built relationships between `Data_Shipments`, `Suppliers`, and `Products`.
* **DAX Formulas Implemented:**
  * **Total Shipping Spend:** `SUM(Data_Shipments[shipping_cost])`
  * **Total Shortage Units:** `SUM(Data_Shipments[shortage_units])`
  * **Average Lead Time:** `AVERAGE(Data_Shipments[actual_lead_time_days])`
  * **OTIF %:**
    ```dax
    OTIF % = 
    DIVIDE(
        CALCULATE(
            COUNTROWS(Data_Shipments),
            Data_Shipments[delay_days] <= 0 && Data_Shipments[shortage_units] = 0
        ),
        COUNTROWS(Data_Shipments),
        0
    )
    ```

##  Key Findings & Metrics Overview

| Supplier Name | Country | Avg Lead Time | Quantity Fulfillment | Major Issues Identified |
| :--- | :--- | :--- | :--- | :--- |
| **EuroTech Manufacturing (S003)** | Germany | 11.2 Days | **100%** | Outstanding benchmark performance across all metrics. |
| **Apex Electronics Ltd (S001)** | India | 18.5 Days | **100%** | Consistent 2–3 day delivery slippage impacting lead-time predictability. |
| **Shenzhen Global Components (S002)** | China | 24.8 Days | **82.3%** | 614 short units (100% of network total); high freight cost ($5.80/unit). |


##  Repository Structure
├── AeroGlow_SupplyChain_Model.xlsx   # Complete Excel Data Model & Pivot Calculations
├── AeroGlow_Control_Tower.pbix       # Power BI Interactive Dashboard File
├── Dashboard_Overview.pdf            # PDF Export of the Power BI Visual Layout
└── README.md                         # Project Case Study & Executive Summary

##  How to Explore This Project
1. **Download the Repository:** Clone or download the ZIP to inspect the raw data and formulas.
2. **View the Dashboard:** Open `AeroGlow_Control_Tower.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/) to interact with filters and slicers.
3. **Review the Model:** Open `AeroGlow_SupplyChain_Model.xlsx` to review the ROP calculations and baseline data transformation.

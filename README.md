
# Business-Optimization-Dashboard

### Tool Used : Power BI Desktop | Excel | Python | SQL | AWS

## Dashboard Link : https://drive.google.com/file/d/127Tw9Z2YiiFwtKFnHnBfhszjUaW574Jo/view?usp=sharing

---

## Problem Statement

This dashboard helps businesses understand the gap between product demand and actual availability and the financial consequences of that gap. It gives operations, supply chain, and management teams a clear picture of where supply shortages are occurring, how much profit is being generated versus lost, and what the average daily demand and availability trends look like across products and order dates.

Since **Total Loss (97K) is significantly higher than Total Profit (22K)**, the business is currently operating at a net loss position. The average daily loss of **88.84** combined with a total supply shortage of **579 units** indicates a critical misalignment between what customers are demanding and what the business is able to supply. Until this gap is addressed through better inventory planning, supplier management, or demand forecasting profitability will continue to suffer.

This dashboard is designed to surface those gaps clearly so that decision-makers can prioritize the right interventions and move toward a balanced, profitable operation.

---

## Steps Followed

- **Step 1 :** Load data into Power BI Desktop. The dataset is a CSV file containing order-level records with fields including Product ID, Product Name, Order Date, Demand, Availability, Unit Price, and Loss/Profit values sourced from e-commerce retail and manufacturing/inventory data.

- **Step 2 :** Open the Power Query Editor. Under the **View** tab, in the **Data Preview** section, enable **"Column Distribution"**, **"Column Quality"**, and **"Column Profile"** options to thoroughly inspect the dataset before modeling.

- **Step 3 :** Change column profiling from the default 1,000 rows to **"Column profiling based on entire dataset"** to ensure data quality checks reflect the full record count.

- **Step 4 :** Inspect all columns for errors and null values. The **Order Date** column was formatted and converted into a proper date field (`Order_Date_DD_MM_YYYY`) to enable time-based analysis. Null values in the Demand and Availability columns were excluded from average calculations.

- **Step 5 :** In the **Report View**, a **dark black background theme** was applied across both pages to align with the Insigh BI brand identity. Purple-toned card visuals with glowing blue metric text were used to create a modern, high-contrast aesthetic.

- **Step 6 :** The **Insigh BI logo and brand header** were added to the top of both report pages using image and text box elements, with the subtitle *"Data Visualization for Business Optimization"* placed beneath it consistently across pages.

- **Step 7 :** A dedicated **Measure Table** (`MEASURE TABLE 1`) was created to house all calculated DAX measures separately from the raw data table, keeping the data model clean and organized. The following measures were created:

  ```DAX
  AVERAGE AVAILABILITY PER DAY = AVERAGE('DEMAND/AVAILABILITY DATA'[Availability])

  AVERAGE DEMAND PER DAY = AVERAGE('DEMAND/AVAILABILITY DATA'[Demand])

  TOTAL AVAILABILITY = SUM('DEMAND/AVAILABILITY DATA'[Availability])

  TOTAL DEMAND = SUM('DEMAND/AVAILABILITY DATA'[Demand])

  TOTAL LOSS = SUMX(FILTER('DEMAND/AVAILABILITY DATA', 'DEMAND/AVAILABILITY DATA'[LOSS/PROFIT] < 0), 'DEMAND/AVAILABILITY DATA'[LOSS/PROFIT])

  TOTAL PROFIT = SUMX(FILTER('DEMAND/AVAILABILITY DATA', 'DEMAND/AVAILABILITY DATA'[LOSS/PROFIT] > 0), 'DEMAND/AVAILABILITY DATA'[LOSS/PROFIT])

  AVERAGE LOSS PER DAY = AVERAGE('DEMAND/AVAILABILITY DATA'[LOSS/PROFIT])

  TOTAL NUMBER OF DAYS = DISTINCTCOUNT('DEMAND/AVAILABILITY DATA'[Order_Date_DD_MM_YYYY])

  TOTAL SUPPLY SHORTAGE = [TOTAL DEMAND] - [TOTAL AVAILABILITY]
  ```

- **Step 8 :** The report was structured into **two pages**, each focused on a specific set of KPIs:

  - **Page 1 : Supply & Demand KPIs**
  - **Page 2 : Profit & Loss KPIs**

- **Step 9 :** On **Page 1**, three large **KPI Card visuals** were added to display the core supply and demand metrics:

  (a) **Average Demand per Day** - 3.40
  ![image alt](https://github.com/user-attachments/assets/1c300f26-974a-4be5-ae2d-d26848d9f366)

  (b) **Average Availability per Day** - 2.87
  ![image alt](https://github.com/user-attachments/assets/cd613f26-1fd9-4435-b356-80c7cd040a3f)

  (c) **Total Supply Shortage** - 579
  ![image alt](https://github.com/user-attachments/assets/e77d78b2-ede8-4ba1-8f7a-fbd06aea922c)

  Cards were styled with a deep purple rounded rectangle background and bold italic blue metric text to make values instantly readable.

- **Step 10 :** On **Page 2**, three large **KPI Card visuals** were added to display the financial performance metrics:

  (a) **Total Profit** - 22K
  ![image alt](https://github.com/user-attachments/assets/645ae2eb-2fea-46d5-b75a-7b5449d2047d)

  (b) **Total Loss** - 97K
  ![image alt](https://github.com/user-attachments/assets/526a04c5-9122-40db-9d18-9fd34821337e)

  (c) **Average Daily Loss** - 88.84
  ![image alt](https://github.com/user-attachments/assets/04e54c10-736f-408d-b90b-e44c4010c3c4)

  The same card styling from Page 1 was maintained for visual consistency across the report.

- **Step 11 :** The **LOSS/PROFIT** column was created as a calculated column in the data model to derive the net financial outcome per order record:

  ```DAX
  LOSS/PROFIT = 'DEMAND/AVAILABILITY DATA'[Availability] * 'DEMAND/AVAILABILITY DATA'[Unit_Price]
              - 'DEMAND/AVAILABILITY DATA'[Demand] * 'DEMAND/AVAILABILITY DATA'[Unit_Price]
  ```

  Positive values indicate profit (supply met or exceeded demand); negative values indicate loss (demand exceeded supply).

- **Step 12 :** The **Order Date** field was formatted using Power Query to ensure consistent `DD/MM/YYYY` formatting across all records, enabling accurate time-series filtering and aggregation in future iterations of the dashboard.

- **Step 13 :** Decorative **3D abstract graphic elements** (purple/blue holographic shapes) were placed in the top-left and top-right corners of both pages using the image insert option, reinforcing the Insigh BI visual brand identity.

- **Step 14 :** The report was then published to **Power BI Service** for sharing and stakeholder access.

---

## Snapshot of Dashboard (Power BI Desktop)

### Page 1 — Supply & Demand KPIs
![image alt](https://github.com/user-attachments/assets/ab37e109-4d79-4f90-b877-054be77be146)

### Page 2 — Profit & Loss KPIs
![image alt](https://github.com/user-attachments/assets/60fe5b98-0a81-4dc1-a40b-5d0a97ae1304)

---

## Insights

A two-page report was created on Power BI Desktop and published to Power BI Service.

The following inferences can be drawn from the dashboard:

---

### [1] Supply vs. Demand Gap

- **Average Demand per Day** - 3.40 units
- **Average Availability per Day** - 2.87 units
- **Total Supply Shortage** - **579 units**

  → On average, the business falls short by **0.53 units per day** in meeting customer demand. While this may seem small on a daily basis, it accumulates to a shortage of 579 units in total - a significant operational gap that directly drives financial losses.

---

### [2] Financial Performance

- **Total Profit** - **22K**
- **Total Loss** - **97K**
- **Average Daily Loss** - **88.84**

  → The business is generating **4.4x more loss than profit**. For every unit of profit earned, approximately 4.4 units of loss are being incurred. The average daily loss of 88.84 confirms this is a persistent, ongoing issue rather than an isolated event.

---

### [3] Root Cause Indication

- The supply shortage of **579 units** is the primary driver of the **97K total loss**.
- Products where demand consistently exceeds availability are generating negative LOSS/PROFIT values, pulling overall financial performance down.
- The **Unit Price** variable means that high-value products with supply shortages contribute disproportionately to total losses.

  → Prioritizing restocking for high unit-price, high-demand products would have the greatest impact on closing the loss gap.

---

### [4] Data Model Structure

The data model consists of two key components:

**DEMAND/AVAILABILITY DATA table** (raw data):
- Availability, Demand, LOSS/PROFIT, Order Date, Product ID, Product Name, Unit Price

**MEASURE TABLE 1** (all DAX measures):
- 9 calculated measures covering averages, totals, shortage, profit, and loss

  → Separating measures from raw data into a dedicated measure table keeps the model clean, scalable, and easier to maintain as the dashboard grows.

---

## Tools & Technologies Used

| Tool | Purpose |
|---|---|
| Power BI Desktop | Dashboard development, data modelling & DAX |
| Power Query Editor | Data cleaning, date formatting & transformation |
| DAX | All KPI measures & calculated columns |
| Power BI Service | Publishing & stakeholder sharing |
| Insigh BI | Dashboard branding & visual theme |
| CSV Dataset | Source data — E-commerce retail & inventory orders |


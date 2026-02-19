# 📊 Electro Hub: End-to-End Sales & Product Analytics

![Power BI](https://img.shields.io/badge/Power%20BI-Desktop-F2C811?style=flat&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/Language-DAX-blue?style=flat)
![ETL](https://img.shields.io/badge/ETL-Power%20Query-green?style=flat)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## 📝 Table of Contents
- [Project Overview](#-project-overview)
- [Data Architecture & Modeling](#-data-architecture--modeling)
- [Key Performance Indicators (KPIs)](#-key-performance-indicators-kpis)
- [Business Questions & STAR Analysis](#-business-questions--star-analysis)
- [Key Insights](#-key-insights)
- [Learnings & Challenges](#-learnings--challenges)
- [Next Steps / Recommendations](#-next-steps--recommendations)
- [Screenshots / Dashboard Previews](#-screenshots--dashboard-previews)

---

## 🚀 Project Overview
**Electro Hub** is a multi-category retail store selling Electronics, Fashion, and Home Appliances.  
Prior to this project, reporting was spreadsheet-based, lacked interactivity, and offered no clear insight into seasonal trends, product profitability, or geographic performance.  

This project leveraged **Microsoft Power BI** to build a **dynamic, interactive 5-page dashboard**, enabling:  
- Multi-period sales comparison  
- Top/Bottom product identification  
- Sales/profit correlation analysis  
- City-wise and product-level insights  

> The result: stakeholders can now make **data-driven inventory, pricing, and promotional decisions** in minutes instead of hours.

---
## 🖼 Screenshots / Dashboard Previews
<img width="1659" height="859" alt="Screenshot 2026-02-19 201557" src="https://github.com/user-attachments/assets/43eb4c63-9a5d-48be-bc45-54b7067e4456" />

<img width="1529" height="844" alt="Screenshot 2026-02-19 202629" src="https://github.com/user-attachments/assets/fb5421f0-af5a-4166-b8e7-c9919b1e3edc" />
<img width="1321" height="728" alt="Screenshot 2026-02-19 202834" src="https://github.com/user-attachments/assets/20fdc8ca-2860-4ee1-afd6-08434de59644" />


---

## 🔄 Project Flow Summary

The end-to-end workflow for **Electro Hub** analytics project is as follows:

1. **Extract & Transform**  
   - Cleaned nulls and missing values  
   - Standardized column names and formats  
   - Calculated derived metrics such as **Net Sales** and **Profit**  

2. **Load**  
   - Created a **Star Schema** with a central Fact Table (`Fact_Sales`) and Dimension Tables (`Dim_Products`, `Dim_Customers`, `Dim_Promotion`)  
   - Optimized for fast aggregation and reporting  

3. **Modeling**  
   - Established **active relationships** for standard reporting  
   - Added **inactive relationships** for dynamic period comparisons using `USERELATIONSHIP` in DAX  
   - Ensured dimensional slicers interact correctly with fact tables  

4. **Visualization**  
   - Built **interactive dashboards** with slicers, filters, and drill-through capabilities  
   - Included multi-period comparison, Top/Bottom products, sales trends, and geographic analysis  

> This structured workflow ensures **clean, accurate, and actionable insights** for stakeholders, while maintaining a scalable and flexible data model.

---

## 🏗 Data Architecture & Modeling

### **Data Source**
- **Format:** Excel / CSV  
- **Volume:** ~3,500 transactional records  
- **Tables:** `Fact_Sales`, `Dim_Products`, `Dim_Customers`, `Dim_Promotion`  

### **Star Schema**
- **Fact Table:** `Fact_Sales`  
  - Contains transaction-level data including **Net Sales** and **Orders**  
- **Dimension Tables:**  
  - `Dim_Products` – Product ID, Name, Category  
  - `Dim_Customers` – Customer ID, Name, City  
  - `Dim_Promotion` – Promotion ID, Discount %  
- **Date Tables:**  
  - Two separate date tables created using `CALENDARAUTO()` in DAX  
  - Used to enable **dynamic period comparisons** in reports  

> This star schema ensures **fast aggregations, reduced redundancy, and easy integration with Power BI visuals**, enabling stakeholders to explore sales, profit, and promotional insights efficiently.

---

## 🔑 Key Performance Indicators (KPIs)

| KPI | Formula / Logic | Purpose |
| --- | --- | --- |
| **Total Sales** | `Unit Sold * Price Per Unit` | Measures overall revenue generated from all transactions |
| **Net Sales** | `Total Sales - Discount Value` | Revenue after accounting for promotions or discounts |
| **Total Profit** | `10% of Net Sales` | Estimated profit margin for the business |
| **Total Orders** | `DISTINCTCOUNT(Order ID)` | Tracks total number of unique orders processed |
| **Average Discount** | `AVERAGE(Discount %)` | Evaluates effectiveness of promotions and discounts |

> These KPIs provide a **quantitative snapshot of business performance**, allowing stakeholders to monitor revenue, profitability, discount impact, and transaction volume in a single dashboard.

---

## 💼 Business Questions & STAR Analysis

### 1️⃣ Top / Bottom 5 Products (Sales / Profit / Quantity)
- **Situation:** No clarity on top revenue-generating or underperforming products  
- **Task:** Identify top and bottom products by Sales, Profit, Quantity  
- **Action:** Created **Stacked Bar Charts** with Top N filter applied to Product Name  
- **Result:** Highlighted **iPhone 14** & **MacBook Air** as top performers, low-margin items like toothpaste as bottom  

### 2️⃣ Sales Trends Over Time
- **Situation:** Seasonality not understood, impacting inventory planning  
- **Task:** Visualize daily, monthly, quarterly, and yearly trends  
- **Action:** **Line Chart** with date hierarchy and drill-down enabled  
- **Result:** Peak sales observed during **Diwali** & **New Year**, guiding inventory stocking  

### 3️⃣ Sales vs Profit Correlation
- **Situation:** Relationship between sales volume and profit margin unclear  
- **Task:** Analyze correlation between Sales & Profit  
- **Action:** **Scatter Plot** with Profit on X-axis, Net Sales on Y-axis  
- **Result:** Strong positive correlation confirmed **consistent margin stability**  

### 4️⃣ Dynamic Period Comparison
- **Situation:** Users required A/B comparison of any two periods  
- **Task:** Compare Sales, Profit, and Quantity dynamically  
- **Action:** Implemented **dual slicers** + inactive relationship + `USERELATIONSHIP` DAX  
- **Result:** Enabled **precise period comparison**, aiding campaign evaluation  

### 5️⃣ Average Discount by Category
- **Situation:** Marketing lacked insights on discount effectiveness  
- **Task:** Compute average discount per promotion category  
- **Action:** **Bar Chart**: Promotion Name vs Average Discount %  
- **Result:** "Weekend Flash Sales" & "Clearance Sales" had highest discounts (20–50%)  

### 6️⃣ Total Number of Orders
- **Situation:** Volume tracking was missing  
- **Task:** Count total orders  
- **Action:** **Card Visual** using `DISTINCTCOUNT(Order ID)`  
- **Result:** **3,510 unique orders** processed  

### 7️⃣ Detailed Transaction View
- **Situation:** Auditing required for all order-level details  
- **Task:** Display Sales, Profit, Discount, Customer, Product, Promotion, Date  
- **Action:** **Table Visual** with multiple slicers for dimensions  
- **Result:** Fully interactive, drillable table enabling granular analysis  

### 8️⃣ Sales by Geography
- **Situation:** Logistics & marketing required city-level insights  
- **Task:** Show sales distribution across cities  
- **Action:** **Map Visual** with bubble size based on Net Sales  
- **Result:** **Delhi, Mumbai, and Bangalore** identified as top revenue hubs

---

## 📊 Key Insights
- **High-margin products drive most revenue** → prioritize inventory for electronics  
- **Seasonality matters** → festive periods increase revenue by ~35%  
- **Discounts effective only on targeted promotions** → optimize marketing spend  
- **Metro cities dominate revenue** → implement city-specific campaigns  

---

## 🧠 Learnings & Challenges
- **Inactive Relationships & USERELATIONSHIP:** Learned how to manage multiple date relationships for dynamic reporting  
- **Null & Missing Data Handling:** Power Query transformations are critical for accurate calculations  
- **Dimension Cross-Filtering:** Using dummy measures ensures slicers filter each other correctly  
- **Dashboard UX:** Proper slicer placement and “Edit Interactions” improve usability and clarity  

---

## 🏁 Next Steps / Recommendations
- Implement **forecasting models** to predict next quarter sales  
- Integrate **real-time POS data** for daily monitoring  
- Add **profit margin visualization** per product category  
- Include **customer segmentation analysis** for targeted marketing  

---
---

## ✍️ Author

**[Vignesh_Raveendran]**  
*Data Engineer / Data Analyst*  

[LinkedIn](https://www.linkedin.com/in/yourprofile) | [Portfolio](https://yourportfolio.com)






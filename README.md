<!-- =========================== -->
<!--  Gurdeep Singh | Sales Insights Dashboard  -->
<!-- =========================== -->

# 🛍️ Sales Insights Dashboard  
**Business Intelligence | SQL | Power BI | Tableau**

![Dashboard Preview](assets/sales-dashboard.png)

## 📊 Project Overview
The **Sales Insights Dashboard** project transforms raw retail sales data into a dynamic and interactive business intelligence dashboard.  
This solution provides **real-time visibility** into revenue trends, customer behavior, and regional performance — enabling leadership to make data-driven decisions that improve profitability.

---

## 🧠 Objective
- Build a **data pipeline** using **SQL** for extraction, cleaning, and transformation.  
- Integrate refined data into **Power BI / Tableau** for advanced visualization.  
- Deliver KPIs that support **strategic decisions in sales, marketing, and inventory**.  

---

## 🧩 SQL Data Framework

**Data Sources:**  
🗄️ `fact_sales` – transactional sales records  
🏬 `dim_customer` – customer profiles & demographics  
📦 `dim_product` – product hierarchy  
🌎 `dim_market` – regional sales & location data  
💰 `dim_currency` – exchange rate tables  

**SQL Workflow:**
1️⃣ **Extract** data from multiple relational tables (MySQL).  
2️⃣ **Cleanse & Validate** data using joins, filters, and window functions.  
3️⃣ **Transform** data for KPIs:  
   - Revenue by product, region, and month  
   - Profit margin % and YOY growth  
   - Top 10 products by sales and contribution  
4️⃣ **Load & Visualize** – Connect to Power BI/Tableau to create interactive dashboards.  
5️⃣ **Automate** refresh using Python scripts and SQL views.

---

## 📈 Key Insights
- 🚀 Identified **15% increase in sales** in Q4 driven by high-performing SKUs.  
- 🧾 Improved **forecasting accuracy** by 12% through regional segmentation.  
- 📦 Highlighted **inventory bottlenecks** in top 3 markets, leading to improved allocation.  
- 💡 Delivered **self-service dashboards** for leadership and regional managers.

---

## 🛠️ Tools & Technologies
| Category | Tools |
|-----------|--------|
| Database | MySQL, SQL Server |
| Data Transformation | SQL (CTEs, Window Functions, Joins) |
| Visualization | Power BI, Tableau |
| Scripting | Python (ETL Automation) |
| Reporting | Excel (Pivot Models, Financial Templates) |

---

## 🧮 Example SQL Queries

```sql
-- Total Revenue by Region
SELECT 
    dim_market.market_name AS Region,
    ROUND(SUM(fact_sales.sales_amount), 2) AS Total_Revenue
FROM fact_sales
JOIN dim_market ON fact_sales.market_id = dim_market.market_id
GROUP BY dim_market.market_name
ORDER BY Total_Revenue DESC;

-- Monthly Sales Growth
SELECT 
    DATE_FORMAT(fact_sales.order_date, '%Y-%m') AS Month,
    ROUND(SUM(fact_sales.sales_amount), 2) AS Monthly_Revenue,
    LAG(ROUND(SUM(fact_sales.sales_amount), 2)) OVER (ORDER BY DATE_FORMAT(fact_sales.order_date, '%Y-%m')) AS Prev_Month_Revenue,
    ROUND(
        (SUM(fact_sales.sales_amount) - LAG(SUM(fact_sales.sales_amount)) OVER (ORDER BY DATE_FORMAT(fact_sales.order_date, '%Y-%m')))
        / LAG(SUM(fact_sales.sales_amount)) OVER (ORDER BY DATE_FORMAT(fact_sales.order_date, '%Y-%m')) * 100, 2
    ) AS Growth_Percentage
FROM fact_sales
GROUP BY Month;

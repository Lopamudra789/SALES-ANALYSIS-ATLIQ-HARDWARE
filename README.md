# **Project: Sales Insights & Data Analysis - AtliQ Hardware**

## **Table of Contents**

- [Problem Statement](#problem-statement)
- [Data Discovery](#data-discovery)
- [Data Analysis using MySQL](#data-analysis-using-mysql)
- [Data Cleaning and ETL (Extract, Transform, Load)](#data-cleaning-and-etl-extract-transform-load)
- [Data Modeling](#data-modeling)
- [Data Analysis (DAX)](#data-analysis-dax)
- [Dashboard & Reporting](#dashboard--reporting)
- [Tools & Technologies Used](#tools--technologies-used)
- [References](#references)

---

## **Problem Statement**

AtliQ Hardware, a leading supplier of computer hardware and peripherals across India, faces challenges in tracking sales due to rapid market dynamics. The Sales Director struggles with:

- Lack of real-time sales insights
- Dependency on verbal updates from regional managers
- Difficulty in making data-driven decisions due to unstructured reporting
- Overall declining sales performance

To address these issues, the company seeks an **automated sales dashboard** using **Microsoft Power BI**, enabling real-time data visualization and supporting **data-driven decision-making**.

---

## **Data Discovery**

### **AIMS Grid (Project Planning Framework)**

1. **Purpose:** Gain actionable sales insights and automate reporting to reduce manual effort.
2. **Stakeholders:**
   - Sales Director
   - Marketing Team
   - Customer Service Team
   - Data & Analytics Team
   - IT Department
3. **End Result:** An automated dashboard offering real-time sales insights.
4. **Success Criteria:**
   - Reduction of manual data gathering by 20%
   - Clear insights into sales performance across regions
   - Data-driven decisions leading to a 10% reduction in operational costs

### **Project Execution Flowchart**

![Flowchart](https://user-images.githubusercontent.com/118357991/231545034-7f6cc437-5683-44f1-92df-a671540ccae9.jpg)

---

## **Data Analysis using MySQL**

After data discovery, **MySQL** was used to analyze the database. The `db_dump.sql` file was imported into **MySQL Workbench** for further analysis.

### **Initial Data Quality Checks:**
- Identified incorrect values in the `market` table
- Found negative sales amounts in the `transactions` table
- Detected USD transactions that needed conversion to INR

### **Key SQL Queries:**

#### 1. Fetch all customer records:
```sql
SELECT * FROM sales.customers;
```
#### 2. Count total customers:
```sql
SELECT COUNT(*) FROM sales.customers;
```
#### 3. Fetch transactions for Chennai market:
```sql
SELECT * FROM sales.transactions WHERE market_code='Mark001';
```
#### 4. Total revenue in 2020:
```sql
SELECT SUM(sales.transactions.sales_amount)
FROM sales.transactions
INNER JOIN sales.date
ON sales.transactions.order_date = sales.date.date
WHERE sales.date.year=2020;
```

---

## **Data Cleaning and ETL (Extract, Transform, Load)**

1. **Connecting MySQL Database to Power BI**
2. **Loading Data into Power BI Desktop**
3. **Transforming Data using Power Query:**
   - Removed null and incorrect values
   - Filtered out transactions with negative or zero amounts
   - Converted USD transactions into INR using a conversion factor of **1 USD = 75 INR**

**DAX Formula for Currency Conversion:**
```DAX
Normalized_Sales_Amount = IF([Currency] = "USD", [Sales_Amount] * 75, [Sales_Amount])
```

---

## **Data Modeling**

After data transformation, the dataset was structured into a **star schema** to optimize reporting performance. The key tables include:

- **Fact Table:** `sales_transactions`
- **Dimension Tables:** `sales_customers`, `sales_products`, `sales_markets`, `sales_date`

### **Data Model Representation:**

![Data Model](https://user-images.githubusercontent.com/118357991/234016242-369bd02e-1ddf-4047-9be4-324c83bd8761.png)

---

## **Data Analysis (DAX)**

Key measures used in Power BI:

- **Profit Margin %**
```DAX
Profit_Margin_Percentage = DIVIDE([Total_Profit], [Revenue], 0)
```
- **Revenue**
```DAX
Total_Revenue = SUM(sales_transactions[Sales_Amount])
```
- **Sales Quantity**
```DAX
Total_Sales_Quantity = SUM(sales_transactions[Sales_Qty])
```
- **Revenue Growth (Year-over-Year)**
```DAX
Revenue_LY = CALCULATE([Total_Revenue], SAMEPERIODLASTYEAR(sales_date[Date]))
```

---

## **Dashboard & Reporting**

The final dashboard provides real-time insights into sales performance, profit margins, and market trends.

### **Key Insights Dashboard**
![Dashboard](https://raw.githubusercontent.com/Lopamudra789/SALES-ANALYSIS-ATLIQ-HARDWARE/main/sc_1.png)

### **Profit Analysis Dashboard**
![Profit Analysis](https://raw.githubusercontent.com/Lopamudra789/SALES-ANALYSIS-ATLIQ-HARDWARE/main/sc_2.png)

---

## **Tools & Technologies Used**

- **Database:** MySQL
- **BI & Visualization:** Microsoft Power BI
- **ETL & Data Transformation:** Power Query
- **Analytics & Metrics Calculation:** DAX (Data Analysis Expressions)

---

## **References**

- [SQLBI - DAX Learning](https://www.sqlbi.com/learn/introducing-dax-video-course/0/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [Power BI Tutorials](https://codebasics.io/panel/webinars/purchases)

---


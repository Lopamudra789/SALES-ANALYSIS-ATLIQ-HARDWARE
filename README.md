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

Completed the Data discovery and then used mySQL for data analysis.

SQL database dump is in db_dump.sql file above. Download db_dump.sql file to your local computer

- Importing Data to MySQL workbench

![Screenshot (2)](https://user-images.githubusercontent.com/118357991/233262007-c36f58cd-df19-42b5-b9cb-4d72c0ef64a4.png)

![Screenshot (3)](https://user-images.githubusercontent.com/118357991/233262064-b1fb8f0f-8c16-402d-adac-07784b81a2fe.png)


The import of data is done from an already existing MySQL file. This file has to be loaded into MySQL workbench for further data analysis. 

- Analysis of data by looking into different tables and reflecting garbage values

   We can see that garbage value that the table market cantains certain values which are incorrect.
   
     `SELECT * FROM sales.market;`
     
   And then we can check that transacation table we can see that ceratin negative value in amount which is not possible. and we can see that certain transactions are      in USD. Hence, filtration of that is also needed by converting into INR.
     
     `SELECT * FROM sales.transactions;`
     
 - Analysis of different SQL statement on data base
     
   1.To find of all customers records 
     
     `SELECT * FROM sales.customers;`
      
   2.To find total number of customers 
     
     `SELECT count(*) From sales.customers;`

   3.To find transactions for Chennai market (market code for chennai is Mark001
     
      `SELECT * FROM sales.transactions where market_code='Mark001';`

   4.To find distrinct product codes that were sold in chennai
     
      `SELECT distinct product_code FROM sales.transactions where market_code='Mark001';`

   5.To find transactions for Chennai market (market code for chennai is Mark002
     
      `SELECT * FROM sales.transactions where market_code='Mark002';`

   6.To find distrinct product codes that were sold in mumbai
     
      `SELECT distinct product_code FROM sales.transactions where market_code='Mark002';`
      
   7.To find transactions where currency is US dollars
     
      `SELECT * from sales.transactions where currency="USD";` 
      
   8.To find transactions in 2020 join by date table
     
      `SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;`  

   8.To find transactions in 2019 join by date table
     
      `SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2019;`  

   9.To find total revenue in year 2020,
     
      `SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";` 
      
   10.To find total revenue in year 2019,
     
      `SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2019 and sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r";`       

   11.To find total revenue in year 2020, January Month,
     
      `SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");` 

   12.To find total revenue in year 2020, February Month,
     
      `SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="February" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");` 

   13.To find total revenue in year 2019, January Month,
     
      `SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="January" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");` 

   14.To find total revenue in year 2019, February Month,
     
      `SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.date.month_name="February" and (sales.transactions.currency="INR\r" or sales.transactions.currency="USD\r");` 

   15.To find total revenue in year 2020 in Chennai
     
      `SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark001";` 

   16.To find total revenue in year 2020 in Mumbai
     
      `SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and sales.transactions.market_code="Mark002";` 

Similarly, if we want different of any other particular city the market code of that city is used on the mysql workbench.
## **Data Cleaning and ETL (Extract, Transform, Load)**
In this process, we are work on data cleaning and ETL.

 Step 1: Connect the MySQL database with the PowerBI desktop.
 
 Step 2: Loading data into the Power BI deskstop.
 This step load all the tables and created in the data base. This load option will connect with the SQL and pull all the records into power BI environment.
         
 In that model view looking up for model which form the star schema.
         
 ![Screenshot (4)](https://user-images.githubusercontent.com/118357991/233265427-94285bbf-79e6-446f-bd72-dc7c220e0680.png)

 Setp 3: Transform data with the help of Power Query
 
 Perform filtration in market’s table: In the tables perform when we click on the transform data option, we are directed to Power query editor. Power query editor is where we perform out ETL.and then we can perform data transformation i.e. Data Cleaning, Data Wrangling, Data Munging. we need to filter the rows where the values are null and filtering the data and deselecting the blank option. 

 Perform filtration in Transaction’s table: In the table perform when we check the query in the MySQL to filter some negative values and also 0 values that appears in the table, the desired output is received.and we will perform the similar filtration in PowerBI. we have deselecting the values, don’t want in the table. The result after filtration. the zero values represent some garbage values which is not possible so we need to clean that data.

Convert USD into INR in the transaction’s table: the AtliQ Hardware only works in India so the USD values are not possible. we need to convert those USD values into INR by using some formulas. Add new column - Conditional column - normalized currency where sales amount will be in INR

In power query editore finding the total values having USD as currency.

     `=Table.AddColumn(#"Filtered Rows", "norm_sales_amount",each if [currency] = "USD" then [sales_amount]*75 else [sales_amount]`
 
 using this correct formula of the conversion,and converted the USD currency into INR.
 
 In MySQL Workbench find that there are duplicates of USD and INR
 
     `SELECT count(*) from sales.transactions where sales.transactions.currency="INR\r";` 
     150000 - can't removed as it is large amount

     `SELECT count(*) from sales.transactions where sales.transactions.currency="INR";` 
     279 - we can remove it as it is small record and can be considered as bad data

     `SELECT count(*) from sales.transactions where sales.transactions.currency="USD\r";` 
 
     `SELECT count(*) from sales.transactions where sales.transactions.currency="USD";`

     `SELECT * from sales.transactions where sales.transactions.currency='USD\r' or sales.transactions.currency='USD';`

we can see that it is duplicate and for analysis its better to delete anyone of them so lets delete USD and keep USD/r. finally we will keep data with INR/r and USD/r-

## **Data Modeling**

After data transformation, the dataset was structured into a **star schema** to optimize reporting performance. The key tables include:

- **Fact Table:** `sales_transactions`
- **Dimension Tables:** `sales_customers`, `sales_products`, `sales_markets`, `sales_date`

### **Data Model Representation:**

![Data Model](https://user-images.githubusercontent.com/118357991/234016242-369bd02e-1ddf-4047-9be4-324c83bd8761.png)

---

## **Data Analysis (DAX)**

Measures used in all visualization are:

Key Measures:
    
  - Profit Margin % = `DIVIDE([Total Profit Margin],[Revenue],0)` 
  - Profit Margin Contribution % = `DIVIDE([Total Profit Margin],CALCULATE([Total Profit Margin],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))`
  - Revenue = `SUM('sales transactions'[sales_amount])`
  - Revenue Contribution % = `DIVIDE([Revenue],CALCULATE([Revenue],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))`
  - Revenue LY = `CALCULATE([Revenue],SAMEPERIODLASTYEAR('sales date'[date]))`
  - sales quntity = `SUM('sales transactions'[sales_qty])`
  - Total Profit Margin = `SUM('Sales transactions'[Profit_Margin])`

Profit Target:
  
  - Profit Target1 = `GENERATESERIES(-0.05, 0.15, 0.01)`
  - Profit Target Value = `SELECTEDVALUE('Profit Target1'[Profit Target])`
  - Target Diff = `[Profit Margin %]-'Profit Target1'[Profit Target Value]`
  

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


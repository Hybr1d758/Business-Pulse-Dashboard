# Business-Pulse-Dashboard

User Guide

🗂️ Table of Contents
- Introduction
- Prerequisites
- Installation & Setup
- Development Steps
- Data Cleaning in Power Query
- Data Modeling
- Define Relationships in the Data Model
- DAX Measures
- Dashboard Design
- Development Lifecycle Practice
- Scalability and Governance
- Troubleshooting



## 1. Introduction 
The Business Pulse Dashboard is an integrated reporting solution designed to monitor and visualize key business performance indicators across sales, operations, finance, and planning. 
Built using Microsoft Power BI, it delivers insights, supports scenario comparisons (Actual, Budget, Forecast), and empowers users at all levels with interactive and role-based dashboards.

## 2. Prerequisites 
- Microsoft Power BI Desktop and Power BI Service installed 
- Microsoft Excel (sample data source)
- Power Query for data transformation
- Data Analysis Expressions (DAX) for calculations
- Basic knowledge of Power BI recommended but not required.


## 3. Installation & Setup
- Clone the Repository:git clone https://github.com/Hybr1d758/Business-Pulse-Dashboard.git
- Open the Dashboard:
- Navigate to the cloned folder.
- Open the .pbix file with Power BI Desktop.


## 4. Development Steps
### Step 1: Data Source Setup
- Update the data source paths to point to your local or server data
- Load the Excel file 'Superstore - Sales.xlsx'.
- Click Refresh on the Power BI toolbar to load your data.
- Use the 'Sales' sheet, which includes key fields such as Order Date, Customer, Region, Category, Sales, Profit, and Quantity.
<img width="1470" alt="Screenshot 2025-05-27 at 10 14 38" src="https://github.com/user-attachments/assets/7e7c2154-6e69-4688-b695-bab4f76c18fe" />
  

   
   
### Step 5: Data Cleaning in Power Query
- Unused columns (Row ID,Order ID, Country and Postcode) was removed.
- Remove Duplicate from the dataset and group by the customer ID to check if there are any duplicates left
<img width="1268" alt="Screenshot 2025-05-27 at 10 21 03" src="https://github.com/user-attachments/assets/6d0a783f-00a1-4334-8d94-7873f76e69f0" />
   
   
   
-  Sales, Profit and CoGS columns were changed from decimal number to fixed decimal number.
<img width="1273" alt="Screenshot 2025-05-27 at 10 33 45" src="https://github.com/user-attachments/assets/eb40713e-a017-408d-864d-04151bffa515" />

   

- CoGS to Cost of Goods Sold was renamed
<img width="1272" alt="Screenshot 2025-05-27 at 10 37 32" src="https://github.com/user-attachments/assets/b9e2e802-25c1-4c30-b1b1-c719fe7bf5f9" />
  


### Step 6: Data Modeling
- Build a star schema:
- NOTE: Duplicate the sales table in order to have one for your fact table and the others for the dimensions table.
<img width="1270" alt="Screenshot 2025-05-27 at 12 04 44" src="https://github.com/user-attachments/assets/e9eece9d-711f-421e-83a2-bf222c74790a" />
<br>



   - Fact Table:

| Column             | Description                         |
|--------------------|-------------------------------------|
| Order Date         | When the order was placed           |
| Ship Date          | When it was shipped                 |
| Sales              | Revenue from the order              |
| Profit             | Profit from the sale                |
| Discount           | Discount applied                    |
| Quantity           | Number of units sold                |
| Cost of Goods Sold | Estimated cost of the products sold |
| Order ID           | Transaction identifier              |
<img width="1268" alt="Screenshot 2025-05-27 at 11 56 11" src="https://github.com/user-attachments/assets/df7801ad-a377-43e5-8e84-a39efec8b8cf" />



   - Dimension Tables:
   - Product Dimension

| Column       | Description               |
| ------------ | ------------------------- |
| Product ID   | Unique product code       |
| Product Name | Name of the product       |
| Category     | High-level grouping       |
| Sub-Category | Sub-group within category |
<img width="1272" alt="Screenshot 2025-05-27 at 12 38 37" src="https://github.com/user-attachments/assets/30b5155c-172c-4871-bf9b-c4182e7fd325" />




   - Customer Dimension
     
| Column      | Description           |
| ----------- | --------------------- |
| Customer ID | Unique identifier     |
| City        | City of the customer  |
| State       | State of the customer |
| Region      | Region                |
<img width="1270" alt="Screenshot 2025-05-27 at 12 43 37" src="https://github.com/user-attachments/assets/33f81834-e0e2-4bb0-a703-2f4a3054fa35" />




   - Geography Dimension

| Column | Description       |
| ------ | ----------------- |
| State  | State or Province |
| Region | Business region   |
<img width="1271" alt="Screenshot 2025-05-27 at 12 49 24" src="https://github.com/user-attachments/assets/c23e7a55-34ae-4f2d-8f80-b10d0cbb10d2" />




   - Time Dimension
     
| Column                                    | Description           |
| ----------------------------------------- | --------------------- |
| Order Date                                | Actual date of sale   |
| Ship Date                                 | When the item shipped |
<img width="1271" alt="Screenshot 2025-05-27 at 12 48 14" src="https://github.com/user-attachments/assets/623a795b-4a2a-4fa1-8981-e9f3db237fae" />




### Step 7: Define Relationships in the Data Model
- Open the Model view in Power BI.
- Connect foreign keys in the Fact Table to the primary keys in the Dimension Tables.

Relationships set up:
- 'Fact_sales'[Customer ID] → 'Dim_product'[Customer ID]
- 'Fact_sales'[Product ID] → 'Dim_product'[Product ID]
- 'Fact_sales'[Order Date] → 'Dim_product'[Date]
- 'Fact_sales'[Region] → 'Dim_product'[Region]
<img width="1463" alt="Screenshot 2025-06-01 at 10 03 11" src="https://github.com/user-attachments/assets/a22d9685-df76-4057-b717-b3381b576e2b" />



### Step 8: DAX Measures
- Total Sales = SUM('Sales'[Sales])
- Total Profit = SUM('Sales'[Profit])
- Profit Margin = DIVIDE([Total Profit], [Total Sales])
- Total Quantity = SUM('Sales'[Quantity])
- Average Discount = AVERAGE('Sales'[Discount])
- Total Cost of Goods Sold = SUM('Sales'[CoGS])
- Gross Margin = [Total Sales] - [Total Cost of Goods Sold]
<img width="1470" alt="Screenshot 2025-06-01 at 12 48 53" src="https://github.com/user-attachments/assets/b2a5d45d-9e82-4307-8566-ed080896693e" />



### Step 9: Dashboard Design
- Create card visuals for KPIs: Total Sales, Profit, Quantity, Profit Margin.
- Use bar/column charts for Sales by Category, Profit by Region.
- Line chart for sales trends over time.
- Add slicers for Category, Segment, Region, Order Date.
<img width="768" alt="Screenshot 2025-06-05 at 11 19 26" src="https://github.com/user-attachments/assets/bcfb308a-4d53-463d-b71a-fffa79fa08d4" />



### Step 10: Development Lifecycle Practice
- Work in a 'Development' workspace.
- Save versioned files (e.g., BusinessPulse_v1_2025-05-25.pbix).
- Include comments in DAX measures for maintainability.
<img width="1467" alt="Screenshot 2025-06-05 at 11 20 23" src="https://github.com/user-attachments/assets/8d12f5c5-a85a-42dc-af0c-7b44c79cb15a" />

### Step 11: Scalability and Governance
- Optimize model (hide unused columns, avoid calculated columns).
- Prepare for Row-Level Security based on user roles or regions.
- Document model structure and maintain a version control log.
<img width="1470" alt="Screenshot 2025-06-05 at 11 40 17" src="https://github.com/user-attachments/assets/0e758c7f-a9b3-48df-b2f6-595429c0848a" />


## Step 12. Troubleshooting
| Issue                          | Solution                                       |
| ------------------------------ | ---------------------------------------------- |
| Dashboard visuals not updating | Check data source connections and refresh      |
| Role-based views not working   | Confirm RLS configuration and user permissions |
| Data errors or blank visuals   | Ensure correct file paths and data formats     |


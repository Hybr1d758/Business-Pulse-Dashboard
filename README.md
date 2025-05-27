# Business-Pulse-Dashboard


## 1. Project Overview
The Business Pulse Dashboard is an integrated reporting solution designed to monitor and visualize key business performance indicators across sales, operations, finance, and planning. 
Built using Microsoft Power BI, it delivers insights, supports scenario comparisons (Actual, Budget, Forecast), and empowers users at all levels with interactive and role-based dashboards.

## 2. Tools and Technologies
- Microsoft Power BI Desktop and Power BI Service
- Microsoft Excel (sample data source)
- Power Query for data transformation
- Data Analysis Expressions (DAX) for calculations


## 3. Development Steps
### Step 1: Data Source Setup
• Load the Excel file 'Superstore - Sales.xlsx'.
• Use the 'Sales' sheet, which includes key fields such as Order Date, Customer, Region, Category, Sales, Profit, and Quantity.
<img width="1470" alt="Screenshot 2025-05-27 at 10 14 38" src="https://github.com/user-attachments/assets/7e7c2154-6e69-4688-b695-bab4f76c18fe" />

### Step 2: Data Cleaning in Power Query
• Unused columns like Row ID was removed.
• Check data types and format appropriately.
• Rename columns for consistency (e.g., CoGS to Cost of Goods Sold).

### Step 3: Data Modeling
• Build a star schema:
   - Fact Table: Sales (contains Sales, Profit, Quantity, etc.)
   - Dimension Tables: Product, Customer, Region, Time
• Define relationships using unique keys such as Customer ID and Product ID.

### Step 4: DAX Measures
• Total Sales = SUM('Sales'[Sales])
• Total Profit = SUM('Sales'[Profit])
• Profit Margin = DIVIDE([Total Profit], [Total Sales])
• Total Quantity = SUM('Sales'[Quantity])
• Average Discount = AVERAGE('Sales'[Discount])
• Total Cost of Goods Sold = SUM('Sales'[CoGS])
• Gross Margin = [Total Sales] - [Total Cost of Goods Sold]

### Step 5: Dashboard Design
• Create card visuals for KPIs: Total Sales, Profit, Quantity, Profit Margin.
• Use bar/column charts for Sales by Category, Profit by Region.
• Line chart for sales trends over time.
• Add slicers for Category, Segment, Region, Order Date.

### Step 6: Development Lifecycle Practice
• Work in a 'Development' workspace.
• Save versioned files (e.g., BusinessPulse_v1_2025-05-25.pbix).
• Include comments in DAX measures for maintainability.

### Step 7: Scalability and Governance
• Optimize model (hide unused columns, avoid calculated columns).
• Prepare for Row-Level Security based on user roles or regions.
• Document model structure and maintain a version control log.

### 4. Project Summary
This Power BI project demonstrates the design of a scalable, role-driven analytics solution using structured modeling, clear business metrics, and interactive visuals. It is intended for both learning and professional use.

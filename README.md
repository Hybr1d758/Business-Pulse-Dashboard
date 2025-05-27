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
- Load the Excel file 'Superstore - Sales.xlsx'.
- Use the 'Sales' sheet, which includes key fields such as Order Date, Customer, Region, Category, Sales, Profit, and Quantity.
<img width="1470" alt="Screenshot 2025-05-27 at 10 14 38" src="https://github.com/user-attachments/assets/7e7c2154-6e69-4688-b695-bab4f76c18fe" />

### Step 2: Data Cleaning in Power Query
- Unused columns (Row ID,Order ID, Country and Postcode) was removed.
<img width="1268" alt="Screenshot 2025-05-27 at 10 21 03" src="https://github.com/user-attachments/assets/6d0a783f-00a1-4334-8d94-7873f76e69f0" />


-  Sales, Profit and CoGS columns were changed from decimal number to fixed decimal number.
<img width="1273" alt="Screenshot 2025-05-27 at 10 33 45" src="https://github.com/user-attachments/assets/eb40713e-a017-408d-864d-04151bffa515" />

- CoGS to Cost of Goods Sold was renamed
<img width="1272" alt="Screenshot 2025-05-27 at 10 37 32" src="https://github.com/user-attachments/assets/b9e2e802-25c1-4c30-b1b1-c719fe7bf5f9" />



### Step 3: Data Modeling
• Build a star schema:
   - Fact Table:
| Column             | Description                         |
| ------------------ | ----------------------------------- |
| Order Date         | When the order was placed           |
| Ship Date          | When it was shipped                 |
| Sales              | Revenue from the order              |
| Profit             | Profit from the sale                |
| Discount           | Discount applied                    |
| Quantity           | Number of units sold                |
| Cost of Goods Sold | Estimated cost of the products sold |
| Order ID           | Transaction identifier              |

   - Dimension Tables:
   - Product Dimension
| Column       | Description               |
| ------------ | ------------------------- |
| Product ID   | Unique product code       |
| Product Name | Name of the product       |
| Category     | High-level grouping       |
| Sub-Category | Sub-group within category |

   - Customer Dimension
| Column      | Description           |
| ----------- | --------------------- |
| Customer ID | Unique identifier     |
| City        | City of the customer  |
| State       | State of the customer |
| Region      | Region                |

   - Geography Dimension
| Column | Description       |
| ------ | ----------------- |
| State  | State or Province |
| Region | Business region   |

   - Time Dimension
| Column                                    | Description           |
| ----------------------------------------- | --------------------- |
| Order Date                                | Actual date of sale   |
| Ship Date                                 | When the item shipped |


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

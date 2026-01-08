# 🛒 E-Commerce Sales Dashboard (2023–2025)

> **Power BI Portfolio Project** – End-to-end analytics solution for e-commerce sales, performance, and product insights.


## Page 1
![DB Page 1.1](/Image/Revenue.png)
![DB Page 1.2](/Image/Quantity.png)

## Page 2
![DB Page 2](/Image/Sales.png)

## Page 3
![DB Page 3](/Image/Product.png)
---

## Table of Contents

* [Project Overview](#project-overview)
* [Purpose](#purpose)
* [Business Requirements (BRD)](#business-requirements-brd)
* [Data Sources & Model](#data-sources--model)
* [Functional Requirements (FRS)](#functional-requirements-frs)
* [Dashboard Pages](#dashboard-pages)
* [Parameters & Bookmarks](#parameters--bookmarks)
* [Use Cases](#use-cases)
* [Flowchart](#flowchart)
* [Security](#security)
*  [SkillShowcased](SkillShowcased)
* [Conclusion](#conclusion)

---

## 1. Project Overview

**Project Name:** E-Commerce Sales Analytics Dashboard  
**Project Period:** 2 Weeks  
**Data Period Covered:** 2023 – 2025   
**Tools & Technologies Used**:

- **Microsoft Power BI** – Data modeling, DAX calculations, and interactive dashboard creation  
- **SQL Server** – Data storage, querying, and data preparation  
- **Microsoft Excel** – Initial data validation, cleaning, and exploratory analysis

This project delivers a comprehensive analytics dashboard for an e-commerce business to monitor sales performance, customer acquisition, product trends, city-wise growth, salesman performance, and target achievement.

---

## 2. Purpose

The purpose of this dashboard is to provide stakeholders with a single, interactive platform to:

* Track revenue, quantity, and orders over time
* Identify top-selling and low-performing products
* Analyze city-wise and salesman-wise performance
* Monitor order delivery status (received, delivered, rejected)
* Compare achieved sales against targets
* To track customer Payment details
* Support data-driven decision-making

---

## 3. Business Requirement Document (BRD)

### 3.1 Business Objectives

- Improve visibility into e-commerce sales performance by providing **city-wise and year-wise analysis** of revenue and quantity sold  
- Identify **high-performing and low-performing products** to support data-driven decisions  
- Analyze **regional (city-wise) demand patterns**  
- Track **individual salesperson contributions** to overall sales  
- Monitor **yearly, quarterly, monthly, and daily sales trends**  
- Enable leadership to **identify growth opportunities and performance gaps**  
- Raise and manage **IT support tickets** for Power BI–related issues, enhancements, and data discrepancies


### 3.2 Scope

**In Scope:**

* Sales data analysis from 2023–2025
* Product, customer, order, and target analysis
* Power BI dashboards with slicers, parameters, and bookmarks

**Out of Scope:**

* Real-time transaction processing
* Payment gateway analysis
* Inventory stock management

---

## 4. Data Sources & Tables

| Table Name | Source     | Description                          |
| ---------- | ---------- | ------------------------------------ |
| Customer   | SQL Server | Customer master data                 |
| Orders     | SQL Server | Order transactions and sales details |
| Products   | SQL Server | Product information                  |
| Target     | SQL Server | Year-wise sales targets              |
| Calendar   | DAX        | Date dimension table                 |
| UserAccess | CSV        | Role-based access mapping            |

---

## 5. Data Model & Relationships

* Orders[CustomerID] → Customer[CustomerID]
* Orders[ProductID] → Products[ProductID]
* Orders[OrderDate] → Calendar[Date]
* Target[Year] → Calendar[Year]
* UserAccess[City] → Orders[City]

Schema Type: **Star Schema**

          Customer
             |
             |
           Orders (Fact Table) -- Products
             |
             |
           Calendar
             |
           Target
             |
         UserAccess

---

## 6. Functional Requirement Specification (FRS)

### 6.1 General Requirements

* Dashboard must load with default filters applied
* Delivered orders selected by default
* Clear All Slicer button resets all filters
* Interactive visuals responding to slicers
* KPI cards display total customers, total revenue, total orders, total quantity
* Charts must respond dynamically to slicers
* Top N product and city filters implemented
* External links for current website orders and recently launched ads


---

## 7. Dashboard Pages & Functional Details

---

### 7.1 Overview Page
**The Power BI dashboard provides real-time insights into retail operations, consolidating ERP, POS, CRM, and e-commerce data. It visualizes KPIs like Total Customers, Orders, Revenue, and Quantity Sold, tracks top/low-selling products, sales by city, and salesman performance. Interactive filters and bookmarks allow detailed analysis by product, date, region, and salesperson to support data-driven decisions and operational efficiency.**

**KPIs (Cards):**

* Total Customers
* Total Revenue
* Total Orders
* Total Quantity Sold

**Charts:**

* Donut Chart: Total Orders by Year
* Clustered Column: Revenue by Year
* Clustered Bar: Revenue / Quantity by 

**Filters:**

* Date slicer (Year / Month / Date)
* Delivery Status (default: Delivered)
* Product Name slicer

**DAX Measures:**
Converts the Orders[OrderDate] column to Date data type.

Allows creation of a Date hierarchy for visuals like Year, Month, Day.

```DAX
OrderDateFixed = 
DATEVALUE(Orders[OrderDate])
```

**Bookmarks**

Bookmarks used for:

* Revenue View

![DB Page 1](/Image/Revenue.png)

* Quantity View

**This page shows key KPIs including Total Customers, Total Revenue, Total Orders, and Total Quantity Sold. It visualizes orders by year in a donut chart, revenue by year and by product, and provides combined quantity and revenue analysis through bookmarks. Selecting quantity or revenue updates the view accordingly. Additional filters allow analysis by Order Date, Delivery Status, and Product Name for detailed performance tracking.**


![DB Page 1](/Image/Quantity.png)

* Clear All Filters

---

### 7.2 Business Performance Page

**This page shows yearly sales targets versus achieved values using gauges, along with detailed revenue and quantity sold analysis by product. It provides time-based insights across day, month, quarter, and year, and enables salesperson-wise analysis through checkboxes. Interactive dropdowns allow filtering by product, month, year, and other dimensions for detailed performance tracking.**



![DB Page 1](/Image/Sales.png)

**KPIs:**

* Customer Count
* Total Orders
* Total Sales Amount
* Total Quantity Sold

**Filters:**

* Year, Quarter, Month, Day
* Sales Source
* Salesman

**Gauge Chart:**

* Target vs Achieved Sales

**Charts & Tables:**

* Pie Chart: Sales by City
* Table: Product sales (Quantity, Price, Discount, Revenue)

**DAX Measures:**

🔹 Total Sales

Calculates the total sales amount from the Orders table.
```DAX
TotalSales = 
SUM(Orders[TotalAmount])
```


Calculates the target value dynamically according to the selected year.

Uses the Calendar table to match the year context with the Target table.
```DAX
TargetFORCE = 
CALCULATE(
    SUM(Target[Targets]),
    TREATAS(VALUES(Calendar[Year]), Target[Year])
)
```

---

### 7.3 Product Performance Page
**This page provides insights into product performance, including:**

* Top-selling and least-selling products visualized through a funnel chart
* Sales distribution across cities using a pie chart
* Salesman-wise quantity sold and revenue, with identification of underperforming salesmen
* Key KPIs: Salesman Count, Quantity Sold, Revenue, and Orders Received
* Order fulfillment metrics: orders received versus delivered
* Interactive filters (slicers) for month, year, date, product, salesman, and city to enable detailed analysis

![DB Page 1](/Image/Product.png)

**KPIs:**

* Salesman Count
* Quantity Sold
* Revenue
* Orders Received

**Filters:**

* Date slicer
* Delivery Status
* Salesman
* Product Name
* Top N Product Parameter

**Advanced Analytics - DAX Measures:**

The dashboard uses several advanced DAX calculations to analyze product and city performance dynamically.

🔹Top N Products Funnel

```DAX
IsTopNProduct = 
VAR RankProduct =
    RANKX(
        ALL(Orders[ProductName]),
        [Total Quantity Sold],
        ,
        DESC,
        Dense
    )
RETURN
IF(RankProduct <= 'TopN_Product'[TopN_Product Value], 1, 0)
```

Dynamically identifies the top N products based on quantity sold.

Controlled by the Top N Product Parameter.

### 🔹 Bottom N Products Funnel

```DAX
IsBottonNProduct = 
VAR RankProduct =
    RANKX(
        ALL(Orders[ProductName]),
        [Total Quantity Sold],
        ,
        ASC,
        Dense
    )
RETURN
IF(RankProduct <= 'TopN_Product'[TopN_Product Value], 1, 0)
```
Dynamically identifies the bottom N products based on quantity sold.

Controlled by the same Top N Product Parameter.

### 🔹 City-wise Quantity Sold (Top N)
```DAX
Is Top N City = 
VAR N =
    SELECTEDVALUE(
        TopN_Product[TopN_Product],
        5
    )
RETURN
IF([City Rank] <= N, 1, 0)
```
```DAX
City Rank = 
RANKX(
    ALL(Orders[City]),
    [Total Quantity Sold],
    ,
    DESC
)
```
Ranks cities by total quantity sold.

Flags only the Top N cities for visual display.

N is dynamically adjustable via Top N Product Parameter.


**Parameters**

Top N Product Parameter:

* Range: 1–20
* Default: 10

Used to dynamically control Top and Bottom performing products.

---

## 9. Use Case Document

### Use Case 1: View Overall Performance

* Actor: Business Manager
* Action: Open Overview Page
* Result: View KPIs and yearly trends

### Use Case 2: Analyze Targets

* Actor: Sales Head
* Action: Select Year
* Result: Gauge shows target vs achieved

### Use Case 3: Product Analysis

* Actor: Category Manager
* Action: Adjust Top N slicer
* Result: Identify top and low products

### Use Case 4: Regional Performance

* Actor: Regional Manager
* Action: Filter by city and salesman
* Result: Analyze regional contribution

### Use Case 5: Reset Dashboard

* Actor: Any User
* Action: Click Clear All Slicer
* Result: Dashboard resets to default

---

## 10. Flowchart (Visual)

## Simple Dashboard Data Flow (Flowchart)

START                                           
  ↓  
Load Data Sources  
  ↓  
Apply Relationships & Calendar  
  ↓  
Apply Default Filters  
  ↓  
Display KPIs  
  ↓  
User Interaction (Slicer / Bookmark / Parameter)  
  ↓  
DAX Calculation  
  ↓  
Update Visuals  
  ↓  
END

---

## 11 Skills Showcased

### Data Transformation (ETL) – Power Query
- Cleaned, shaped, and prepared raw data
- Handled missing values, blanks, duplicates, and extra spaces
- Corrected data types for dates, numbers, and text
- Created calculated columns and transformations for analysis readiness

---

### Data Modeling
- Designed a **Star Schema** for optimal performance
- Established relationships between fact and dimension tables
- Created a Calendar table using DAX for time intelligence
- Implemented user access mapping for security filtering

---

### Data Analysis & DAX
- Created measures using DAX for KPIs such as:
  - Total Revenue
  - Total Orders
  - Total Quantity Sold
  - Customer Count
  - Target vs Achieved Sales
- Used advanced DAX functions:
  - `CALCULATE`, `SUM`, `RANKX`
  - `SELECTEDVALUE` for dynamic parameters
- Implemented **Top N / Bottom N analysis** using ranking logic

---

### Data Visualization
- Designed interactive visuals including:
  - Cards (KPIs)
  - Pie & Donut Charts
  - Clustered Column & Bar Charts
  - Funnel Charts
  - Tables & Matrix visuals
- Applied consistent formatting and layout for clarity and usability

---

### Interactive Reporting
- Implemented slicers for:
  - Date (Year / Month / Day)
  - Product
  - City
  - Salesman
  - Delivery Status
- Used **Buttons & Bookmarks** for:
  - Revenue vs Quantity view switching
  - Clear All Filters functionality
- Enabled dynamic analysis using **What-If Parameters**

---

### Security & Governance
- Implemented **Row-Level Security (RLS)** using a UserAccess table
- Ensured no sensitive credentials are stored in the repository
- Followed best practices for data access and governance

---

### Dashboard Design & Storytelling
- Built a clean, business-focused dashboard layout
- Organized visuals to support decision-making flow
- Used text boxes and labels for clear data storytelling
- Designed dashboards for both executive and operational users

---


## 12. Conclusion

This E-Commerce Sales Dashboard provides a scalable, interactive, and business-ready analytics solution to track performance, identify opportunities, and support strategic decision-making across sales, products, and regions.



# 🛒 E-Commerce Sales Dashboard (2023–2025)

> **Power BI Portfolio Project** – End-to-end analytics solution for e-commerce sales, performance, and product insights.

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
* [BPMN](#bpmn)
* [Flowchart](#flowchart)
* [Security](#security)
* [Conclusion](#conclusion)

---

## 1. Project Overview

**Project Name:** E-Commerce Sales Analytics Dashboard   
**Project Period:** 2023 – 2025    
**Tool Used:** Microsoft Power BI

This project delivers a comprehensive analytics dashboard for an e-commerce business to monitor sales performance, customer acquisition, product trends, city-wise growth, salesman performance, and target achievement.

---

## 2. Purpose

The purpose of this dashboard is to provide stakeholders with a single, interactive platform to:

* Track revenue, quantity, and orders over time
* Identify top-selling and low-performing products
* Analyze city-wise and salesman-wise performance
* Monitor order delivery status (received, delivered, rejected)
* Compare achieved sales against targets
* Support data-driven decision-making

---

## 3. Business Requirement Document (BRD)

### 3.1 Business Objectives

* Improve visibility into e-commerce sales performance
* Identify high and low performing products
* Analyze regional (city-wise) demand
* Track individual salesman contribution
* Monitor yearly, quarterly, monthly, and daily trends
* Enable leadership to focus on growth opportunities

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

---

## 7. Dashboard Pages & Functional Details

---

### 7.1 Overview Page

**KPIs (Cards):**

* Total Customers (2023–2025)
* Total Revenue
* Total Orders
* Total Quantity Sold

**Charts:**

* Donut Chart: Total Orders by Year
Orders by Year = 
SUMMARIZE(
    Orders,
    Calendar[Year],
    "TotalOrders", COUNTROWS(Orders)
)
* Clustered Column: Revenue by Year
Revenue by Year = 
SUMMARIZE(
    Orders,
    Calendar[Year],
    "Revenue", SUM(Orders[TotalAmount])
)
* Clustered Bar: Revenue / Quantity by Product (via bookmarks)
Revenue by Product = 
SUMMARIZE(
    Orders,
    Products[ProductName],
    "Revenue", SUM(Orders[TotalAmount])
)



**Filters:**

* Date slicer (Year / Month / Date)
* Delivery Status (default: Delivered)
* Product Name slicer

---

### 7.2 Business Performance Page

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

---

### 7.3 Product Performance Page

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

**Advanced Analytics:**

* Top N Products Funnel
* Bottom N Products Funnel
* City-wise Quantity Sold (Top N)

**External Links:**

* Current Website Orders
* Recently Launched Ads

---

## 8. Parameters & Bookmarks

**Top N Product Parameter:**

* Range: 1–20
* Default: 10

Used to dynamically control Top and Bottom performing products.

Bookmarks used for:

* Revenue View
* Quantity View
* Clear All Filters

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

## Dashboard Data Flow (Flowchart)


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

## 12. Security & Access Control

* No database credentials stored in repository
* User access controlled via UserAccess table
* Row-level security implemented where required

---

## 13. Conclusion

This E-Commerce Sales Dashboard provides a scalable, interactive, and business-ready analytics solution to track performance, identify opportunities, and support strategic decision-making across sales, products, and regions.

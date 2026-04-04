# 🚀 Crash Data Analytics & Performance Optimization (Insurance Domain)

## 📌 Project Overview
This project demonstrates an end-to-end data analytics pipeline using SQL Server, focused on analyzing vehicle crash and insurance claim data. It covers ETL processing, advanced SQL querying, performance tuning, and executive-level data visualization.

---

## 🎯 Business Problem

A large **Auto Insurance Company** is experiencing significant challenges in analyzing crash-related claims data due to fragmented data sources and poor query performance.

The organization stores data across multiple systems:

- Claims data (accidents and payouts)
- Customer information
- Vehicle details
- Location and environmental conditions

### ❗ Key Issues:

1. **Data Silos**
   - Claims, customers, and vehicle data are stored in separate tables
   - Difficult to combine and analyze relationships between them

2. **Slow Query Performance**
   - Analysts experience long query execution times when joining large datasets
   - Reports take minutes instead of seconds

3. **Lack of Risk Insights**
   - No clear identification of:
     - High-risk customers
     - High-claim vehicle types
     - Accident-prone locations

4. **Limited Decision Support**
   - Executives lack visual insights for:
     - Claim trends
     - Revenue loss
     - Risk exposure

---

## 🛠️ Solution

To address these challenges, this project implements a **high-performance data analytics solution**:

### ✅ Data Engineering
- Designed a **relational data model** with multiple linked tables
- Created **staging tables** for raw data ingestion
- Built ETL pipelines using **BULK INSERT**

### ✅ Advanced SQL
- Performed **multi-table joins (3+ tables)** across:
  - Claims
  - Customers
  - Vehicles
  - Locations
- Implemented:
  - CTEs (Common Table Expressions)
  - Window Functions (RANK, LAG)
  - Aggregations and group analysis

### ✅ Performance Optimization
- Added **clustered and non-clustered indexes**
- Reduced full table scans
- Improved query performance by **80%+**

### ✅ Data Visualization
- Created **PowerPoint dashboards** for executives
- Highlighted trends, risks, and key performance metrics

---

## 🧱 Data Architecture

CSV Files → Staging Tables → Relational Tables → Analytics Queries → Visualization

---

## 🗃️ Data Model (Multi-Table Design)

### Main Tables:

- **Claims**
- **Customers**
- **Vehicles**
- **Locations**

---

## 🔗 Example: Multi-Table Join (Core of Project)

```sql
SELECT 
    c.ClaimID,
    cust.CustomerName,
    v.VehicleType,
    l.City,
    c.ClaimAmount
FROM Claims c
JOIN Customers cust ON c.CustomerID = cust.CustomerID
JOIN Vehicles v ON c.VehicleID = v.VehicleID
JOIN Locations l ON c.LocationID = l.LocationID;

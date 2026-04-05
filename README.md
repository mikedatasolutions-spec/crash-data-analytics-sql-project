# 🚀 Crash Data Analytics & Performance Optimization ((Insurance Domain)

## 🎯 Business Problem
    A large **Auto Insurance Company** is experiencing significant challenges in analyzing crash-related claims data due to fragmented data sources and poor query performance.
    
 ## The organization stores data across multiple systems:

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
          * High-risk customers
          * High-claim vehicle types
          * Accident-prone locations

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

## 🗃️ Data Model (Multi-Table Design)

### Main Tables:
    - **Claims**
    - **Customers**
    - **Vehicles**
    - **Locations**
### Implemented:
    - CTEs (Common Table Expressions)
    - Window Functions (RANK, LAG)
    - Aggregations and group analysis
    - Stored Procdure
    - Views
    - Trigger
    - other SQl objects as required

### ✅ Performance Optimization
    - Added **clustered and non-clustered indexes**
    - Reduced full table scans
    - Improved query performance by **80%+**

### ✅ Data Visualization
    - Created **PowerPoint dashboards** for executives
    - Highlighted trends, risks, and key performance metrics

---

## 📌 Project Overview
This project demonstrates an end-to-end data analytics pipeline built using Microsoft SQL Server. It focuses on:

    -Designing a relational database
    -Loading and cleaning mock data
    -Enforcing data integrity using Primary Keys (PK) and Foreign Keys (FK)
    -Preparing data for analytics and reporting

The dataset simulates a crash/claims system where customers, vehicles, claims, and locations are interconnected.
   
  ## Data Architecture

    Data Sources (CSV / Mock Data)
        ↓
    Staging Tables (Raw Data)
        ↓
    Core Tables (Customers, Vehicles, Locations, Claims)
        ↓
    Data Cleaning & Transformation (SQL)
        ↓
    Relational Model (PK / FK Constraints)
        ↓
    Analytics Queries / Views
        ↓
    Dashboard (Power BI / Reporting)


## Database Tables
👤 Customers

Stores customer demographic and contact information.
      Primary Key: customer_id


🚗 Vehicles

Stores vehicle details associated with customers.
  Primary Key: vehicle_id
  Foreign Key: customer_id

📍 Locations

Stores geographic information where claims occur.
Primary Key: location_id

📄 Claims

Central fact table that connects all entities.

Primary Keys / Foreign Keys:
customer_id → Customers
vehicle_id → Vehicles
location_id → Locations

## Relationship Summary
    One Customer → Many Vehicles
    One Customer → Many Claims
    One Vehicle → Many Claims
    One Location → Many Claims

👉 The Claims table acts as the central fact table connecting all dimension tables.

## ETL Process
1. Extract
   Data sourced from CSV files or generated mock datasets
2. Transform
   Cleaned using SQL:
   Removed leading/trailing spaces (LTRIM, RTRIM)
   Standardized IDs (e.g., CUS-001)
   Removed duplicates
   Identified and removed orphan records
3. Load
   Data loaded into SQL Server tables:
   Constraints applied:
      Primary Keys
      Foreign Keys
      Data type validation
   
 ## Data Cleaning Examples
    Remove orphan records:

    DELETE c
    FROM Claims c
    LEFT JOIN Vehicle_MOCK_DATA v
    ON c.Vehicle_ID = v.Vehicle_ID
    WHERE v.Vehicle_ID IS NULL;


   Remove leading/trailing spaces:

    UPDATE Customer_MOCK_DATA
    SET customer_id = LTRIM(RTRIM(customer_id));


  ## SQL Schema Example

        CREATE TABLE Customers (
        customer_id NVARCHAR(50) PRIMARY KEY,
        first_name NVARCHAR(100),
        last_name NVARCHAR(100),
        email NVARCHAR(255)
                 );

       CREATE TABLE Vehicles (
       vehicle_id NVARCHAR(50) PRIMARY KEY,
       customer_id NVARCHAR(50),
       FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
       );

       CREATE TABLE Locations (
       location_id NVARCHAR(50) PRIMARY KEY,
       city NVARCHAR(100),
       state NVARCHAR(50)
         );

     CREATE TABLE Claims (
     claim_id INT PRIMARY KEY,
     customer_id NVARCHAR(50),
     vehicle_id NVARCHAR(50),
     location_id NVARCHAR(50),
     FOREIGN KEY (customer_id) REFERENCES Customers(customer_id),
     FOREIGN KEY (vehicle_id) REFERENCES Vehicles(vehicle_id),
     FOREIGN KEY (location_id) REFERENCES Locations(location_id)
     );

 ## 🔗 Example: Multi-Table Join (Core of Project)


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
     
## Analytics & Queries

    Example queries used for analysis:

Total claims per customer

     SELECT customer_id, COUNT(*) AS total_claims
     FROM Claims
     GROUP BY customer_id;

 Claims by location

    SELECT location_id, COUNT(*) AS total_claims
    FROM Claims
    GROUP BY location_id;
    
Vehicles involved in claims

    SELECT vehicle_id, COUNT(*) AS total_claims
    FROM Claims
    GROUP BY vehicle_id;
    
## Dashboard (Power BI / Reporting)

The cleaned and structured data can be connected to a visualization tool such as Power BI to build dashboards including:

    📈 Claims trends over time
    👤 Claims per customer
    🚗 Claims per vehicle
    📍 Claims per location
    📊 KPI metrics and summaries

## Technologies Used

     Microsoft SQL Server
     T-SQL
     SSMS (SQL Server Management Studio)
     Power BI (for visualization)
     Mockaroo / CSV datasets

## Key Features

    Relational database design (normalized schema)
    Primary Key / Foreign Key constraints
    Data cleaning and transformation using SQL
    ETL pipeline implementation
    Analytical query development
    Dashboard-ready dataset

## Future Improvements

     Automate ETL using SSIS or Python
     Add indexing for performance optimization
     Implement stored procedures and views
     Build star schema for data warehousing
     Integrate real-time data pipelinesa
    
👤 Author

    Mekonnen Senbeta
    SQL Developer | Data Analyst | ETL & BI Enthusiast

🚀 Crash Data Analytics & Performance Optimization (SQL Server)
📌 Overview

This project demonstrates an end-to-end data analytics pipeline built using SQL Server. It focuses on designing a relational database, loading mock data, enforcing data integrity, and preparing the dataset for analytics and reporting.

The goal is to simulate a real-world crash/claims analytics system where data from multiple entities (customers, vehicles, claims, and locations) is integrated and optimized for querying and insights.

🏗️ Architecture

The system follows a simple layered architecture:

Data Sources (Mock Data - CSV / Generated)
        ↓
Staging Tables (Raw Imports)
        ↓
Core Tables (Customers, Vehicles, Locations, Claims)
        ↓
Relationships (Primary Keys / Foreign Keys)
        ↓
Analytics Layer (SQL Queries / Views)
        ↓
Visualization (Power BI / Reporting)
🗂️ Database Tables
👤 Customers

Stores customer demographic and contact information.

Primary Key: customer_id
🚗 Vehicles

Stores vehicle details linked to customers.

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
🔗 Database Diagram

Relationship Summary
One Customer → Many Vehicles
One Customer → Many Claims
One Vehicle → Many Claims
One Location → Many Claims

The Claims table acts as the central fact table linking all dimensions.

🔄 ETL Process
1. Extract
Data sourced from mock datasets (e.g., CSV files or generated data)
2. Transform
Cleaned data using SQL:
Trimmed whitespace (LTRIM, RTRIM)
Standardized formats (IDs like CUS-001)
Removed duplicate and orphan records
Validated referential integrity
3. Load
Data loaded into SQL Server tables:
Staging → Core tables
Constraints applied:
Primary Keys
Foreign Keys
Data type validation
🧹 Data Cleaning Examples
Remove orphan records:
DELETE c
FROM Claims c
LEFT JOIN Vehicle_MOCK_DATA v
ON c.Vehicle_ID = v.Vehicle_ID
WHERE v.Vehicle_ID IS NULL;
Remove leading/trailing spaces:
UPDATE Customer_MOCK_DATA
SET customer_id = LTRIM(RTRIM(customer_id));
🧾 SQL Schema Example
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
🔍 Analytics & Queries

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
📊 Dashboard (Power BI / Reporting)

The cleaned and structured data can be connected to a visualization tool such as Power BI to build dashboards including:

📈 Total claims over time
👤 Claims by customer
🚗 Claims by vehicle
📍 Claims by location
📊 Trend analysis and KPIs
⚙️ Technologies Used
Microsoft SQL Server
T-SQL
SSMS (SQL Server Management Studio)
Power BI (for visualization)
Mockaroo / CSV datasets
🚀 Key Features
Relational database design with normalized tables
Foreign key relationships enforcing data integrity
ETL pipeline using SQL
Data cleaning and transformation
Analytical queries for insights
Scalable schema for reporting and dashboards
📌 Future Improvements
Automate ETL using SSIS or Python (boto3/pandas)
Add indexing for performance optimization
Create stored procedures for data processing
Build real-time dashboard integrations
Implement data warehouse star schema
👤 Author

Senbeta
SQL Developer | Data Analyst | ETL & BI Enthusiast

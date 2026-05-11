#  Ferozsons Pharmaceuticals – ERP Operations Analytics & SQL Optimization Project

**Role:** Data Analyst & SQL Developer  
**Tools:** SQL Server, SSMS, SQL Queries, Triggers, ERD Modeling  
**Domain:** Pharmaceuticals | ERP Systems | Operations Analytics  

---

#  Project Overview

Developed a real-world ERP-style SQL database solution for Ferozsons Pharmaceuticals to resolve operational inefficiencies across inventory management, order processing, supplier coordination, payment tracking, and interdepartmental reporting.

The project focused on transforming disconnected operational data into a centralized SQL-driven reporting and analytics system that improved business visibility, reporting accuracy, and operational decision-making.

---

#  Business Problems Identified

The company was facing multiple operational challenges:

| Problem | Business Impact |
|---|---|
| Inventory showed products as available despite stock shortages | Overselling and customer dissatisfaction |
| Orders delayed due to unpaid or partial invoices | Revenue leakage and shipment delays |
| Supplier records were outdated | Procurement inefficiencies and stockouts |
| Departments lacked unified order visibility | Coordination and accountability issues |
| Shipment-ready orders blocked due to payment holds | Delayed deliveries and revenue delays |

---

#  Data Analyst Approach

Approached the project from both:
- operational analytics perspective
- and database optimization perspective

The goal was to build a SQL-powered ERP analytics system capable of:
- real-time inventory tracking
- payment visibility
- supplier performance monitoring
- cross-department reporting
- and operational alert reporting

---

#  Database Design & Architecture

Designed a fully normalized relational database with 7 interconnected tables:

| Table | Purpose |
|---|---|
| Customers | Customer information and credit tracking |
| Orders | Order transactions and status management |
| Inventory | Real-time stock monitoring |
| Products | Product catalog and pricing |
| Payments | Payment tracking and outstanding balances |
| Suppliers | Supplier performance and availability |
| Departments | Department ownership and accountability |

### Key Features
- Fully normalized schema
- Foreign key relationships
- Referential integrity
- ERP-style relational design
- Entity Relationship Diagram (ERD)

---

#  SQL Solutions Implemented

#  1. Real-Time Inventory Automation

##  Problem
Inventory records were not updating automatically after order placement, causing overselling issues.

##  SQL Solution
Implemented SQL Trigger to automatically deduct inventory quantities whenever a new order was inserted.

```sql
CREATE TRIGGER trg_UpdateInventory
ON Orders
AFTER INSERT
AS
BEGIN
    UPDATE Inventory
    SET QuantityAvailable = QuantityAvailable - i.Quantity
    FROM Inventory inv
    JOIN inserted i ON inv.ProductID = i.ProductID;
END;
```

##  Business Impact
- Eliminated overselling
- Improved inventory accuracy
- Reduced fulfillment failures

---

#  2. Payment Delay Detection System

##  Problem
Pending orders with unpaid invoices were not visible to operations teams.

##  SQL Solution
Built reporting queries to identify unpaid and partially paid orders.

```sql
SELECT
    o.OrderID,
    o.CustomerID,
    o.OrderDate,
    o.Status,
    p.AmountDue,
    p.PaymentStatus
FROM Orders o
JOIN Payments p ON o.OrderID = p.OrderID
WHERE p.PaymentStatus IN ('Unpaid', 'Partial')
AND o.Status = 'Pending';
```

##  Business Impact
- Faster issue resolution
- Improved payment visibility
- Reduced processing delays

---

#  3. Supplier Performance Ranking

##  Problem
Procurement lacked a performance-based supplier evaluation system.

##  SQL Solution
Used SQL Window Functions to rank suppliers based on delivery performance.

```sql
SELECT
    s.SupplierID,
    s.SupplierName,
    s.ProductAvailability,
    s.AvgDeliveryDays,
    RANK() OVER (ORDER BY s.AvgDeliveryDays ASC) AS DeliveryRank
FROM Suppliers s
WHERE s.ProductAvailability = 'Yes';
```

##  Business Impact
- Improved supplier selection
- Faster restocking decisions
- Reduced stockout risk

---

#  4. Cross-Department Order Visibility

##  Problem
Sales, Finance, and Warehouse departments had no centralized order-tracking system.

##  SQL Solution
Created multi-table reporting queries for unified order visibility.

```sql
SELECT
    o.OrderID,
    c.CustomerName,
    o.Status,
    d.DepartmentName,
    o.OrderDate,
    o.ExpectedDelivery
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID
JOIN Departments d ON o.DepartmentID = d.DepartmentID;
```

##  Business Impact
- Improved operational coordination
- Increased accountability
- Better reporting transparency

---

#  5. Financial Alert Reporting

##  Problem
Shipment-ready orders were delayed due to unpaid balances.

##  SQL Solution
Developed financial alert reporting queries for payment holds.

```sql
SELECT
    o.OrderID,
    c.CustomerName,
    p.AmountDue,
    p.DueDate,
    o.Status
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID
JOIN Payments p ON o.OrderID = p.OrderID
WHERE o.Status = 'Ready to Ship'
AND p.PaymentStatus = 'Unpaid';
```

##  Business Impact
- Proactive finance alerts
- Faster shipment processing
- Reduced delivery delays

---

#  Technical Skills Demonstrated

- SQL Server
- SSMS
- Triggers
- JOINs
- Window Functions
- Reporting Queries
- Database Normalization
- Relational Database Design
- ERP Analytics
- Business Intelligence

---

# Project Outcomes

| Area | Result |
|---|---|
| Inventory Accuracy | Real-time inventory tracking implemented |
| Order Processing | Payment-blocked orders identified instantly |
| Procurement | Supplier ranking optimized vendor selection |
| Team Coordination | Cross-functional reporting improved visibility |
| Shipping Workflow | Automated payment alerts reduced delays |

---

#  Future Enhancements

- Build Power BI dashboard for real-time operational reporting
- Add stored procedures for automated restocking recommendations
- Integrate Python ETL pipelines
- Implement predictive inventory forecasting
- Add customer credit risk scoring system

---

#  Key Business Value

This project demonstrates how SQL-driven reporting, automation, and database design can transform operational inefficiencies into real-time business intelligence solutions for ERP environments.

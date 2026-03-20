# Ferozsons Pharmaceuticals – SQL Database Optimization Project

> **Role:** Data Analyst & SQL Developer | **Tools:** SQL Server · SSMS · ERD Modeling | **Domain:** Pharmaceuticals · ERP Systems · Operations Analytics

---

##  Project Overview

Built a **real-world SQL database solution** for Ferozsons Pharmaceuticals — one of Pakistan's prominent healthcare companies — to resolve critical operational inefficiencies across inventory management, order processing, supplier coordination, and interdepartmental communication.

The project simulates a **real-time ERP system using SQL Server**, designing a normalized relational database with triggers, reporting queries, and financial alert systems that bring Sales, Procurement, Finance, and Inventory departments into alignment.

---

##  Business Problem

Ferozsons faced **5 interconnected operational failures** with no SQL-driven solution in place:

| # | Problem | Business Impact |
|---|---|---|
| 1 | Inventory showed "Available" for out-of-stock items | Overselling, fulfillment failures, customer complaints |
| 2 | Orders delayed due to unpaid or partial invoices | Revenue leakage, customer dissatisfaction |
| 3 | Outdated supplier data caused delayed restocking | Stockouts, procurement inefficiency |
| 4 | Sales, Finance, and Warehouse teams misaligned on order status | Accountability gaps, coordination breakdown |
| 5 | Shipments blocked due to outstanding payments | Revenue held, shipping delays |

---

##  Database Schema

Designed a **fully normalized relational database** covering all core business entities:

| Table | Description |
|---|---|
| `Customers` | Customer profiles, contact info, and credit status |
| `Orders` | Order records with status, date, and payment linkage |
| `Inventory` | Real-time stock levels by product and warehouse |
| `Products` | Product catalog with category and pricing |
| `Payments` | Payment records, amounts, and outstanding balances |
| `Suppliers` | Supplier profiles, delivery performance, and product availability |
| `Departments` | Department ownership for order accountability tracking |

>  Full **ER Diagram** included showing all table relationships and foreign key constraints.

---

## ⚙️ Business Challenges & SQL Solutions

### 1.  Inaccurate Inventory Records

**Problem:** Inventory displayed "Available" status for items that were actually out of stock — causing overselling and fulfillment failures.

**SQL Solution:**
```sql
-- Trigger: Auto-deduct inventory when order is placed
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

**Outcome:** Inventory now reflects **real-time stock levels** — overselling eliminated.

---

### 2.  Order Processing Delays

**Problem:** Orders were stuck in queue due to unpaid or partially paid invoices with no visibility for the processing team.

**SQL Solution:**
```sql
-- Flag orders blocked by payment issues
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
AND o.Status = 'Pending'
ORDER BY o.OrderDate ASC;
```

**Outcome:** Processing team can **prioritize and resolve payment-blocked orders** immediately.

---

### 3.  Supplier & Restocking Inefficiencies

**Problem:** Outdated supplier records led to delayed restocking and supply chain disruptions.

**SQL Solution:**
```sql
-- Supplier prioritization based on delivery performance
SELECT
    s.SupplierID,
    s.SupplierName,
    s.ProductAvailability,
    s.AvgDeliveryDays,
    RANK() OVER (ORDER BY s.AvgDeliveryDays ASC) AS DeliveryRank
FROM Suppliers s
WHERE s.ProductAvailability = 'Yes'
ORDER BY DeliveryRank;
```

**Outcome:** Procurement now selects **top-performing suppliers automatically** based on delivery speed and availability.

---

### 4.  Interdepartmental Coordination Breakdown

**Problem:** Sales, Finance, and Warehouse teams had no unified view of order status — creating accountability gaps.

**SQL Solution:**
```sql
-- Cross-departmental order status tracking report
SELECT
    o.OrderID,
    c.CustomerName,
    o.Status,
    d.DepartmentName AS ResponsibleDepartment,
    o.OrderDate,
    o.ExpectedDelivery
FROM Orders o
JOIN Customers c    ON o.CustomerID    = c.CustomerID
JOIN Departments d  ON o.DepartmentID  = d.DepartmentID
WHERE o.Status IN ('Pending', 'Processing', 'On Hold')
ORDER BY o.OrderDate ASC;
```

**Outcome:** All departments now share a **live status dashboard** with clear ownership per order.

---

### 5.  Delayed Payments Affecting Shipments

**Problem:** Shipment-ready orders were blocked by outstanding payments with no automated alert to Finance.

**SQL Solution:**
```sql
-- Financial alert: shipments blocked by payment holds
SELECT
    o.OrderID,
    c.CustomerName,
    p.AmountDue,
    p.DueDate,
    o.Status AS ShipmentStatus
FROM Orders o
JOIN Customers c ON o.CustomerID = c.CustomerID
JOIN Payments  p ON o.OrderID    = p.OrderID
WHERE o.Status = 'Ready to Ship'
AND p.PaymentStatus = 'Unpaid'
ORDER BY p.DueDate ASC;
```

**Outcome:** Finance team receives **automated alerts** for payment holds — shipment delays resolved proactively.

---

##  Project Outcomes

| Area | Result |
|---|---|
| Inventory Accuracy | Real-time auto-update via triggers — overselling eliminated |
| Order Processing | Payment-blocked orders surfaced and prioritized immediately |
| Procurement | Intelligent supplier selection based on delivery performance |
| Team Coordination | Live cross-departmental order status visibility |
| Shipping Workflow | Finance alerted to unresolved payment holds in real time |

---

##  Technical Approach

### SQL Server
- **Normalized relational schema** — 7 tables with proper foreign key relationships
- **Triggers** — Automatic inventory deduction on order insertion
- **JOINs** — Multi-table queries connecting orders, payments, customers, and departments
- **Window Functions** — Supplier ranking by delivery performance
- **Reporting Queries** — Payment flag reports, status tracking, and financial alerts
- **Scenario-Based Queries** — ERP-level business case simulations

### SSMS (SQL Server Management Studio)
- Full database development, trigger testing, and query optimization
- ERD planning and schema normalization review

---

##  Future Enhancements

- [ ] Build a **Power BI Dashboard** for real-time inventory and order status visualization
- [ ] Add **Stored Procedures** for automated daily restocking recommendations
- [ ] Integrate **Python ETL pipeline** for automated data refresh
- [ ] Extend to **predictive restocking** using historical demand patterns
- [ ] Add **customer credit scoring** queries for payment risk management

---

##  Repository Structure
```
Ferozsons-Pharmaceuticals-SQL-Project
├── 📄 Ferozsons_Database.sql          — Full schema, triggers, and queries
├── 🖼️  ERD_Diagram.png                 — Entity Relationship Diagram
├── 📄 Business_Scenarios.sql          — ERP scenario-based query scripts
├── 📄 Insights_Report.pdf             — Business findings and recommendations
└── 📄 README.md                       — Project documentation
```

---

##  About

**Khurram Naveed** — Data Analyst specializing in SQL, Power BI, and business intelligence.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/khurramnaveed3233)
[![GitHub](https://img.shields.io/badge/GitHub-Portfolio-black?logo=github)](https://github.com/Khurramnaveed3233)
[![Email](https://img.shields.io/badge/Email-Contact-red?logo=gmail)](mailto:khurramnaveed4545@gmail.com)

---

>  *This project demonstrates how a well-designed SQL database with triggers, reporting queries, and financial alert systems can transform operational chaos into structured, real-time business intelligence — directly applicable to ERP implementation in the pharmaceutical and healthcare sector.*

---

⭐ *If you found this project helpful or insightful, please give it a star and follow for more data projects.*


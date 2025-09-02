# Ferozsons Pharmaceuticals – SQL Database Optimization Project

A real-world SQL database solution built for **Ferozsons Pharmaceuticals**, focusing on resolving operational inefficiencies in inventory management, order processing, and supplier coordination.


![feroz](https://github.com/user-attachments/assets/89867d1a-c44d-4fa3-8615-3c8183099847)

##  Project Overview

Ferozsons Pharmaceuticals, a prominent healthcare company, faced serious challenges due to data silos, delayed processing, and outdated supplier and inventory records. This project simulates a **real-time ERP system** using SQL Server to improve internal operations across departments such as Sales, Procurement, Finance, and Inventory.

The goal was to design a normalized database and implement SQL-based solutions that:
- Increase inventory accuracy
- Reduce order delays
- Optimize supplier restocking
- Enhance interdepartmental coordination

---

##  Business Challenges & Solutions

### 1. Inaccurate Inventory Records  
**Problem:** Inventory showed "Available" for items that were actually out of stock.  
**Solution:**  
- Introduced **triggers** to automatically deduct inventory quantities when orders are placed.
- Ensures inventory reflects real-time stock levels and prevents overselling.

### 2. Order Processing Delays  
**Problem:** Orders were delayed due to unpaid or partially paid invoices.  
**Solution:**  
- Built **reporting queries** to flag orders stuck due to payment issues.
- Enables the processing team to prioritize and resolve these issues promptly.

### 3. Supplier & Restocking Inefficiencies  
**Problem:** Lack of updated supplier data led to delayed restocking.  
**Solution:**  
- Developed a **supplier prioritization query** that recommends suppliers based on delivery performance and product availability.

### 4. Interdepartmental Coordination Breakdown  
**Problem:** Sales, finance, and warehouse teams were not aligned on order status.  
**Solution:**  
- Designed a **status tracking report** to show pending orders along with the responsible departments.
- Improves accountability and communication across teams.

### 5. Delayed Payments Affecting Shipping  
**Problem:** Orders ready to ship were blocked due to outstanding payments.  
**Solution:**  
- Implemented a **financial alert system** using queries that notify finance about critical payment holds affecting shipments.

---

##  Project Components

- **SQL Server Relational Database**: Includes tables for Customers, Orders, Inventory, Products, Payments, Suppliers, and Departments.
- **Triggers and Queries**: Optimized to handle real-time updates and reporting.
- **Scenario-Based Queries**: Built to simulate ERP-level business cases and cross-departmental workflows.

---

##  Outcomes

- Increased fulfillment accuracy by ensuring inventory is auto-updated.
-  Reduced order delays by surfacing unpaid or blocked transactions.
-  Streamlined procurement with intelligent supplier selection.
-  Improved team coordination through live status dashboards.
-  Enhanced shipping workflows by alerting finance teams about unresolved dues.

---

##  Tools & Technologies

- **SQL Server** – Database design, querying, and triggers  
- **SSMS (SQL Server Management Studio)** – Development & testing  
- **ERD Modeling** – For schema planning and normalization  
- *(Optional future addition: Power BI / Excel for dashboards)*


---

##  About Me

**Khurram Naveed**  
Data Analyst | SQL Developer | BI Enthusiast  
Arif Wala, Pakistan  
[LinkedIn](https://www.linkedin.com/in/khurram-naveed-0083851aa/) | ✉️ khurramnaveed4545@gmail.com  

---

 *If you found this project helpful or insightful, please consider giving it a star and following my profile for more data projects.*


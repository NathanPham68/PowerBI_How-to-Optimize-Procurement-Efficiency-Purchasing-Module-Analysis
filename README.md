# [POWER BI] How to Optimize Procurement Efficiency? - Purchasing Module Analysis

<img width="1400" height="784" alt="image" src="https://github.com/user-attachments/assets/7dae7931-5abe-4414-81e3-a6fc8300871f" />

## Table of Contents

1. [📌 Background & Overview](#background--overview)

2. [📂 Dataset Description & Data Structure](#dataset-description--data-structure)

3. [🧠 Design Thinking Process](#design-thinking-process)

4. [📊 Key Insights & Visualizations](#key-insights--visualizations)

5. [🔎 Final Conclusion & Recommendation](#final-conclusion--recommendation)

## I. Introduction

### 📖 What is this project about?

This project focuses on analyzing and understanding the Purchasing Module of the AdventureWorks database — a sample enterprise resource planning (ERP) system for a manufacturing company. The module manages all purchasing operations, including vendor information, purchase orders, purchase order details, and receipts. By exploring this module, we aim to uncover inefficiencies, optimize procurement processes and generate actionable insights that can help a business make informed purchasing decisions.

### ❓ Business Questions:

* Are our back order rates high enough to potentially affect production schedules?

* How efficient are our purchase orders in terms of cost across various vendors and materials?

* Which suppliers consistently meet delivery deadlines and stay within budget?

* Are there any abnormal increases in purchasing costs that require deeper analysis?

* What steps can we take to enhance procurement planning to minimize delays and control costs?

### 👤 Who is this project for?

This dashboard is designed for key stakeholders involved in the purchasing process at AdventureWorks, including:

✔️ Purchasing Manager: To monitor supplier performance, order fulfillment, and spot procurement issues early.

✔️ Purchasing Executive: To track purchasing KPIs, ensure compliance with procurement strategies, and manage day-to-day operations efficiently.

✔️ Board of Directors (BOD): To gain high-level insights into purchasing efficiency and cost control for strategic decision-making.

### 🎯 Project Outcome:

The project delivered valuable insights into order processing, cost management, and vendor performance, pinpointing key areas for improvement to enhance operational efficiency.

Key Results:

  ✔️ Strengthened order management during peak periods to minimize backorder risks.

  ✔️ Streamlined purchase order cost control, maintaining consistency year-round.

  ✔️ Reduced vendor-related risks through contract renegotiations with high-cost suppliers.

  ✔️ Improved product categorization to support better resource allocation and expense monitoring.

Outcome: The initiative empowered data-driven decision-making, leading to greater efficiency, cost optimization, and improved vendor management.

## II. Dataset

📂 Dataset Access - [AdventureWorksDW2019.bak](https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms)

  * The Purchase_OrderDetails table contains 8,845 records
  
  * Format: Pbix

📂 Requirements

  * Visualization Tool - Microsoft PowerBI

📊 Data Structure

The dataset consists of 7 main tables used to build the purchasing dashboard:

<details>
<summary><strong>Table 1: Fact_Purchasing_OrderDetail</strong></summary>

- 📦 **Fact_Purchasing_OrderDetail** – Line-level order details.

| Column Name             | Description                                  |
|-------------------------|----------------------------------------------|
| `OrderQty`              | Quantity ordered                             |
| `ReceivedQty`           | Quantity received                            |
| `RejectedQty`           | Quantity rejected                            |
| `StockedQty`            | Quantity stocked                             |
| `LeadTime_Days`         | Lead time in days                            |
| `DelayDays`             | Number of delay days                         |
| `DueDate`, `OnTime`     | Delivery due date and on-time flag           |
| `IsBackorderedFlag`     | Indicates if the item was backordered        |
| `UnitPrice`             | Unit price of the item                       |
| `PurchaseOrderDetailID` | Line item identifier                         |
| `PurchaseOrderID`, `ProductID` | Foreign keys to orders and products     |

</details>

<details>
<summary><strong>Table 2: Fact_Product_Inventory</strong></summary>

- 🏷️ **Fact_Product_Inventory** – Current inventory levels.

| Column Name           | Description                                |
|------------------------|--------------------------------------------|
| `Quantity`             | Current inventory quantity                 |
| `Below Reorder Flag`   | Indicates if inventory is below reorder level |
| `BelowSafetyStock`     | Indicates stock is below safety threshold  |
| `OutOfStockProducts`   | Out of stock status                        |
| `ProductID`            | Foreign key to product                     |

</details>

<details>
<summary><strong>Table 3: Dim_Product_Product</strong></summary>

- 🧾 **Dim_Product_Product** – Product master data.

| Column Name           | Description                                |
|------------------------|--------------------------------------------|
| `ProductID`            | Unique product identifier                  |
| `Name`, `Class`, `Style` | Product characteristics                   |
| `SafetyStockLevel`     | Safety stock value                         |
| `ReorderPoint`         | Reorder threshold                          |
| `ListPrice`, `StandardCost` | Price and cost info                  |
| `ProductSubcategoryID` | Foreign key to product taxonomy            |

</details>

<details>
<summary><strong>Table 4: Dim_Purchasing_OrderHeader</strong></summary>

- 📄 **Dim_Purchasing_OrderHeader** – Order-level metadata.

| Column Name         | Description                                 |
|----------------------|---------------------------------------------|
| `PurchaseOrderID`    | Header-level order ID                       |
| `OrderDate`, `ShipDate` | Order creation and shipping date         |
| `VendorID`           | Foreign key to vendor                       |
| `TotalDue`, `Freight`, `SubTotal` | Order-level cost details      |

</details>

<details>
<summary><strong>Table 5: Dim_Purchasing_Vendor</strong></summary>

- 🧑‍💼 **Dim_Purchasing_Vendor** – Vendor master data.

| Column Name             | Description                            |
|--------------------------|----------------------------------------|
| `VendorID`               | Unique vendor ID                       |
| `Name`, `AccountNumber`  | Vendor info                            |
| `PreferredVendorLabel`   | Whether vendor is preferred            |
| `CreditRating`           | Vendor's credit rating                 |

</details>

<details>
<summary><strong>Table 6: Dim_Purchasing_ProductVendor</strong></summary>

- 🔗 **Dim_Purchasing_ProductVendor** – Product-vendor mapping.

| Column Name           | Description                              |
|------------------------|------------------------------------------|
| `ProductID`            | Linked product                           |
| `VendorID`             | Linked vendor                            |
| `MinOrderQty`, `MaxOrderQty` | Order quantity boundaries        |
| `StandardPrice`        | Standard unit cost                       |
| `AverageLeadTime`      | Vendor delivery time in days             |

</details>

<details>
<summary><strong>Table 7: Dim_Product_ProductTaxonomy</strong></summary>

- 🧱 **Dim_Product_ProductTaxonomy** – Product categories.

| Column Name           | Description                                |
|------------------------|--------------------------------------------|
| `ProductID`            | Product reference                          |
| `Category`, `Subcategory` | Product hierarchy                      |

</details>

<details>
<summary><strong>Table 8: Dim_Product_ProductTable</strong></summary>

- 🗂️ **Dim_Product_ProductTable** – Product category and hierarchy.

| Column Name             | Description                         |
|--------------------------|-------------------------------------|
| `ProductID`              | Linked product                      |
| `ProductCategoryID`      | Category reference                  |
| `ProductSubcategoryID`   | Subcategory reference               |
| `Category`               | Product category name               |
| `Subcategory`            | Product subcategory name            |

</details>

## III. Design Thinking Method
To approach this project effectively, we applied the Design Thinking methodology, which ensures a user-centric, iterative, and problem-solving mindset.

### Step 1 – Empathize

We studied the end-users of the purchasing process, such as procurement officers, warehouse staff, and finance teams. By understanding their pain points — like tracking supplier performance, managing purchase order accuracy, and ensuring timely deliveries — we could better define project goals.

### Step 2 – Define

* Based on our research, we defined key challenges:
* Delays in purchase order approvals.
* Difficulty in monitoring vendor reliability.
* Complex tracking of received goods vs. ordered quantities.
* Potential duplication or inconsistency in supplier records.

### Step 3 – Ideate

We brainstormed potential solutions, including:
* Developing dashboards to monitor supplier performance.
* Automating alerts for delayed deliveries.
* Implementing visualizations to compare ordered vs. received quantities.
* Enhancing data integrity with duplicate checks.

Step 4 – Prototype

We designed data models and sample reports using the AdventureWorks Purchasing tables:
* Vendor: Stores supplier details.
* PurchaseOrderHeader: Holds summary info of each PO.
* PurchaseOrderDetail: Contains line items.
* ShipMethod: Tracks shipment methods.
* ProductVendor: Connects products to vendors.
* VendorContact: Manages vendor contact information.

Step 5 – Review

We reviewed our prototype with stakeholders to ensure it addressed the identified issues and provided clear, actionable insights for the procurement team.

## IV. Visualization
### 1. Entity Relationship Diagram Model

![image](https://github.com/user-attachments/assets/705a4d22-ed11-49cd-b754-148ee90a7197)

<details>
<summary><strong>Data Relationships</strong></summary>

| **From Table**                  | **To Table**                     | **Join Key**                | **Relationship Type**                                      |
|--------------------------------|----------------------------------|-----------------------------|------------------------------------------------------------|
| `Fact_Purchasing_OrderDetail`  | `Dim_Purchasing_OrderHeader`     | `PurchaseOrderID`           | Many-to-One (many order lines per order header)            |
| `Fact_Purchasing_OrderDetail`  | `Dim_Product_Product`            | `ProductID`                 | Many-to-One (many order lines for one product)             |
| `Fact_Purchasing_OrderDetail`  | `Dim_Order_Date`                 | `DueDate` / `ModifiedDate`  | Many-to-One (orders map to one date)                       |
| `Dim_Purchasing_OrderHeader`   | `Dim_Purchasing_Vendor`          | `VendorID`                  | Many-to-One (multiple orders per vendor)                   |
| `Dim_Purchasing_ProductVendor` | `Dim_Purchasing_Vendor`          | `VendorID`                  | Many-to-One (vendor supplies many products)                |
| `Dim_Purchasing_ProductVendor` | `Dim_Product_Product`            | `ProductID`                 | Many-to-One (vendor offers multiple products)              |
| `Dim_Product_Product`          | `Dim_Product_ProductTaxonomy`    | `ProductSubcategoryID`      | Many-to-One (each product belongs to one subcategory)      |
| `Fact_Product_Inventory`       | `Dim_Product_Product`            | `ProductID`                 | Many-to-One (each inventory record linked to a product)    |

</details>

### 2. Summary

![image](https://github.com/user-attachments/assets/d1b940bc-d942-4824-9e72-b118a983f754)

### 3. RejectRate

![image](https://github.com/user-attachments/assets/51ac75fe-96fc-47de-a69c-9e3992eea251)

### 4. Database

![image](https://github.com/user-attachments/assets/78b97da7-eee6-4e20-8c6c-f82622658c99)

### 5. ScrapReason

![image](https://github.com/user-attachments/assets/158d2e4a-0704-4870-8927-89d2dd1713ee)

## V. Insights
Key insights from the analysis include:
* A small number of vendors account for the majority of spending.
* Delayed shipments are concentrated with specific vendors and shipment methods.
* Certain products consistently have higher receipt discrepancies.
* High frequency of low-value orders, suggesting opportunities for order consolidation.

## VI. Recommendations
Based on the findings, we recommend:
* Negotiating better terms with top vendors and phasing out underperforming suppliers.
* Automating approval workflows to reduce purchase order delays.
* Consolidating frequent small orders to optimize shipping costs.
* Implementing stricter checks and balances to improve data accuracy in vendor records.

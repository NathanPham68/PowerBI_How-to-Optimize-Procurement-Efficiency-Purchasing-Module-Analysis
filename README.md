# [POWER BI] How to Optimize Procurement Efficiency? - Purchasing Module Analysis

<img width="1400" height="784" alt="image" src="https://github.com/user-attachments/assets/7dae7931-5abe-4414-81e3-a6fc8300871f" />

## Table of Contents

1. [📌 Introduction](#Introduction)

2. [📂 Dataset](#dataset)

3. [🧠 Design Thinking Method](#design-thinking-method)

4. [📊 Visualizations](#visualizations)

5. [🔎 Insights & Recommendations](#Insights-&-recommendation)

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

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b4cae5d9-2c99-4ba6-b1a7-1091e34eae87" />

### ✅ Step 1 – Empathize

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fb0471a2-3c74-42f0-8020-53cf3a22f5fb" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cbc1a848-18eb-4fd1-b695-a6521d081fde" />

The Purchasing department faced multiple challenges in managing procurement effectively. Stakeholders had to open many files to gather data, information was not real-time, and there was no clear reporting structure to track key KPIs. This made it difficult to monitor vendor performance, order handling, and purchasing costs.

To address these pain points, stakeholders approached the Data Analyst team with a request for a dashboard that could centralize procurement data, display key metrics, and provide insights into operational trends.

* Executives would use it daily to check if strategic KPIs were met.

* Managers would rely on it for weekly/monthly meetings to identify root causes of issues.

* Operational staff would track inventory readiness and supplier performance.

This set the foundation for a data-driven approach to procurement improvement.

### ✅ Step 2 – Define

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8fa09d30-65b5-417b-89c2-df53215671cd" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8eac1205-12d0-4234-b5b2-f4b70535cfdf" />

From stakeholder discussions, two North Star Metrics were defined:

* Back Order Rate – A measure of how many orders were not fulfilled on time.

Success Indicator: A decreasing back order rate, ensuring smoother production and reduced costs from emergency orders.

* Average Purchase Order Cost – A measure of cost efficiency in procurement.

Success Indicator: Optimized purchasing costs, ensuring the right quantity and quality at a reasonable price.

These metrics captured the most critical aspects of procurement: delivery performance and cost effectiveness.

### ✅ Step 3 – Ideate

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/494015ca-57c0-455b-8e6c-bbf4a2181120" />

The Purchasing team brainstormed perspectives (POVs) to guide dashboard design:

1. Supplier Performance – Who consistently delivers on time and within budget?

2. Order Fulfillment – How are orders progressing, and are back orders under control?

3. Cost Efficiency – Are we buying at the right cost compared to benchmarks?

4. Inventory Readiness – Do we have sufficient stock to prevent production delays?

Ideas were structured into layers of analysis:

* Layer 0 (Scorecards): High-level KPIs for quick checks.

* Layer 1 (Breakdowns): Metrics by vendor, category, or time period.

* Layer 2 (Deep-Dives): Multi-dimensional views (e.g., cost by vendor × product) to identify root causes.

### ✅ Step 4 – Prototype

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/d2015a0c-52d5-4758-899f-b5e831765858" />

The first prototype of the Procurement Performance Dashboard was developed with:

* Scorecards for Back Order Rate, On-Time Delivery %, Average PO Cost, and Stockout Risk %.

* Trend charts and filters to track performance over time and across vendors.

* Breakdown tables by supplier, product category, and time for deeper analysis.

* Color-coded status indicators (green/yellow/red) for quick decision-making.

This allowed different stakeholders to use the dashboard according to their needs: executives for quick checks, managers for root-cause analysis, and staff for operational monitoring.

### ✅ Step 5 – Review

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e2240e7f-33c7-4588-a7ae-67f9eea50056" />

After rollout, the dashboard underwent review sessions with stakeholders:

* Executives confirmed it provided real-time visibility into procurement KPIs.

* Managers used it effectively in meetings to diagnose issues and validate trends.

* Staff found it helpful in detecting supplier delays and potential stockouts earlier.

Key outcomes of the review:

* Positive Impact: Faster identification of vendor risks and cost anomalies, improved alignment between Purchasing and Production.

* Improvement Areas: Need for demand forecast accuracy and supplier benchmarking against market prices.

* Next Steps: Add predictive analytics, refine filters, and expand supplier evaluation criteria (e.g., quality, responsiveness).

### ✅ Conclusion

Through the Design Thinking process, the project successfully transformed fragmented procurement data into a centralized, actionable dashboard. This empowered the organization to make data-driven decisions, resulting in:

* Reduced back order risks

* Optimized purchasing costs

* Stronger vendor management

* Improved operational efficiency

The Procurement Performance Dashboard became a strategic tool for enhancing both short-term operations and long-term supply chain resilience.

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

<img width="1436" height="825" alt="image" src="https://github.com/user-attachments/assets/40ca97bf-bcbc-4c03-a456-ceb2b2e480ed" />

* Back Orders & Late Deliveries: Spikes up to 50%, revealing supply bottlenecks and poor demand forecasting.

* Category Insights: Clothing & Components dominate; demand follows seasonal cycles that can be predicted.

* Cost Efficiency: Average PO cost shows high volatility, suggesting inconsistent supplier pricing and order planning.

* Quality Issues: Rejection rates average 3%, but peak near 30%, pointing to supplier quality gaps.

* Fulfillment & Lead Time: Overall strong (90–100% fulfillment, 9 days ship time) but with noticeable dips in continuity.

### 3. RejectRate

<img width="1436" height="826" alt="image" src="https://github.com/user-attachments/assets/98598126-9418-4124-9b72-5e84786e8491" />

* Total Purchase Spend: $63.8M with an average PO cost of $7.2K.

* On-Time Fulfillment Rate: Excellent at 99.9%, ensuring supply continuity.

* Back Order Rate: 9.4%, still a concern that signals demand-supply mismatch.

* Rejections: Concentrated among a few vendors (e.g., Supersales Inc. tops with 6.4K rejects).

* Product-Level Issues: High rejection in components (Decals, Crankarms, Pedals) → highlights potential quality control gaps.

* Credit Rating: Majority of rejected orders come from suppliers with rating “1”, showing volume doesn’t always equal reliability.

### 4. Product

<img width="1436" height="827" alt="image" src="https://github.com/user-attachments/assets/15bd38d2-f1fa-4914-9338-a649bc2cb832" />

* Purchase volume peaked in early 2014, then dropped; avg. price stable → consistent supplier pricing.

* Inventory turnover spiked in Jul 2014 (17K) but weak in prior years → risk of overstocking.

* Critical stockouts: Hex Nuts, Hitch Racks, Gloves → urgent reorder needed.

* High spend concentration on bike frames → strategic supplier dependency.

* Backorder rate high in Components (15.7%) → supplier reliability issue.

### 5. Vendor

<img width="1436" height="825" alt="image" src="https://github.com/user-attachments/assets/4836b95f-0da6-47da-aa1d-c9cb84b986ae" />

* Superior Bicycles (4.6M) & Professional Athletic Consultants (3.1M) drive most cost variance.

* High backorders with Superior Bicycles (20%), Jackson Authority & Vision Cycles (>17%) = supply risk.

* 90% of POs are with preferred vendors → good alignment, but 10% non-preferred adds risk.

* Victory Bikes (high spend, Below Avg rating) → underperforming; Sport Fan Co. shows strong potential.

### 6. Database

<img width="1436" height="825" alt="image" src="https://github.com/user-attachments/assets/1e7c1694-c1f3-450f-b22f-9dbb4badccc9" />

## V. Insights & Recommendations

| **Aspect**                         | **Insight**                                                                                                                                                                                                                                       | **Recommendation**                                                                                                                                                                              |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Order & PO Performance**         | - **Peak demand in May–June** leads to pressure on operations, with **Late Orders & Back Orders** peaking in June–July (\~9–10%). <br> - After August, fulfillment stabilizes.                                                                    | - Strengthen **capacity planning** for peak seasons. <br> - Apply tighter tracking for **at-risk POs** to avoid backlog.                                                                        |
| **PO Cost & Trends**               | - **PO costs fluctuate**, highest in March, dropping by October. <br> - Year-end average stabilizes around **\$7.0K–\$7.2K**.                                                                                                                     | - Maintain strict **cost controls** at year-end. <br> - Proactively **adjust procurement strategy** to offset sudden cost spikes.                                                               |
| **Vendor Performance & Risks**     | - Suppliers like **Supersales Inc.** show **6.4K rejects** (highest). <br> - Vendors with **Credit Rating = 1** generate largest rejection volumes. <br> - Backorders concentrated with **Chicago City (21.6%)** and **Superior Bicycles (20%)**. | - Implement stronger **supplier scorecards & audits**. <br> - **Renegotiate terms** or reassess suppliers with high backorders/rejections. <br> - Focus on improving **delivery reliability**.  |
| **Product & Inventory Management** | - **Blank category (\$22M)** indicates incomplete product classification, limiting spend visibility. <br> - **Pedals, Tires & Tubes** are major spend drivers. <br> - High reject SKUs include **Decals, Pedals, Crankarms**.                     | - Enhance **product categorization** for accurate spend tracking. <br> - Prioritize **high-spend categories** in procurement planning. <br> - Apply stricter **QC measures** on high-risk SKUs. |
| **Logistics & Transportation**     | - **Cargo Transport** is the weakest logistics partner, accounting for **29K rejected shipments**.                                                                                                                                                | - Reassess **logistics providers** with high rejection rates. <br> - Explore alternative transport options to reduce risks.                                                                     |



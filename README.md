# [POWER BI] How to Optimize Procurement Efficiency? - Purchasing Module Analysis

## I. Introduction

This project focuses on analyzing and understanding the Purchasing Module of the AdventureWorks database — a sample enterprise resource planning (ERP) system for a manufacturing company. The module manages all purchasing operations, including vendor information, purchase orders, purchase order details, and receipts. By exploring this module, we aim to uncover inefficiencies, optimize procurement processes, and generate actionable insights that can help a business make informed purchasing decisions.

## II. Dataset

📂 Dataset Access - [AdventureWorksDW2019.bak](https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms)

📂 Requirements
* Visualization Tool - Microsoft PowerBI

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

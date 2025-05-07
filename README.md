# Purchasing-Performance-Cost-Optimization-for-Manufacturing-at-AdventureWorks-Power-BI

![Image](https://github.com/user-attachments/assets/3cbe74ea-1dbf-43c0-a860-fd5e16151c35)

**Author:** Nguyễn Hoàng Đỗ Uyên

**Date:** May 2025

**Tools Used:** BI

## Table of Contents
1. [📌 Background & Overview](#background--overview)
2. [📂 Dataset Description & Data Structure](#dataset-description--data-structure)
3. [🧠 Design Thinking Process](#design-thinking-process)
4. [📊 Key Insights & Visualizations](#key-insights--visualizations)
5. [🔎 Final Conclusion & Recommendation](#final-conclusion--recommendation)

---

**Objective:**

**📖 What is this project about?**

This project analyzes purchasing activities at **AdventureWorks** to support better operational decisions. The Power BI dashboard focuses on:

- **Purchasing Performance**: Monitoring back order rates to ensure timely and sufficient supply for manufacturing needs.  
- **Cost Optimization**: Evaluating average purchase order costs to identify savings opportunities and improve procurement efficiency.


**👤 Who is this project for?**

This dashboard is designed for key stakeholders involved in the purchasing process at **AdventureWorks**, including:

- **Purchasing Manager**: To monitor supplier performance, order fulfillment, and spot procurement issues early.  
- **Purchasing Executive**: To track purchasing KPIs, ensure compliance with procurement strategies, and manage day-to-day operations efficiently.  
- **Board of Directors (BOD)**: To gain high-level insights into purchasing efficiency and cost control for strategic decision-making.

**❓Business Questions:**

- Are we experiencing high back order rates that may impact production timelines?  
- How cost-effective are our purchase orders across different vendors and materials?  
- Which vendors are consistently delivering on time and within budget?  
- Are there any unusual spikes in purchasing cost that need further investigation?  
- How can we improve procurement planning to reduce delays and optimize costs?

## 📂 Dataset Description & Data Structure

### **📌 Data Source** 
- **Source**: Kaggle - Dataset of AdventureWorks
- **Size**: The **Purchase_OrderDetails** table contains **8,845** records.  
- **Format**: Pbix

### 📊 **Data Structure & Relationships**  

#### 1️⃣ **Tables Used:**  
## 1️⃣ Tables Used:
The dataset consists of **7 main tables** used to build the purchasing dashboard:

- 📦 **Fact_Purchasing_OrderDetail** – Line-level order details.

<details>
<summary><strong>Table 1: Fact_Purchasing_OrderDetail</strong></summary>

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

- 🏷️ **Fact_Product_Inventory** – Current inventory levels.

<details>
<summary><strong>Table 2: Fact_Product_Inventory</strong></summary>

| Column Name           | Description                                |
|------------------------|--------------------------------------------|
| `Quantity`             | Current inventory quantity                 |
| `Below Reorder Flag`   | Indicates if inventory is below reorder level |
| `BelowSafetyStock`     | Indicates stock is below safety threshold  |
| `OutOfStockProducts`   | Out of stock status                        |
| `ProductID`            | Foreign key to product                     |

</details>

- 🧾 **Dim_Product_Product** – Product master data.

<details>
<summary><strong>Table 3: Dim_Product_Product</strong></summary>

| Column Name           | Description                                |
|------------------------|--------------------------------------------|
| `ProductID`            | Unique product identifier                  |
| `Name`, `Class`, `Style` | Product characteristics                   |
| `SafetyStockLevel`     | Safety stock value                         |
| `ReorderPoint`         | Reorder threshold                          |
| `ListPrice`, `StandardCost` | Price and cost info                  |
| `ProductSubcategoryID` | Foreign key to product taxonomy            |

</details>

- 📄 **Dim_Purchasing_OrderHeader** – Order-level metadata.

<details>
<summary><strong>Table 4: Dim_Purchasing_OrderHeader</strong></summary>

| Column Name         | Description                                 |
|----------------------|---------------------------------------------|
| `PurchaseOrderID`    | Header-level order ID                       |
| `OrderDate`, `ShipDate` | Order creation and shipping date         |
| `VendorID`           | Foreign key to vendor                       |
| `TotalDue`, `Freight`, `SubTotal` | Order-level cost details      |

</details>

- 🧑‍💼 **Dim_Purchasing_Vendor** – Vendor master data.

<details>
<summary><strong>Table 5: Dim_Purchasing_Vendor</strong></summary>

| Column Name             | Description                            |
|--------------------------|----------------------------------------|
| `VendorID`               | Unique vendor ID                       |
| `Name`, `AccountNumber`  | Vendor info                            |
| `PreferredVendorLabel`   | Whether vendor is preferred            |
| `CreditRating`           | Vendor's credit rating                 |

</details>

- 🔗 **Dim_Purchasing_ProductVendor** – Product-vendor mapping.

<details>
<summary><strong>Table 6: Dim_Purchasing_ProductVendor</strong></summary>

| Column Name           | Description                              |
|------------------------|------------------------------------------|
| `ProductID`            | Linked product                           |
| `VendorID`             | Linked vendor                            |
| `MinOrderQty`, `MaxOrderQty` | Order quantity boundaries        |
| `StandardPrice`        | Standard unit cost                       |
| `AverageLeadTime`      | Vendor delivery time in days             |

</details>

- 🧱 **Dim_Product_ProductTaxonomy** – Product categories.

<details>
<summary><strong>Table 7: Dim_Product_ProductTaxonomy</strong></summary>

| Column Name           | Description                                |
|------------------------|--------------------------------------------|
| `ProductID`            | Product reference                          |
| `Category`, `Subcategory` | Product hierarchy                      |

</details>

- 🗂️ **Dim_Product_ProductTable** – Product category and hierarchy.

<details>
<summary><strong>Table 8: Dim_Product_ProductTable</strong></summary>

| Column Name             | Description                         |
|--------------------------|-------------------------------------|
| `ProductID`              | Linked product                      |
| `ProductCategoryID`      | Category reference                  |
| `ProductSubcategoryID`   | Subcategory reference               |
| `Category`               | Product category name               |
| `Subcategory`            | Product subcategory name            |

</details>

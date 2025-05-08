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

#### 2️⃣ Data Relationships:

![Image](https://github.com/user-attachments/assets/5d697c87-7628-4d70-b1d4-3163e44ae1fc)

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

## 🧠 Design Thinking Process

### 1️⃣ Empathize

![Image](https://github.com/user-attachments/assets/e69224c7-8272-45b7-9341-2e73aee0be8b)

![Image](https://github.com/user-attachments/assets/dfd3a807-480c-4382-b57d-71744fdf4e92)

![Image](https://github.com/user-attachments/assets/92e0d009-b0fe-441d-9901-86ece9a87ca6)

### 2️⃣ Define point of view 

![Image](https://github.com/user-attachments/assets/9c8b2fd9-4bf6-47cc-878f-802d5f67eb66)

![Image](https://github.com/user-attachments/assets/7328ee67-4acf-4094-9c7e-ce2c322e54fe)

### 3️⃣ Ideate

![Image](https://github.com/user-attachments/assets/a1596b12-a5c2-4008-95fd-b5f6d80ed7f8)

![Image](https://github.com/user-attachments/assets/a2c1aa14-8610-4927-b839-19261dc8ee31)

### 4️⃣ Prototype and review

This part is in the dashboard

## 📊 Key Insights & Visualizations

### 🔍 Dashboard Preview

### I. Executive Summary

![Image](https://github.com/user-attachments/assets/e35ac020-48b2-4f37-b682-6a92962205b9)

### 📌 Key Findings:

#### **1. Total Order, Late Orders and Back Order Rate (%)**

- Total orders peaked in **May–June** (456 orders).
- Both **Late Orders** and **Back Order Rate** reached their highest in **June–July (~10.5%)**.
- Steady decline in these two metrics after August.

-> Mid-year appears to be a **peak demand period**, stressing the fulfillment system. However, performance **improved significantly in Q4**, indicating better operational control.


#### **2. AVG Purchase Order Cost Trend**

- Average PO cost fluctuated between **$6.3K and $7.8K**.
- Peaked in **March**, dropped sharply by **October**.
- The Last Month (LM) line remains stable around **$7.0K–$7.2K**.

-> PO costs show **seasonal fluctuations**, suggesting **stronger cost control or supplier negotiations** toward the end of the year.


#### **3. Cumulative PO Cost and Cumulative PO Count**

- Cumulative PO Cost steadily increased to **$64M by August**, followed by a sharp drop.
- This year’s PO count is significantly lower compared to last year.

-> Indicates a **batch purchasing strategy** or increased **PO efficiency**, reducing frequency while maintaining volume.


#### **4. Top 3 Vendor Pricing vs Market Average Over Time**

- **Chicago City** consistently charges higher than **market average** (~35.5 vs 34.3–34.7).
- **SUPERSALES** and **Custom Framing** offer **lower-than-market** pricing with consistent trends.

-> Heavy reliance on **higher-cost vendors** may impact purchasing efficiency unless there’s a **strategic reason** (e.g. quality, lead time).


#### **5. Total PO by Month and Category**

- PO volume peaked in **August**, dropped drastically afterward.
- The **(Blank)** category dominates, while other categories like Accessories and Components are minimal.

-> Product classification is likely **incomplete or inconsistent**, which can **limit granular tracking and analysis** by category.


#### **6. Total Purchase Spend by Sub-Category**

- The sub-category **"(Blank)"** represents the **highest total purchase spend ($22M)**, dwarfing all other defined categories.
- Categories like **Pedals and Tires and Tubes** show substantial spending **($13M each)**, others like **Jerseys, Shorts, Vests, and Bib-Shorts** have considerably **lower spending ($1M or less).
-> Spending heavily concentrated in **Pedals and Tires**, suggesting a focus that warrants further demand/sourcing review. Large "(Blank)" spending obscures understanding of where funds are truly allocated.



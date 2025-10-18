# 💼 Lab 4 — Adventure Works Sales Analysis Dashboard

### 📁 Data Source  
**Source:** [AdventureWorks2022.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2022.bak)  
**Connection Mode:** DirectQuery (Real-time connection to SQL Server)

---

## 🔧 Data Preparation & Connection

**1. Connect to Data Source**  
- Open Power BI Desktop → *Get Data* → *SQL Server Database*.  
- Connect to SQL Server instance containing the restored **AdventureWorks2022** database.  
- Choose **DirectQuery Mode** for live connection.

**2. Imported Tables**
- `vw_DimProducts`  
- `vw_DimSalesPersons`  
- `vw_DimShipMethods`  
- `vw_DimStatuses`  
- `vw_DimTerritories`  
- `vw_FactOrderDetails`

**3. Relationship Setup**
- Created relationships using key fields:  
  `ProductKey`, `SalesPersonKey`, `TerritoryKey`, `ShipMethodKey`, `StatusKey`  
- Ensured **1-to-many** relationships between dimension and fact tables.

---

## 📅 Dates Table (DAX)
A **Dates table** was created using DAX for time intelligence calculations:

```DAX
Dates =
ADDCOLUMNS (
    CALENDAR (DATE(2010,1,1), DATE(2015,12,31)),
    "Year", YEAR([Date]),
    "MonthNumber", MONTH([Date]),
    "MonthName", FORMAT([Date], "MMMM"),
    "Quarter", "Q" & FORMAT([Date], "Q")
)
```

Then related `[OrderDate]` in `vw_FactOrderDetails` with `[Date]` in `Dates`.

---

## 📏 Measures Created (DAX)

| Measure | Description |
|----------|--------------|
| **No. Orders** | Count of distinct Sales Order Numbers |
| **Total Subtotal** | Sum of SubTotal |
| **Total Tax** | Sum of TaxAmt |
| **Total Freight** | Sum of Freight |
| **Total Due** | Sum of TotalDue |
| **Total Quantity** | Sum of OrderQty |
| **Sales Growth %** | Year-over-year growth in Total Due |

**Sales Growth % Formula:**
```DAX
SalesGrowth% =
VAR CurrentSales = [TotalDue]
VAR PreviousSales = CALCULATE([TotalDue], DATEADD(Dates[Date], -1, YEAR))
RETURN DIVIDE(CurrentSales - PreviousSales, PreviousSales)
```

---

## 📊 Dashboard Structure (3 Pages)

### **Page 1: Sales Overview**
**Visuals:**
- KPI Cards:
  - Total Due = **123M**
  - Total Subtotal = **110M**
  - Total Tax = **10M**
  - Total Freight = **3M**
  - Total Quantity = **275K**
  - No. Orders = **31K**
- **Line Chart:** Sales Growth % by Year  
- **Scatter Chart:** Total Due vs Total Tax (Correlation Analysis)  
- Navigation button → *Sales Analysis*

---

### **Page 2: Sales Analysis**
**Visuals:**
- **Decomposition Tree:** Total Due → Territory → Product Category → Product Name  
- **Top 10 Salespersons** by Total Due  
- **Top 5 Products:** Showing Sales Growth % and Total Due  
- **Q&A Visual:** Example queries — “Top categories by total tax”, “Top colors by total freight”

**Insights:**
- *Mountain-200* products dominate sales.  
- *Linda C. Mitchell* and *Jillian Carson* are the top sales performers.  

---

### **Page 3: Sales Regions**
**Visuals:**
- **Map:** Sales by Territory (North America, Europe, Pacific)  
- **Pie Chart:** Sales by Group  
  - North America: **89.23M**  
  - Europe: **22.17M**  
  - Pacific: **11.81M**  
- **Bar Chart:** Sales by Category  
  - Bikes: **75.6M**  
  - Components: **10.9M**  
  - Clothing: **1.8M**  
  - Accessories: **0.87M**

---

## 🏷️ Bookmarks & Navigation (Bonus)
Created bookmarks to toggle between:
- **Chart 1:** Sales by Territory (Pie Chart)  
- **Chart 2:** Sales Growth % by Year (Bar Chart)  
Using buttons for smooth navigation and interactivity.

---

## 🔍 Q&A Visual Example
Enabled the **Q&A** feature for natural language insights, e.g.:
- “Top 5 products by TotalDue”  
- “Compare Total Tax by Category”

---

## 🎯 Drill Through (Bonus)
A **Drill Through page** was created for detailed *Order and Customer Insights*, accessible when clicking a salesperson or territory.

---

## 🎨 Creative Design
- Dark professional theme  
- Clean layout and alignment  
- Consistent use of colors and spacing  
- Navigation buttons between pages  
- Custom tooltips for detailed data (product, region, salesperson)  
- Interactive slicers: Year, Product Category, Territory, Salesperson  

---

## 🧠 Key Insights
1. **Total Sales:** $123M across all territories.  
2. **Strongest Region:** North America (≈70% of total).  
3. **Best Category:** Bikes (≈61% of revenue).  
4. **Top Salespersons:** Linda C. Mitchell & Jillian Carson.  
5. **Sales Growth:** Significant improvement post-2012.  
6. **Tax & Freight:** Positive correlation with order volume.

---

## 📎 Files
- `AdventureWorks2022.bak` — SQL Database Source  
- `Lab04.pbix` — Power BI Project File  
- `Lab04.pdf` — Exported Report  

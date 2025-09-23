# 📊 Superstore Sales Analysis  
*From Flat File to Star Schema — Power BI project demonstrating ETL, modeling, and visualization*

---

## 📌 Project Overview  
This project analyzes the **Superstore** sales dataset using **Power BI**. It demonstrates the full analytical workflow:
- Data ingestion & cleaning (Power Query)  
- Feature engineering (date parts, week-of-month)  
- Splitting a flat file into a **star schema**  
- Establishing relationships and validating the model  
- Building interactive dashboards and extracting business insights  

---

## 🗂 Dataset Summary  
- **Source**: Single flat file (orders, product, customer, shipping, region, sales columns).  
- **Goal**: Normalize to a star schema (fact + dimensions) for performant, accurate reporting.  

---

## 🔄 Step-by-step: Data Preparation & Modeling

### 1. Import
- Load CSV/Excel flat file into Power BI.  
- Use **Transform data** to open Power Query Editor.  

### 2. Data cleaning (Power Query)
- Convert **Kenyan date format (dd/mm/yyyy)** to **U.S. format (mm/dd/yyyy)** using *Using Locale*.  
- Change and validate data types: IDs (Text), Dates (Date), Numbers (Decimal/Whole Number).  
- Handle missing values: remove blanks or replace nulls.  
- Trim & clean text fields.  
- Remove duplicates for dimension tables.  

### 3. Feature engineering (date parts)
From `OrderDate` in the Orders table:  
- Extract **Year, MonthNumber, MonthName, DayName**.  
- Create **Week of Month** (capped at 5):  
  - Custom column formula:  
    ```powerquery
    if [Week of Month] > 5 then 5 else [Week of Month]
    ```  

### 4. Split flat file into tables
Using **Reference** queries in Power Query:  
- **Products** → ProductID, ProductName, Category, UnitPrice  
- **Customers** → CustomerID, CustomerName, Region, City, State, Segment  
- **Orders** → OrderID, OrderDate, ShipDate, derived date parts  
- **Sales (Fact)** → SaleID, OrderID, ProductID, CustomerID, Quantity, UnitPrice, TotalAmount, Profit  

### 5. Load & build relationships
- Load all tables into the model.  
- Relationships (star schema):  
  - Products[ProductID] → Sales[ProductID]  
  - Customers[CustomerID] → Sales[CustomerID]  
  - Orders[OrderID] → Sales[OrderID]  
- Validate one-to-many cardinality and referential integrity.  

### 6. Month sorting & order
- Create **MonthNumber** column.  
- Sort MonthName by MonthNumber.  
- Sort DayName by DayNumber for proper ordering.  

### 7. Measures & visuals
- Create KPIs: Total Sales, Total Profit, Avg Order Value.  
- Use line charts, bar charts, maps, and cards for dashboards.  

---

## 🛠 ERD & Dashboards

### ERDs
- **Initial flat file ERD**  
![ERD Final](https://github.com/evans-njau/Sale/blob/master/flat%20file%20fields.png)  

- **Star schema ERD**  
![ERD Final](https://github.com/evans-njau/Sale/blob/master/Tables%20relationships.png)  

---

### Dashboards
- **General Overview**  
![General Overview](https://github.com/evans-njau/Sale/blob/master/Screenshot%20(52).png)  

- **Regional Overview**  
![Regional Overview](https://github.com/evans-njau/Sale/blob/master/Screenshot%20(53).png)  

- **Insights Dashboard**  
![Insights](https://github.com/evans-njau/Sale/blob/master/Screenshot%20(54).png)  

---

## 🔑 Key Insights
- 📈 **Seasonality:** March consistently shows the highest spike in sales (spring effect).  
- 💻 **Category Performance:** Technology is the top-performing category; Office Supplies underperform. Technology shows consistent yearly spikes.  
- 💰 **Profit vs Revenue:** Technology generated the highest profit over four years; Furniture produced the least revenue.  
- 🚚 **Ship Mode:** Average profit per ship mode is nearly equal (First Class leads at ~31%). Revenue per ship mode is irregular overall, but all modes spike in March.  
- 🗺️ **Geography:** California, New York, and Washington generated the highest profits. Central & Eastern regions spiked in the 4th week of the month, while Southern & Western declined.  

---

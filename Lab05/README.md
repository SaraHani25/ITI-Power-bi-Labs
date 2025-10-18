# ✈️ Power BI Lab 5 — Airline Delay Causes Analysis Dashboard

### 📁 Data Source  
**Dataset:** [Airline Delay Causes](https://www.kaggle.com/datasets/giovamata/airlinedelaycauses)  
**Connection Mode:** Import Mode  
**Tool Used:** Power BI Desktop  

---

## 🧩 Data Preparation & Modeling

### 1️⃣ Connecting to the Data
- Imported the dataset from Kaggle into Power BI.
- Verified and corrected data types (e.g., Date → Date, Delay Columns → Decimal Number).
- Cleaned null values and handled missing delay durations.
- Ensured all numeric fields were converted to *Whole Number* or *Decimal Number* types for accurate aggregation.

---

### 2️⃣ Creating the **Dates Table (DAX)**
A custom **Calendar Table** was created for time-based analysis using DAX:

```DAX
Dates =
ADDCOLUMNS (
    CALENDAR (MIN('Airline Delay'[FL_DATE]), MAX('Airline Delay'[FL_DATE])),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMM"),
    "MonthNumber", MONTH([Date]),
    "Day", DAY([Date]),
    "Quarter", "Q" & FORMAT([Date], "Q"),
    "Weekday", FORMAT([Date], "dddd")
)
```

Then, relationships were built between:
- `Dates[Date]` ↔ `Airline Delay[FL_DATE]`

---

### 3️⃣ DAX Measures Created

| Measure | Formula (Simplified) | Description |
|----------|----------------------|--------------|
| **Total Flights** | `COUNTROWS('Airline Delay')` | Total flight count |
| **Delayed Flights** | `CALCULATE(COUNTROWS('Airline Delay'), 'Airline Delay'[DepDelay] > 0)` | Number of delayed flights |
| **Cancelled Flights** | `COUNTROWS(FILTER('Airline Delay', 'Airline Delay'[Cancelled] = 1))` | Total cancelled flights |
| **Diverted Flights** | `COUNTROWS(FILTER('Airline Delay', 'Airline Delay'[Diverted] = 1))` | Total diverted flights |
| **Delay %** | `DIVIDE([Delayed Flights], [Total Flights])` | % of flights delayed |
| **Average DepDelay** | `AVERAGE('Airline Delay'[DepDelay])` | Average departure delay in minutes |
| **Average ArrDelay** | `AVERAGE('Airline Delay'[ArrDelay])` | Average arrival delay in minutes |
| **Total Delay Causes** | `SUM('Airline Delay'[CarrierDelay] + 'Airline Delay'[WeatherDelay] + 'Airline Delay'[NASDelay] + 'Airline Delay'[SecurityDelay] + 'Airline Delay'[LateAircraftDelay])` | Combined total of all delay causes |

---

## 📊 Dashboard Overview (3 Pages)

### 🟦 **Page 1 — Flight Overview**
**Visuals & KPIs:**
- **Cards:**  
  - Total Flights → **2M**  
  - Delayed Flights → **1.94M**  
  - Cancelled Flights → **633K**  
  - Diverted Flights → **7.7K**  
  - Average Departure Delay → **43.19 min**  
- **Charts:**
  - Total Flights by Month (line chart showing seasonal patterns)
  - Flights Distribution by Day Period (Morning, Afternoon, Evening, Night)
  - Flights by City (Top performing regions)

**Insights:**
- Over **89%** of flights were delayed.  
- **Afternoon** and **Evening** are the most congested and delay-prone periods.  
- Major hubs like **Texas, California, Georgia, Florida, and Illinois** show the highest flight volumes.

---

### 🟨 **Page 2 — Delay Cause Analysis**
**Visuals:**
- **Pie Chart:** Delay Type Breakdown  
  - Carrier Delay → 30%  
  - Late Aircraft → 40%  
  - NAS Delay → 24%  
  - Weather Delay → 6%  
  - Security Delay → <1%  
- **Bar Chart:** Average Delay by Period (Day vs Night)
- **Top 10 Delayed Carriers**
- **Average Delay per Cause**

**Insights:**
- **Late Aircraft Delay (40%)** is the largest contributor to overall delays.  
- **Carrier-related delays (30%)** are the second biggest factor, suggesting operational inefficiencies.  
- **Night flights** show slightly higher average delays compared to **Day flights** (≈ 45 vs 40 min).  

---

### 🟩 **Page 3 — Carrier & Airport Performance**
**Visuals:**
- **Bar Chart:** Total Flights by Carrier  
  - Southwest Airlines, American Airlines, and Delta Air Lines dominate in flight volume.  
- **Stacked Bar Chart:** Delayed vs On-Time flights by Carrier  
- **Map:** Delayed Flights by City/Region  
- **Bar Chart:** Cancelled Flights per Airport  
  - Top cancellations: *Chicago O’Hare*, *George Bush Intercontinental*, *Atlanta*, *Denver*.

**Insights:**
- **Chicago O’Hare** and **Atlanta Hartsfield** airports experience the most cancellations.  
- **Southwest Airlines** has the largest flight volume, but also one of the highest delay rates.  
- Coastal states (California, Florida, Texas) experience frequent delays due to congestion and weather.  

---

## 📈 KPIs Summary

| KPI | Value | Insight |
|------|--------|----------|
| **Total Flights** | 2M | Overall dataset coverage |
| **Delayed Flights** | 1.94M (≈89%) | High proportion of delays |
| **Cancelled Flights** | 633K | Moderate cancellation rate |
| **Diverted Flights** | 7.7K | Very small fraction diverted |
| **Avg Departure Delay** | 43.19 min | Typical outbound delay |
| **Avg Taxi Out Time** | 18.23 min | Average pre-takeoff wait |
| **Avg Taxi In Time** | 6.81 min | Average post-landing time |

---

## 🧠 Key Business Insights

1. **High delay rate (≈89%)** indicates systemic operational and scheduling issues across major carriers.  
2. **Late Aircraft and Carrier delays (70% combined)** are the leading causes — suggesting inefficient turnaround management.  
3. **Peak delay times:** Afternoon and Evening periods, aligning with busiest traffic windows.  
4. **Regional trend:** Delays concentrated in *Texas, California, Georgia, and Illinois*.  
5. **Airports with most cancellations:** Chicago O’Hare, Atlanta, and Houston Bush Intercontinental.  
6. **Southwest Airlines** leads total flights but also among top delayed carriers.  
7. **Weather delays** relatively low (6%) — meaning most issues are controllable (not external).

---

## 🧭 Interactive Features & Design Choices
- **Navigation Buttons:** Between Overview → Delay Causes → Performance pages.  
- **Slicers:** By Year, Carrier, Airport, and Delay Type.  
- **Custom Tooltips:** Showing flight counts, average delay, and delay breakdown per carrier.  
- **Day/Night Segmentation:** Derived from departure/arrival time columns.  
- **Icons & Cards:** Used minimalist design for clarity.  
- **Professional Color Palette:** Blue–Yellow–Gray scheme for contrast and readability.  
- **Map Visualization:** For regional delay density.

---

## 🧩 Tools & Techniques Used

| Tool / Feature | Purpose |
|----------------|----------|
| **Power BI Desktop** | Main visualization tool |
| **Power Query Editor** | Data cleaning, transformations, and type corrections |
| **DAX (Data Analysis Expressions)** | Custom measures and calculated columns |
| **Calendar Table (DAX)** | Time intelligence and seasonal trends |
| **Bookmarks & Navigation Buttons** | Page interactivity |
| **Custom Tooltips** | Contextual insights |
| **Card & KPI visuals** | Key metrics display |
| **Maps & Pie Charts** | Regional and categorical insights |
| **Line & Bar Charts** | Trend and comparison visualization |
| **Slicers & Filters** | Interactive data exploration |

---

## 🧾 Bonus: Time Dimension
A **Time Table** was also created to analyze flight patterns by time of day:

| Period | Range | Notes |
|---------|--------|-------|
| **Morning** | 06:00–11:59 | Low congestion, fewer delays |
| **Afternoon** | 12:00–17:59 | Peak flight hours |
| **Evening** | 18:00–23:59 | High delays due to traffic |
| **Night** | 00:00–05:59 | Fewer flights, but longer average delays |

---

## 🪄 Creative Design Highlights
- Clean, minimalist theme with airline-inspired color palette (Blue/Sky/White).  
- Page navigation icons for easy user experience.  
- Distinct report pages to avoid clutter.  
- Responsive visuals for interactive storytelling.  
- Focus on interpretability and trend discovery.

---

## 📎 Files
- `Airline_Delay_Causes.csv` — Source dataset
- `Airport_codes.csv` — Source dataset
- `DelayedFlights.csv` — Source dataset  
- `Lab05.pbix` — Power BI Project  
- `Lab05.pdf` — Exported Dashboard Report  

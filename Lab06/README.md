# 🏨 Hotel Bookings Dashboard

### 📁 Dataset
**Source:** `hotels.csv`  
**Description:** The dataset contains detailed records of hotel bookings including information such as hotel type, reservation status, room type, arrival date, lead time, customer type, ADR (Average Daily Rate), and more.

---

## 🔧 Data Preparation & Cleaning (Power Query Editor)

**1. Data Loading**
- Imported `hotels.csv` into Power BI Desktop.
- Verified column headers and data types.

**2. Data Cleaning**
- Removed nulls / missing values in key fields such as `hotel`, `arrival_date`, `adr`, and `reservation_status_date`.
- Corrected data types:
  - `arrival_date` → *Date*
  - `adr` (Average Daily Rate) → *Decimal number*
  - `is_canceled`, `is_repeated_guest` → *Whole number (binary)*
- Handled inconsistent entries: fixed spelling and categorical values for columns like `customer_type`, `market_segment`, and `meal`.
- Filtered invalid ADRs (negative or zero).

**3. Transformations & New Columns**
- `Revenue = ADR × (Stays_in_week_nights + Stays_in_weekend_nights)`
- `Length of Stay = Stays_in_week_nights + Stays_in_weekend_nights`
- `Peak Season` based on arrival month (June–August → “Summer Peak”)
- `Occupancy Rate = (Number of Bookings / Total Rooms Available) × 100`
- `Cancellation Rate = (Canceled Bookings / Total Bookings) × 100`

---

## 📊 Dashboard Overview

A modern, interactive dashboard was built to visualize key metrics and insights.

### 🎯 KPIs
| Metric | Description | Value |
|---------|--------------|--------|
| **Total Bookings** | Total number of bookings | 119K |
| **Total Revenue** | Total ADR-based revenue | 198.93M |
| **Average Daily Rate (ADR)** | Mean ADR per booking | ~108 |
| **Occupancy Rate** | Booked rooms vs. total capacity | ~82% |
| **Cancellation Rate** | Share of cancelled bookings | 36% |
| **Repeated Guest Bookings** | Loyal customer indicator | 15K (≈13%) |

---

## 📈 Visualizations & Insights

### 1. Bookings & Cancellations Overview
- 63% of bookings were completed successfully, 36% canceled, 1% no-shows.
- Portugal, UK, and France are top booking sources — Portugal leads both total and canceled bookings.

### 2. Bookings by Hotel Type
- City Hotels: 79K bookings (≈60%)
- Resort Hotels: 40K bookings (≈40%)
- City hotels generate higher ADR and revenue due to business demand.

### 3. Seasonal Trends
- Summer (June–August) = Peak season (~36K bookings).
- Winter = Lowest bookings (~20K).

### 4. Market Segment Performance
- Online TA/TO leads in revenue (≈108M) and volume.
- Offline TA/TO and Direct bookings follow.
- Groups show higher ADR but lower volume.

### 5. Customer Behavior
- Transient customers dominate (≈59%).
- Contract customers have longest average stays (≈5.3 nights).
- Repeated Guests: 13% of all bookings, mostly in City Hotels.

### 6. Room Type Analysis
- Room types G, H, F have highest ADR (≈170–180).
- These premium rooms also face higher cancellations.

### 7. Revenues by Country
- Portugal (≈60M), UK (24M), France (19M), Spain (16M), Germany (12M).

### 8. Meal Type Impact
- Bed & Breakfast generates ≈146M revenue.
- Full Board and Half Board have higher ADRs but smaller volumes.

---

## 🧭 Interactive Features
- **Slicers:** Date, Hotel Type, Market Segment, Country, and Customer Type.
- **Tooltips:** Customized to show ADR, Revenue, and Cancellation Rate.
- **Dynamic Cards:** KPIs auto-update with slicers.
- **Clean Layout:** Grid-based design and intuitive navigation.

---

## 🎨 Design & User Experience
- Professional **blue–gray theme**.
- Clear hierarchy: KPIs → Trends → Segments → Behavior.
- Consistent fonts, spacing, and colors.
- Subtle background to enhance focus.
- Tooltips add contextual insights.

---

## ☁️ Bonus: Publishing
- Dashboard successfully published to **Power BI Report Server**.
- Screenshot shows live report hosted online with full interactivity.

---

## 🧠 Key Business Insights
1. High cancellation rate (36%) — mainly from online channels and premium rooms. Suggest deposit policies.
2. City Hotels outperform Resorts in volume and loyalty.
3. Summer months drive majority of revenue; off-season marketing recommended.
4. Transient guests form largest revenue base — target for loyalty programs.
5. Portugal and UK are top-performing markets.
6. Premium room types (G–H–F) show price sensitivity despite high ADRs.

---

## 📎 Files
- `hotels.csv` — Source dataset  
- `Lab06.pbix` — Power BI Dashboard  
- `Lab06.pdf` — Exported report  

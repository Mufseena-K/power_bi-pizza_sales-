# Power BI Pizza Sales Dashboard
# 🍕 Plato Pizza Sales Dashboard

## 📌 Project Overview
### 1.1 Project Title
**Plato Pizza Sales Dashboard**

### 1.2 Objective
To help the restaurant **Plato Pizza** improve its operations and performance using the dataset collected in **2015**.

### 1.3 Scope
#### 📂 Datasets Used
The project analyzes a year's worth of sales (2015) from a fictitious pizza place, leveraging four tables:

- **Order Details (Fact Table)**: 48,621 rows, 4 columns → `order_details_id`, `order_id`, `pizza_id`, `quantity`
- **Orders (Dimension Table)**: 21,350 rows, 3 columns → `order_id`, `date`, `time`
- **Pizza Types (Sub-Dimension Table of Pizza)**: 33 rows, 4 columns → `pizza_type_id`, `name`, `category`, `ingredients`
- **Pizzas (Dimension Table)**: 97 rows, 4 columns → `pizza_id`, `pizza_type_id`, `size`, `price`

#### 📊 Key Metrics
- **Total Revenue** → Overall sales performance
- **Total Orders** → Number of orders placed
- **Total Pizzas Sold** → Total quantity of pizzas sold

#### 🔍 Visualizations
- **Total Sales Overview** → Summary dashboard with revenue, order count, and pizzas sold
- **Time-Based Sales Trends** → Monthly, daily, and hourly sales trends
- **Best & Worst Selling Pizzas** → Bar charts and tables ranking pizzas by revenue and quantity
- **Pizza Category & Size Analysis** → Pie charts & bar graphs displaying revenue distribution
- **Customer Behavior Insights** → Stacked bar charts comparing 2-person vs. 3+ person orders
- **Seat Occupancy Impact** → Heatmaps or scatter plots showing table occupancy effects on sales

### 1.4 Timeline
| Phase | Description | Estimated Duration |
|---|---|---|
| **Data Collection** | Gathering relevant datasets | 1 day |
| **Data Cleaning** | Handling missing values, removing duplicates | 0.5 day |
| **Data Modeling** | Defining relationships, creating measures | 0.5 day |
| **Visualization** | Designing dashboard and visual elements | 3 days |
| **Final Review** | Testing and refining dashboard | 2 days |

---

## 📂 2. Data Collection & Preparation
### 2.1 Data Sources
The datasets are in **CSV format**.

### 2.2 Data Cleaning & Transformation
Performed in **Power Query**, steps include:

- **Handling Missing Values** → Checked for NULLs using column profiling
- **Removing Duplicates** → Used "Remove Duplicates" feature for:
  - `orders` (order_id)
  - `order_details` (order_details_id)
  - `pizzas` (pizza_id)
  - `pizza_types` (pizza_type_id)
- **Data Type Transformations**:
  - Converted `orders.date` and `orders.time` to **datetime**
  - Transformed `pizzas.price` to **decimal**
  - Standardized text columns by removing extra spaces
  - Extracted **Year, Month, Day, and Weekday** for trend analysis

### 2.3 Data Model
A **Snowflake Schema** was developed with **one-to-many** relationships:
- `orders` → `order_details` (`order_id`)
- `pizzas` → `order_details` (`pizza_id`)
- `pizza_types` → `pizzas` (`pizza_type_id`)

---

## 📊 3. Dashboard Development
### 3.1 Mockup Designs
Wireframes were created to define layout and design.

### 3.2 Key Visualizations
#### 🔥 **Key Performance Indicators (KPIs)**
**Purpose:** Summarize overall business performance.
**Metrics:**
- Total Revenue
- Total Orders
- Total Pizzas Sold
- Average Daily Pizza Sold
- Average Pizza per Order

**Visualization Type:** KPI Cards with dynamic period comparison.

#### 📌 **Sales Trends Over Time**
**Purpose:** Analyze revenue and order volume trends.

**Visuals Used:**
- Bar Chart → **Monthly Revenue Trends**
- Line Chart → **Daily Revenue Trends**
- Heat Map → **Hourly Sales Distribution**
- Donut Chart → **Weekend vs. Weekday Sales**

#### 🍕 **Pizza Performance Analysis**
- **Top 5 Pizzas by Revenue** → Horizontal Bar Chart
- **Bottom 5 Pizzas by Revenue** → Horizontal Bar Chart
- **Top 10 Pizzas by Quantity Sold** → Vertical Bar Chart
- **2-Person vs. 3+ Person Orders** → Donut Chart
- **Pizza Category & Size Sales** → Treemap
- **Seat Occupancy Trends** → Area Chart

### 3.3 DAX Measures & Calculations
- **Total Revenue** = SUM(`order_details.quantity * pizzas.price`)
- **Total Orders** = DISTINCTCOUNT(`orders.order_id`)
- **Total Pizzas Sold** = SUM(`order_details.quantity`)
- **Avg Daily Pizza Sold** = DIVIDE(`Total Pizzas Sold`, DISTINCTCOUNT(`orders.date`))
- **Avg Pizza Per Order** = DIVIDE(`Total Pizzas Sold`, `Total Orders`)
- **Weekend vs. Weekday Sales** = CALCULATE(`Total Revenue`, FILTER(`orders`, `orders.weekday` IN {"Saturday", "Sunday"}))

### 3.4 Filters & Slicers
- **Month Selector** → Compare seasonal trends
- **Day of the Week Filter** → Compare weekdays vs. weekends
- **Pizza Category Filter** → Veg, Non-Veg, Classic, Specialty
- **Pizza Size Filter** → Small, Medium, Large, Extra-Large

---

## 🔍 4. Insights & Findings
### Sales Performance Overview
- **Total Sales**: $818K revenue from **21K orders** and **50K pizzas sold**.
- **Business Impact**: Helps track revenue trends and performance evaluation.

### Peak Sales Hours & Time-Based Trends
- **Highest Sales**: **6 PM - 9 PM (Evening hours)**.
- **Lowest Sales**: **Early mornings & late nights**.
- **Business Impact**: Optimize staffing, promotions & inventory.

### Top & Least Selling Pizzas
- **Best-Selling Pizzas**: Classic Pepperoni & BBQ Chicken.
- **Low-Demand Pizzas**: Some specialty pizzas.
- **Business Impact**: Promote best-sellers, re-evaluate underperforming items.

### Customer Order Behavior
- **Small Orders (1-2 Pizzas)**: Dominant, indicating many individual/couple orders.
- **Group Orders (3+ Pizzas)**: High volume, suggesting potential for combo deals.
- **Business Impact**: Optimize menu deals & pricing strategies.

### Seat Occupancy & Sales Impact
- **Higher Sales Days**: Weekends show peak occupancy and higher revenue.
- **Business Impact**: Targeted promotions for quieter times.

---

## 🚧 5. Challenges & Limitations
- Difficulty selecting **DAX measures vs. calculated columns**.
- **Zero value errors** in `DIVIDE()` function.
- Assumptions in **Seat Occupancy & Order Grouping**.
- **Customer group classification (2 vs. 3+ persons)** is based on assumptions.

---

## 🔮 6. Future Enhancements
- Add **customer demographics** for deeper insights.
- Include **campaign & discount data** to track marketing impact.
- Integrate **supplier & inventory data** for cost tracking.
- Implement **year-over-year sales trend analysis**.

---

## 🏁 7. Conclusion
This project helps **Plato Pizza** make **data-driven decisions** to optimize menu pricing, improve operations, and enhance customer experience. **Power BI** provides an intuitive visual representation of key metrics, empowering stakeholders to act on insights.

---

## 📌 8. References
Inspired by Maven Analytics' Power BI Challenge.

---

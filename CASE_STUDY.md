<div align="center">

# 📊 Case Study: ZestyEats Analytics

## Transforming Food Delivery Operations Through Data Intelligence

🍕

*How I built an end-to-end Power BI solution to optimize delivery performance and drive revenue growth*

</div>

---

## 📌 Executive Summary

| Aspect | Details |
|--------|---------|
| **Project** | ZestyEats - Food Delivery Analytics Dashboard |
| **Duration** | 3 weeks |
| **Role** | Data Analyst / BI Developer |
| **Tools** | Power BI, DAX, Power Query, Excel |
| **Outcome** | 3 production-ready dashboards with 15+ visualizations |

### 🔗 [**View Live Dashboard →**](https://app.powerbi.com/groups/5c9dc702-7a40-4b6f-bb78-cacd8b8b75fe/reports/3fddc3de-9054-41e3-8b36-ff2add5ddaae/97b0d558e989029bcba1?experience=power-bi)

---

## 🎯 The Challenge

### Business Context

ZestyEats, a growing food delivery platform, was facing operational challenges due to lack of data visibility:

- **No centralized view** of business performance
- **Manual Excel reports** taking hours to prepare
- **Delivery delays** impacting customer satisfaction
- **Revenue leakage** from unoptimized operations

### Key Problems

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│   ❌ SILOED DATA              5 separate Excel sheets, no insights │
│   ❌ MANUAL REPORTING         4+ hours weekly on Excel reports     │
│   ❌ NO REAL-TIME KPIs        Decisions based on outdated data     │
│   ❌ DELIVERY INEFFICIENCY    No visibility into performance       │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Stakeholder Requirements

| Stakeholder | Need |
|-------------|------|
| **CEO/Management** | Executive KPI dashboard for quick decisions |
| **Operations Team** | Delivery performance tracking & optimization |
| **Marketing** | Customer demographics & ordering patterns |
| **Finance** | Revenue analysis by category, time, region |

---

## 🔍 My Approach

### Phase 1: Data Discovery & Assessment

**Objective**: Understand data sources and define analytics requirements

**Data Sources Analyzed**:
```
📁 Multi-Sheet Excel File
├── 📋 Orders Table (10,000+ transactions)
├── 🚚 Deliveries Table (delivery status & times)
├── 👥 Customers Table (demographics)
├── 🏪 Restaurants Table (catalog & categories)
└── 🛵 Delivery Personnel Table (rider information)
```

**Key Questions to Answer**:
1. What are our key performance metrics?
2. Which customer segments drive the most revenue?
3. How efficient is our delivery operation?
4. What factors impact on-time delivery?

---

### Phase 2: Data Modeling & Transformation

**Objective**: Build a robust data model for efficient analysis

**Power Query Transformations**:

| Transformation | Purpose |
|----------------|---------|
| Column Type Standardization | Ensure correct data types |
| Null Value Handling | Replace blanks with defaults |
| Date Table Creation | Enable time intelligence |
| Calculated Columns | Derived metrics for analysis |

**Star Schema Design**:

```
                    ┌─────────────────┐
                    │   📅 Date       │
                    │   Dimension     │
                    └────────┬────────┘
                             │
┌─────────────────┐          │          ┌─────────────────┐
│   👥 Customers  │          │          │   🏪 Restaurants │
│   Dimension     │          │          │   Dimension      │
└────────┬────────┘          │          └────────┬────────┘
         │                   │                   │
         │         ┌─────────┴─────────┐         │
         └─────────┤   📋 Orders       ├─────────┘
                   │   Fact Table      │
         ┌─────────┤                   ├─────────┐
         │         └─────────┬─────────┘         │
         │                   │                   │
┌────────┴────────┐          │          ┌────────┴────────┐
│   🚚 Deliveries │          │          │   🛵 Personnel  │
│   Fact Table    │──────────┘          │   Dimension     │
└─────────────────┘                     └─────────────────┘
```

**Relationships Created**:
- Orders → Customers (Many-to-One)
- Orders → Restaurants (Many-to-One)
- Orders → Deliveries (One-to-One)
- Deliveries → Personnel (Many-to-One)
- Orders → Date (Many-to-One)

---

### Phase 3: DAX Measures Development

**Objective**: Create calculated measures for comprehensive analysis

**Core Measures Created**:

```dax
// Revenue Metrics
Total Revenue = SUM(Orders[Amount])

Average Order Value = 
    DIVIDE([Total Revenue], [Total Orders], 0)

// Delivery Performance
On-Time Delivery Rate = 
    DIVIDE(
        COUNTROWS(FILTER(Deliveries, Deliveries[DeliveryTime] <= 30)),
        COUNTROWS(Deliveries),
        0
    ) * 100

// Customer Metrics
Revenue by Segment = 
    CALCULATE(
        [Total Revenue],
        ALLEXCEPT(Customers, Customers[AgeGroup])
    )

// Context Manipulation
Revenue % of Total = 
    DIVIDE(
        [Total Revenue],
        CALCULATE([Total Revenue], ALL(Orders)),
        0
    )
```

**Measure Categories**:

| Category | Measures Count | Examples |
|----------|----------------|----------|
| **Revenue** | 4 | Total, Average, % of Total, Growth |
| **Orders** | 3 | Count, Completion Rate, Frequency |
| **Delivery** | 4 | On-Time %, Avg Time, Efficiency Score |
| **Customer** | 3 | Count, Avg Age, Segment Revenue |

---

### Phase 4: Dashboard Design & Development

**Objective**: Create intuitive, actionable dashboards for each stakeholder

#### 📌 Dashboard 1: Executive KPIs
*For: CEO, Management*

```
┌─────────────────────────────────────────────────────────────────────┐
│                      📊 EXECUTIVE DASHBOARD                         │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐    │
│  │  Total     │  │  Avg Order │  │  On-Time   │  │  Customer  │    │
│  │  Revenue   │  │  Value     │  │  Delivery  │  │  Count     │    │
│  │  ₹12.5M    │  │  ₹485      │  │  87%       │  │  5,247     │    │
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘    │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │              Revenue Trend (Monthly)                         │   │
│  │  📈 ════════════════════════════════════════════════════    │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                                                                     │
│  ┌──────────────────────┐  ┌──────────────────────┐                │
│  │  Revenue by Category │  │  Top Restaurants     │                │
│  │  🥧 [Donut Chart]    │  │  📊 [Bar Chart]      │                │
│  └──────────────────────┘  └──────────────────────┘                │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**Components**:
- 4 KPI Cards with sparklines
- Monthly revenue trend line chart
- Revenue by food category (Donut)
- Top 10 restaurants by revenue (Bar)
- Date range slicer

---

#### 📌 Dashboard 2: Customer Analytics
*For: Marketing, Sales*

```
┌─────────────────────────────────────────────────────────────────────┐
│                      👥 CUSTOMER ANALYTICS                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌──────────────────────┐  ┌──────────────────────┐                │
│  │  Age Distribution    │  │  Gender Split        │                │
│  │  📊 [Histogram]      │  │  🥧 [Pie Chart]      │                │
│  │                      │  │                      │                │
│  │  18-25: 35%         │  │  Male: 58%           │                │
│  │  26-35: 40%         │  │  Female: 42%         │                │
│  │  36-45: 18%         │  │                      │                │
│  │  45+: 7%            │  │                      │                │
│  └──────────────────────┘  └──────────────────────┘                │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │           Revenue by Customer Segment                        │   │
│  │  Young (18-25)    ████████████████████  35%  (₹4.4M)        │   │
│  │  Adult (26-35)    ██████████████████████████  45%  (₹5.6M)  │   │
│  │  Middle (36-45)   ████████████  15%  (₹1.9M)                │   │
│  │  Senior (45+)     ████  5%  (₹0.6M)                         │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                                                                     │
│  ┌──────────────────────┐  ┌──────────────────────┐                │
│  │  Order Value Dist.  │  │  Order Frequency     │                │
│  │  📊 [Histogram]      │  │  📈 [Scatter Plot]   │                │
│  └──────────────────────┘  └──────────────────────┘                │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**Components**:
- Age group distribution histogram
- Gender breakdown pie chart
- Revenue by segment horizontal bar
- Order value distribution
- Customer frequency scatter plot
- Interactive slicers (Age, Gender, Location)

---

#### 📌 Dashboard 3: Delivery Performance
*For: Operations Team*

```
┌─────────────────────────────────────────────────────────────────────┐
│                    🚚 DELIVERY PERFORMANCE                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐    │
│  │  Total     │  │  On-Time   │  │  Avg       │  │  Delayed   │    │
│  │ Deliveries │  │  Rate      │  │  Time      │  │  Orders    │    │
│  │  9,847     │  │  87%       │  │  28 min    │  │  1,280     │    │
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘    │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │         Delivery Time vs Traffic Conditions                  │   │
│  │  📈 [Scatter Plot with Trend Line]                           │   │
│  │                                                               │   │
│  │  • Low Traffic: 22 min avg                                   │   │
│  │  • Medium Traffic: 28 min avg                                │   │
│  │  • High Traffic: 38 min avg                                  │   │
│  └─────────────────────────────────────────────────────────────┘   │
│                                                                     │
│  ┌──────────────────────┐  ┌──────────────────────┐                │
│  │  By Vehicle Type     │  │  Top Performers      │                │
│  │  🗺️ [Treemap]        │  │  📊 [Bar Chart]      │                │
│  │                      │  │                      │                │
│  │  Bike: 45%          │  │  1. Rider A: 98%    │                │
│  │  Scooter: 35%       │  │  2. Rider B: 96%    │                │
│  │  Car: 20%           │  │  3. Rider C: 95%    │                │
│  └──────────────────────┘  └──────────────────────┘                │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

**Components**:
- 4 KPI cards (Deliveries, On-Time %, Avg Time, Delayed)
- Traffic impact scatter plot
- Vehicle type efficiency treemap
- Top 10 delivery personnel bar chart
- Hourly delivery heatmap
- Time period slicers

---

### Phase 5: Testing & Refinement

**Objective**: Ensure accuracy, performance, and usability

**Testing Performed**:

| Test Type | Actions | Result |
|-----------|---------|--------|
| **Data Accuracy** | Cross-verified totals with source | ✅ 100% match |
| **DAX Validation** | Tested edge cases in measures | ✅ All passed |
| **Performance** | Optimized slow visuals | ✅ < 3s load time |
| **Usability** | Stakeholder feedback sessions | ✅ Approved |
| **Cross-filtering** | Verified slicer interactions | ✅ Working |

**Refinements Made**:
- Simplified cluttered visuals based on feedback
- Added conditional formatting for KPIs
- Implemented bookmarks for quick navigation
- Created mobile-optimized view

---

## 📊 Results & Impact

### Quantitative Outcomes

<div align="center">

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| **Report Preparation Time** | 4+ hours/week | 0 (real-time) | ⬇️ 100% reduction |
| **Data Freshness** | Weekly | Real-time | ⬆️ Instant insights |
| **Stakeholder Satisfaction** | Manual requests | Self-service | ⬆️ High adoption |
| **Decision Speed** | Days | Minutes | ⬆️ 95% faster |

</div>

### Dashboard Deliverables

| Dashboard | Visualizations | Measures | Slicers |
|-----------|----------------|----------|---------|
| Executive KPIs | 6 | 4 | 2 |
| Customer Analytics | 5 | 4 | 4 |
| Delivery Performance | 5 | 4 | 3 |
| **Total** | **16** | **12** | **9** |

---

## 💡 Key Insights Delivered

### 🎯 Insight 1: Customer Demographics
> **80% of revenue comes from customers aged 18-35**

*Recommendation*: Focus marketing campaigns on young adults; consider loyalty programs for this segment

### 📦 Insight 2: Order Value Patterns
> **Orders between ₹400-₹600 have highest frequency; orders > ₹1000 are rare**

*Recommendation*: Create combo deals in the ₹400-600 range; implement upselling for larger orders

### 🚚 Insight 3: Traffic Impact
> **High traffic conditions increase delivery time by 73% (22 min → 38 min)**

*Recommendation*: Implement dynamic delivery time estimates; consider peak-hour surge pricing

### 🛵 Insight 4: Vehicle Efficiency
> **Bikes outperform scooters and cars in urban deliveries by 15%**

*Recommendation*: Prioritize bike fleet for dense urban areas

### 🏪 Insight 5: Restaurant Performance
> **Top 20% of restaurants generate 65% of total revenue**

*Recommendation*: Strengthen partnerships with top performers; analyze success factors

---

## 🛠️ Technical Implementation

### Data Architecture

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Excel      │ ──▶ │ Power Query │ ──▶ │ Data Model  │ ──▶ │ Dashboards  │
│  (5 sheets) │     │ (Transform) │     │ (Star Schema)│     │ (3 pages)   │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
```

### Advanced DAX Patterns Used

**1. Time Intelligence**:
```dax
Revenue YoY Growth = 
    VAR CurrentYear = [Total Revenue]
    VAR PreviousYear = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR(Date[Date]))
    RETURN DIVIDE(CurrentYear - PreviousYear, PreviousYear, 0)
```

**2. Dynamic Segmentation**:
```dax
Order Category = 
    SWITCH(
        TRUE(),
        Orders[Amount] < 300, "Low",
        Orders[Amount] < 700, "Medium",
        "High"
    )
```

**3. Context Manipulation**:
```dax
% of Category = 
    DIVIDE(
        [Total Revenue],
        CALCULATE([Total Revenue], ALL(Restaurants[Category])),
        0
    )
```

---

## 💭 Lessons Learned

### What Worked Well

✅ **Starting with stakeholder interviews** - Understood real needs before building

✅ **Star schema design** - Enabled efficient DAX calculations

✅ **Iterative feedback** - Weekly demos kept stakeholders engaged

✅ **Clear naming conventions** - Made measures self-documenting

### Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Complex DAX calculations | Broke into smaller measures |
| Slow dashboard load | Removed unnecessary columns |
| Stakeholder alignment | Created shared glossary |
| Mobile responsiveness | Built separate mobile view |

### What I'd Do Differently

1. **Define KPIs formally** with stakeholders upfront
2. **Create data dictionary** before starting development
3. **Plan for mobile** from the beginning
4. **Implement row-level security** for department views

---

## 📚 Skills Demonstrated

<div align="center">

| Category | Skills |
|----------|--------|
| **Power BI** | Data Modeling, DAX, Power Query, Visualizations |
| **Data Analysis** | KPI Definition, Trend Analysis, Segmentation |
| **Business Intelligence** | Dashboard Design, Storytelling with Data |
| **Communication** | Stakeholder Management, Requirements Gathering |
| **Problem Solving** | Performance Optimization, Data Quality |

</div>

---

## 🔗 Project Links

<div align="center">

| Resource | Link |
|----------|------|
| 🔴 **Live Dashboard** | [View on Power BI](https://app.powerbi.com/groups/5c9dc702-7a40-4b6f-bb78-cacd8b8b75fe/reports/3fddc3de-9054-41e3-8b36-ff2add5ddaae/97b0d558e989029bcba1?experience=power-bi) |
| 📁 **GitHub Repository** | [ZestyEatsAnalysis](https://github.com/rahulx2001/ZestyEatsAnalysis) |
| 🌐 **Portfolio** | [rahulkumarsingh-portfolio.vercel.app](https://rahulkumarsingh-portfolio.vercel.app) |
| 💼 **LinkedIn** | [linkedin.com/in/rahulx2001](https://linkedin.com/in/rahulx2001) |

</div>

---

<div align="center">

## 📫 Let's Connect

Interested in discussing this project or data analysis opportunities?

[![Email](https://img.shields.io/badge/Email-rahulsinghx2001@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:rahulsinghx2001@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/rahulx2001)

---

*Case Study by [Rahul Kumar Singh](https://github.com/rahulx2001) • Data Analyst*

</div>

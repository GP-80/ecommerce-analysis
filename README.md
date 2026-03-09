# E-Commerce Customer Segmentation Analysis

A comprehensive RFM (Recency, Frequency, Monetary) analysis of e-commerce transaction data to identify and segment customers based on purchasing behavior.

## 📊 Project Overview

This project analyzes over 540,000 transactions from an online retail dataset to segment customers into actionable groups. Using RFM methodology, customers are scored and categorized to enable targeted marketing strategies and improve customer retention.

**Key Insights:**
- Segmented 4,338 customers into 6 distinct groups
- Identified that Champions (13.2% of customers) drive 55% of total revenue
- Found 203 At-Risk customers (previously frequent buyers now inactive) requiring immediate re-engagement
- Discovered 1,505 Lost customers representing recovery opportunities

## 🎯 Business Value

- **Targeted Marketing:** Different segments require different strategies (Champions vs. Lost customers)
- **Revenue Optimization:** Focus resources on high-value segments
- **Churn Prevention:** Identify At-Risk customers before they're lost
- **Customer Lifecycle Management:** Track customer journey from New to Champion

## 🛠️ Technologies Used

- **Python 3.x**
  - pandas: Data manipulation and analysis
  - sqlite3: Database operations
  - datetime: Date/time handling
- **Power BI Desktop**: Interactive dashboard and visualizations
- **SQLite**: Data storage and querying
- **Jupyter Lab**: Development environment

## 📁 Project Structure

```
ecommerce-analysis/
│
├── data/
│   ├── raw/                    # Original CSV data (not tracked)
│   ├── ecommerce.db           # SQLite database
│   ├── transactions_clean.csv # Cleaned transaction data
│   └── rfm_analysis.csv       # RFM scores and segments
│
├── notebooks/
│   ├── 01_initial_exploration.ipynb    # Data loading and exploration
│   ├── 02_data_cleaning.ipynb          # Data cleaning and feature engineering
│   └── 03_rfm_analysis.ipynb           # RFM calculation and segmentation
│
├── RFM_Dashboard.pbix         # Power BI dashboard file
│
└── README.md
```

## 🔍 Methodology

### 1. Data Cleaning
- Removed cancelled orders (InvoiceNo starting with 'C')
- Filtered out negative quantities and prices
- Handled missing CustomerIDs
- Removed duplicate transactions
- **Result:** 392,692 clean transactions from 541,909 raw records

### 2. Feature Engineering
- Created `TotalPrice` (Quantity × UnitPrice)
- Extracted `Year`, `Month`, `YearMonth` from InvoiceDate
- Converted dates to datetime format for analysis

### 3. RFM Calculation

**Recency:** Days since last purchase (lower = better)
```python
recency = (snapshot_date - last_purchase_date).days
```

**Frequency:** Number of unique orders per customer
```python
frequency = count(distinct InvoiceNo)
```

**Monetary:** Total revenue contributed by customer
```python
monetary = sum(TotalPrice)
```

### 4. Scoring (1-5 scale using quintiles)
- Customers divided into 5 equal groups per metric
- Recency: Inverted scoring (fewer days = higher score)
- Frequency & Monetary: Standard scoring (higher value = higher score)

### 5. Customer Segmentation

| Segment | Criteria | Count | % of Customers | Total Revenue |
|---------|----------|-------|----------------|---------------|
| **Champion** | R≥4, F≥4, M≥4 | 573 | 13.2% | $4.95M (55.7%) |
| **Loyal Customer** | R≥3, F≥3 | 726 | 16.7% | $1.56M (17.6%) |
| **New Customer** | R≥4, F≤2 | 737 | 17.0% | $675K (7.6%) |
| **Potential Loyalist** | Others | 594 | 13.7% | $380K (4.3%) |
| **At Risk** | R≤2, F≥3 | 203 | 4.7% | $371K (4.2%) |
| **Lost** | R≤2, F≤2 | 1,505 | 34.7% | $946K (10.6%) |

## 📈 Key Findings

1. **Revenue Concentration:** 13% of customers (Champions) generate 56% of revenue
2. **Large Inactive Base:** 35% of customers are Lost, representing significant re-engagement opportunity
3. **At-Risk Alert:** 203 previously valuable customers haven't purchased recently
4. **Seasonal Trends:** Revenue peaks in November (holiday shopping), lowest in January/February
5. **Geographic Distribution:** UK dominates with 91% of transactions

## 🎨 Dashboard

Interactive Power BI dashboard featuring:
- **KPI Cards:** Total customers, revenue, avg recency/frequency, total orders
- **Segment Breakdown:** Customer count and revenue by segment
- **Time Series:** Revenue trends by month
- **Filters:** Country selector for geographic analysis

[Dashboard Preview]

<img width="1568" height="860" alt="dashboard" src="https://github.com/user-attachments/assets/b9848a82-87e7-44b4-a7cf-a139813fe1a4" />


## 🚀 How to Run This Project

### Prerequisites
```bash
pip install pandas jupyter
```

### Steps

1. **Clone the repository**
```bash
git clone https://github.com/GP-80/ecommerce-analysis.git
cd ecommerce-analysis
```

2. **Run the analysis notebooks in order:**
   - `01_initial_exploration.ipynb` - Data loading and exploration
   - `02_data_cleaning.ipynb` - Data cleaning and feature engineering  
   - `03_rfm_analysis.ipynb` - RFM calculation and segmentation

3. **View the Power BI Dashboard:**
   - Open `RFM_Dashboard.pbix` in Power BI Desktop
   - Data automatically loads from CSV files in `/data/` folder

## 💡 Actionable Recommendations

**For Champions (573 customers, $4.95M revenue):**
- Implement VIP loyalty program
- Early access to new products
- Personalized thank-you campaigns

**For At Risk (203 customers, $371K revenue):**
- Immediate win-back email campaign
- Special discount offers (10-15%)
- Survey to understand why they stopped buying

**For Lost (1,505 customers, $946K potential):**
- Large-scale re-engagement campaign
- "We miss you" incentives
- Segment by previous value - prioritize high spenders

**For New Customers (737 customers):**
- Onboarding email series
- Second-purchase incentive
- Build habit with targeted campaigns

## 📊 Dataset Information

**Source:** UCI Machine Learning Repository - Online Retail Dataset  
**Period:** December 2010 - December 2011  
**Transactions:** 541,909 (392,692 after cleaning)  
**Customers:** 4,338 unique  
**Countries:** 38  
**Products:** 4,000+ unique items

## 📝 License

This project is available for educational and portfolio purposes.

## 🙏 Acknowledgments

- Dataset provided by UCI Machine Learning Repository
- RFM methodology based on industry best practices for customer segmentation
- Built as part of data analytics portfolio development

---

**Last Updated:** March 2026  
**Status:** Complete (unpolished - pending final documentation review)

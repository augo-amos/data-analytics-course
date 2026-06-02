# Week 4 Class Notes: Capstone Project

**Course:** Foundations of Data Analytics (Pilot)  
**Week:** 4 of 4 (Final Week)  
**Prerequisites:** Weeks 1, 2, and 3 completed  
**Instructor:** [Your Name]

---

## Table of Contents

1. [Course Review: Weeks 1-3](#course-review-weeks-1-3)
   - [Week 1: Python Fundamentals](#week-1-python-fundamentals)
   - [Week 2: Data Manipulation with Pandas](#week-2-data-manipulation-with-pandas)
   - [Week 3: Visualization & Tableau](#week-3-visualization--tableau)
2. [Capstone Project Overview](#capstone-project-overview)
3. [The New Dataset](#the-new-dataset)
4. [Step-by-Step Capstone Guide](#step-by-step-capstone-guide)
   - [Step 1: Setup & Initial Exploration](#step-1-setup--initial-exploration)
   - [Step 2: Data Cleaning](#step-2-data-cleaning)
   - [Step 3: Answer Question 1 (Regional Performance)](#step-3-answer-question-1-regional-performance)
   - [Step 4: Answer Question 2 (Category & Segment Analysis)](#step-4-answer-question-2-category--segment-analysis)
   - [Step 5: Answer Question 3 (Time Trend)](#step-5-answer-question-3-time-trend)
   - [Step 6: Export Cleaned Data](#step-6-export-cleaned-data)
   - [Step 7: Build Tableau Dashboard](#step-7-build-tableau-dashboard)
   - [Step 8: Record Loom Video](#step-8-record-loom-video)
   - [Step 9: Submit via GitHub](#step-9-submit-via-github)
5. [Grading Rubric](#grading-rubric)
6. [Common Pitfalls & How to Avoid Them](#common-pitfalls--how-to-avoid-them)
7. [Sample Solutions](#sample-solutions)
8. [Time Management Plan](#time-management-plan)
9. [Final Checklist](#final-checklist)
10. [Key Takeaways from the Pilot](#key-takeaways-from-the-pilot)

---

## Course Review: Weeks 1-3

Before diving into the capstone, let's review what you've learned. **You will need all of these skills this week.**

### Week 1: Python Fundamentals

**What you learned:**
- Variables and data types (int, float, str, bool)
- Lists and list operations (indexing, slicing, appending)
- Loops (`for` and `while`)
- Conditionals (`if`/`elif`/`else`)
- Functions (`def`, parameters, `return`)
- Reading CSV files with Python's `csv` module

**Key syntax reminder:**
```python
# Variables
name = "Data"
price = 19.99

# Lists
items = [1, 2, 3]
items.append(4)

# Loops
for item in items:
    print(item)

# Conditionals
if price > 100:
    print("Expensive")
else:
    print("Cheap")

# Functions
def calculate_total(prices):
    return sum(prices)

# CSV reading
import csv
with open('file.csv', 'r') as f:
    reader = csv.reader(f)
    next(reader)  # Skip header
    for row in reader:
        print(row)
```

**Why this matters for the capstone:** You'll write functions to organize your cleaning code. You'll use loops implicitly through Pandas (which is built on these concepts).

---

### Week 2: Data Manipulation with Pandas

**What you learned:**
- Series and DataFrames
- Reading data: `pd.read_csv()`
- Exploring data: `.head()`, `.info()`, `.describe()`
- Selecting columns: `df['col']`
- Filtering rows: `df[df['col'] > value]`
- Handling missing values: `.isnull()`, `.fillna()`, `.dropna()`
- Grouping and aggregation: `.groupby()`, `.agg()`
- Merging DataFrames: `pd.merge()`
- Exporting data: `.to_csv()`

**Key syntax reminder:**
```python
import pandas as pd

# Read data
df = pd.read_csv('data.csv')

# Explore
print(df.head())
print(df.info())
print(df.isnull().sum())

# Clean
df['col'] = df['col'].fillna(df['col'].median())
df['category'] = df['category'].str.title()

# Filter
high_sales = df[df['sales'] > 1000]

# Group and aggregate
summary = df.groupby('region')['profit'].sum()

# Merge
merged = pd.merge(df1, df2, on='key')

# Export
df.to_csv('clean.csv', index=False)
```

**Why this matters for the capstone:** **This is the most important week for the capstone.** You'll spend 60% of your time cleaning the new dataset with Pandas.

---

### Week 3: Visualization & Tableau

**What you learned:**

**Python (Matplotlib/Seaborn):**
- Line plots: `plt.plot()`
- Bar charts: `plt.bar()` or `sns.barplot()`
- Scatter plots: `plt.scatter()` or `sns.scatterplot()`
- Histograms: `plt.hist()` or `sns.histplot()`
- Customization: titles, labels, colors, legends

**Tableau:**
- Connecting to CSV files
- Dimensions (blue) vs Measures (green)
- Building bar charts, line charts, scatter plots, maps
- Creating calculated fields
- Building dashboards with multiple sheets
- Adding filters and dashboard actions
- Publishing to Tableau Public

**Key syntax reminder (Python):**
```python
import matplotlib.pyplot as plt
import seaborn as sns

# Bar chart
sns.barplot(data=df, x='region', y='profit', estimator=sum)
plt.title('Profit by Region')
plt.show()

# Line chart
plt.plot(dates, profits)
plt.xlabel('Date')
plt.ylabel('Profit')
plt.show()

# Scatter plot
sns.scatterplot(data=df, x='sales', y='profit', hue='region')
plt.show()
```

**Key actions reminder (Tableau):**
- Drag dimension to Columns, measure to Rows = bar chart
- Drag date to Columns, measure to Rows = line chart
- Drag region to Color = color-coded by region
- Right-click date → Month/Week/Day = change granularity
- Drag field to Filters = add filter
- New Dashboard → drag sheets = build dashboard

**Why this matters for the capstone:** You'll create Python charts for exploration (not required but recommended) and a Tableau dashboard for the final deliverable.

---

## Capstone Project Overview

### The Scenario

You are a junior data analyst at **ShopFast**, an online retailer selling electronics, furniture, and office supplies. Your manager, Alex, needs a clear picture of sales performance across regions and customer segments.

### The Dataset

You receive `online_orders.csv` with 5,000 orders. The data is **intentionally messy** – just like real employer data.

**Known issues:**
- 200 missing profit values
- 50 dates in wrong format
- Inconsistent category names ("Electronics", "electronics", "ELECTRONICS")
- 15 missing region values
- 20 rows with negative or zero quantity (data errors)
- 5 rows with "Small Business" segment (not in expected list)

### The Three Questions You Must Answer

| Question | What to Find | Chart Type |
|----------|--------------|------------|
| **Q1** | Which region has highest total profit? Lowest? | Bar chart |
| **Q2** | Within Electronics category, which customer segment has highest average profit per order? | Bar chart + table |
| **Q3** | Is profit trending upward, downward, or flat over 3 months? | Line chart + trend line |

### The Four Deliverables

| # | Deliverable | Format | Weight |
|---|-------------|--------|--------|
| 1 | Jupyter Notebook (cleaning + analysis + Q1-Q3) | `.ipynb` | 40% |
| 2 | Cleaned CSV | `.csv` | 10% |
| 3 | Tableau Dashboard (2 pages) | Public URL | 30% |
| 4 | Loom Video (3-5 min presentation) | URL | 20% |

---

## The New Dataset

### File Location
```
week4-capstone/data/online_orders.csv
```

### Column Descriptions

| Column | Type | Description | Issues |
|--------|------|-------------|--------|
| `order_id` | int | Unique ID | None |
| `order_date` | string | YYYY-MM-DD or MM/DD/YYYY | 50 wrong format |
| `region` | string | North, South, East, West | 15 missing |
| `category` | string | Electronics, Furniture, Office Supplies | Inconsistent casing |
| `customer_segment` | string | Consumer, Corporate, Home Office | 5 have "Small Business" |
| `sales` | float | Total sale amount | None |
| `profit` | float | Profit (can be negative) | 200 missing (NaN) |
| `quantity` | int | Number of items | 20 have ≤ 0 |

### First Look (Run This Yourself)

```python
import pandas as pd

df = pd.read_csv('week4-capstone/data/online_orders.csv')

print(f"Shape: {df.shape}")
print(f"\nMissing values:\n{df.isnull().sum()}")
print(f"\nFirst 5 rows:\n{df.head()}")
print(f"\nData types:\n{df.dtypes}")
```

---

## Step-by-Step Capstone Guide

### Step 1: Setup & Initial Exploration

**Create your notebook:** Start with `submission_template/yourname_capstone.ipynb`

**Cell 1: Import libraries**
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Set style for better looking plots
sns.set_style('whitegrid')
plt.rcParams['figure.figsize'] = (10, 6)
```

**Cell 2: Load data**
```python
df = pd.read_csv('../data/online_orders.csv')
print("Data loaded successfully!")
```

**Cell 3: Initial exploration**
```python
# Shape
print(f"Rows: {df.shape[0]}, Columns: {df.shape[1]}")

# Column names
print(f"\nColumns:\n{df.columns.tolist()}")

# Data types and missing
print(f"\nInfo:")
df.info()

# Statistical summary
print(f"\nDescribe:")
df.describe()

# Missing values count
print(f"\nMissing values per column:")
print(df.isnull().sum())

# Unique values in categorical columns
print(f"\nUnique regions: {df['region'].unique()}")
print(f"Unique categories: {df['category'].unique()}")
print(f"Unique segments: {df['customer_segment'].unique()}")
```

**Expected findings:**
- 5,000 rows, 8 columns
- Missing: profit (200), region (15)
- Inconsistent: category casing, date format
- Invalid: negative quantity, "Small Business" segment

---

### Step 2: Data Cleaning

**Cell 4: Create a clean dataset (copy to avoid warnings)**
```python
df_clean = df.copy()
print(f"Working with {len(df_clean)} rows")
```

**Cell 5: Fix column names (remove spaces, lowercase)**
```python
df_clean.columns = df_clean.columns.str.lower().str.replace(' ', '_')
print(df_clean.columns.tolist())
```

**Cell 6: Convert order_date to datetime**
```python
# Convert (errors become NaT - Not a Time)
df_clean['order_date'] = pd.to_datetime(df_clean['order_date'], errors='coerce')

# Check how many failed conversion
failed_dates = df_clean['order_date'].isnull().sum()
print(f"Failed date conversions: {failed_dates}")

# Drop rows where date conversion failed (50 rows)
df_clean = df_clean.dropna(subset=['order_date'])
print(f"Rows after fixing dates: {len(df_clean)}")
```

**Cell 7: Fix missing region values**
```python
# Check missing regions
print(f"Missing regions before: {df_clean['region'].isnull().sum()}")

# Option 1: Fill with 'Unknown' (or drop if few)
df_clean['region'] = df_clean['region'].fillna('Unknown')

# Option 2: Drop missing regions if <5% (your choice)
# df_clean = df_clean.dropna(subset=['region'])

print(f"Missing regions after: {df_clean['region'].isnull().sum()}")
```

**Cell 8: Fix inconsistent category names**
```python
# Before
print(f"Unique categories before: {df_clean['category'].unique()}")

# Convert to title case (first letter capital, rest lowercase)
df_clean['category'] = df_clean['category'].str.title()

# After
print(f"Unique categories after: {df_clean['category'].unique()}")
```

**Cell 9: Fix customer_segment (map 'Small Business' to 'Corporate' or create new)**
```python
# Before
print(f"Unique segments before: {df_clean['customer_segment'].unique()}")

# Map 'Small Business' to 'Corporate' (or keep as separate)
segment_map = {
    'Consumer': 'Consumer',
    'Corporate': 'Corporate',
    'Home Office': 'Home Office',
    'Small Business': 'Corporate'  # Map to Corporate
}
df_clean['customer_segment'] = df_clean['customer_segment'].map(segment_map)

# After
print(f"Unique segments after: {df_clean['customer_segment'].unique()}")
```

**Cell 10: Remove negative or zero quantity**
```python
# Before
print(f"Rows with quantity <= 0: {(df_clean['quantity'] <= 0).sum()}")

# Remove
df_clean = df_clean[df_clean['quantity'] > 0]

print(f"Rows after removing bad quantity: {len(df_clean)}")
```

**Cell 11: Handle missing profit values (most important cleaning step)**
```python
# Check missing profit count
missing_profit = df_clean['profit'].isnull().sum()
print(f"Missing profit values: {missing_profit}")

# Fill missing profit with median profit of that category
df_clean['profit'] = df_clean.groupby('category')['profit'].transform(
    lambda x: x.fillna(x.median())
)

# Verify no more missing
print(f"Missing profit after fill: {df_clean['profit'].isnull().sum()}")
```

**Cell 12: Remove duplicates if any**
```python
duplicates = df_clean.duplicated().sum()
print(f"Duplicate rows: {duplicates}")

df_clean = df_clean.drop_duplicates()
print(f"Rows after deduplication: {len(df_clean)}")
```

**Cell 13: Verify cleaning was successful**
```python
print("=== CLEANING VERIFICATION ===")
print(f"Final row count: {len(df_clean)}")
print(f"\nMissing values:\n{df_clean.isnull().sum()}")
print(f"\nData types:\n{df_clean.dtypes}")
print(f"\nSample of cleaned data:")
df_clean.head()
```

---

### Step 3: Answer Question 1 (Regional Performance)

**Question:** Which region has the highest total profit? Which has the lowest?

**Cell 14: Calculate total profit by region**
```python
# Group by region and sum profit
profit_by_region = df_clean.groupby('region')['profit'].sum().sort_values(ascending=False)

print("=== PROFIT BY REGION ===")
print(profit_by_region)

# Identify highest and lowest
highest_region = profit_by_region.index[0]
highest_profit = profit_by_region.iloc[0]
lowest_region = profit_by_region.index[-1]
lowest_profit = profit_by_region.iloc[-1]

print(f"\nHighest profit: {highest_region} with ${highest_profit:,.2f}")
print(f"Lowest profit: {lowest_region} with ${lowest_profit:,.2f}")
```

**Cell 15: Create bar chart**
```python
# Create bar chart
plt.figure(figsize=(10, 6))
colors = ['green' if x > 0 else 'red' for x in profit_by_region.values]
profit_by_region.plot(kind='bar', color=colors)

plt.title('Total Profit by Region', fontsize=16, fontweight='bold')
plt.xlabel('Region', fontsize=12)
plt.ylabel('Total Profit ($)', fontsize=12)
plt.axhline(y=0, color='black', linestyle='-', linewidth=0.5)

# Add value labels on bars
for i, (region, profit) in enumerate(profit_by_region.items()):
    plt.text(i, profit + (1000 if profit > 0 else -3000), 
             f'${profit:,.0f}', ha='center', fontweight='bold')

plt.tight_layout()
plt.show()
```

**Cell 16: Write interpretation**
```python
# Markdown cell - write your interpretation
"""
## Q1 Interpretation

The {highest_region} region generates the highest total profit at ${highest_profit:,.2f}, 
which is {profit_difference:,.0f}% higher than the second-ranked region.

The {lowest_region} region shows a net loss of ${abs(lowest_profit):,.2f}, 
likely due to [explain possible reasons based on data].
"""
```

---

### Step 4: Answer Question 2 (Category & Segment Analysis)

**Question:** Within the Electronics category only, which customer segment has the highest average profit per order?

**Cell 17: Filter to Electronics category**
```python
electronics_df = df_clean[df_clean['category'] == 'Electronics'].copy()
print(f"Electronics orders: {len(electronics_df)} rows")
```

**Cell 18: Calculate average profit by segment**
```python
# Group by segment and calculate average profit
avg_profit_by_segment = electronics_df.groupby('customer_segment')['profit'].mean().sort_values(ascending=False)

print("=== AVERAGE PROFIT BY SEGMENT (Electronics Only) ===")
print(avg_profit_by_segment)

# Identify highest segment
highest_segment = avg_profit_by_segment.index[0]
highest_avg_profit = avg_profit_by_segment.iloc[0]

print(f"\nHighest average profit: {highest_segment} with ${highest_avg_profit:.2f} per order")
```

**Cell 19: Create bar chart with error bars**
```python
# Create bar chart with error bars (standard deviation)
plt.figure(figsize=(10, 6))

# Calculate mean and std for each segment
segment_stats = electronics_df.groupby('customer_segment')['profit'].agg(['mean', 'std', 'count']).reset_index()

# Create bar plot
sns.barplot(data=segment_stats, x='customer_segment', y='mean', 
            yerr=segment_stats['std'], capsize=5, palette='viridis')

plt.title('Average Profit per Order by Customer Segment (Electronics Only)', fontsize=14, fontweight='bold')
plt.xlabel('Customer Segment', fontsize=12)
plt.ylabel('Average Profit ($)', fontsize=12)

# Add value labels
for i, row in segment_stats.iterrows():
    plt.text(i, row['mean'] + 2, f'${row["mean"]:.2f}', ha='center', fontweight='bold')

plt.tight_layout()
plt.show()
```

**Cell 20: Create summary table**
```python
# Create formatted table
summary_table = electronics_df.groupby('customer_segment').agg({
    'profit': ['mean', 'median', 'count', 'sum']
}).round(2)

# Rename columns
summary_table.columns = ['Avg Profit', 'Median Profit', 'Number of Orders', 'Total Profit']
summary_table['Avg Profit'] = summary_table['Avg Profit'].apply(lambda x: f'${x:.2f}')
summary_table['Median Profit'] = summary_table['Median Profit'].apply(lambda x: f'${x:.2f}')
summary_table['Total Profit'] = summary_table['Total Profit'].apply(lambda x: f'${x:,.2f}')

print("=== SUMMARY TABLE (Electronics Only) ===")
print(summary_table)
```

**Cell 21: Write interpretation**
```python
"""
## Q2 Interpretation

Within the Electronics category, the {highest_segment} segment has the highest average profit 
per order at ${highest_avg_profit:.2f}.

This is {percent_higher:.0f}% higher than the next highest segment.

Possible reasons: [Corporate customers may buy in bulk, higher-end products, etc.]
"""
```

---

### Step 5: Answer Question 3 (Time Trend)

**Question:** Over the 3-month period, is profit trending upward, downward, or flat?

**Cell 22: Prepare time series data**
```python
# Ensure order_date is datetime (already done in cleaning)
# Set date as index for time series operations
df_time = df_clean.set_index('order_date')

# Group by date and sum profit
daily_profit = df_time.groupby(df_time.index)['profit'].sum()

print(f"Date range: {daily_profit.index.min()} to {daily_profit.index.max()}")
print(f"Number of days: {len(daily_profit)}")
```

**Cell 23: Create line plot with trend line**
```python
# Create figure
plt.figure(figsize=(12, 6))

# Plot daily profit (semi-transparent)
plt.plot(daily_profit.index, daily_profit.values, alpha=0.3, label='Daily Profit', linewidth=1)

# Add 7-day rolling average
rolling_avg = daily_profit.rolling(window=7).mean()
plt.plot(rolling_avg.index, rolling_avg.values, color='red', linewidth=2, label='7-Day Rolling Average')

# Add trend line (linear regression)
from scipy import stats
x_numeric = np.arange(len(daily_profit))
slope, intercept, r_value, p_value, std_err = stats.linregress(x_numeric, daily_profit.values)
trend_line = intercept + slope * x_numeric
plt.plot(daily_profit.index, trend_line, 'g--', linewidth=2, label=f'Trend Line (slope: ${slope:.2f}/day)')

# Formatting
plt.title('Profit Trend Over Time', fontsize=16, fontweight='bold')
plt.xlabel('Date', fontsize=12)
plt.ylabel('Daily Profit ($)', fontsize=12)
plt.legend()
plt.axhline(y=0, color='gray', linestyle='-', linewidth=0.5)
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Determine trend direction
if slope > 0:
    trend_direction = "upward"
    trend_icon = "📈"
elif slope < 0:
    trend_direction = "downward"
    trend_icon = "📉"
else:
    trend_direction = "flat"
    trend_icon = "➡️"

print(f"{trend_icon} Profit trend is {trend_direction} with slope of ${slope:.2f} per day")
```

**Cell 24: Calculate percentage change**
```python
# Calculate total profit first month vs last month
first_month = daily_profit[daily_profit.index < '2024-02-01'].sum()
last_month = daily_profit[daily_profit.index >= '2024-03-01'].sum()
percent_change = ((last_month - first_month) / first_month) * 100

print(f"First month (Jan) profit: ${first_month:,.2f}")
print(f"Last month (Mar) profit: ${last_month:,.2f}")
print(f"Change: {percent_change:+.1f}%")
```

**Cell 25: Write interpretation**
```python
"""
## Q3 Interpretation

Over the 3-month period from January to March 2024, profit shows a {trend_direction} trend 
with a slope of ${slope:.2f} per day.

The first month (January) generated ${first_month:,.2f} in profit, 
while the last month (March) generated ${last_month:,.2f}, 
representing a {percent_change:+.1f}% change.

[Possible explanations: seasonal effects, marketing campaigns, new products, etc.]
"""
```

---

### Step 6: Export Cleaned Data

**Cell 26: Save cleaned CSV for Tableau**
```python
# Export to CSV (no index column)
df_clean.to_csv('cleaned_online_orders.csv', index=False)
print("Cleaned data saved to 'cleaned_online_orders.csv'")
print(f"Export shape: {df_clean.shape}")
```

---

### Step 7: Build Tableau Dashboard

**Now switch to Tableau Public.** Use the exported `cleaned_online_orders.csv`.

#### Dashboard Page 1: Executive Summary

**Sheets to create:**

**Sheet 1: KPI - Total Sales**
- Create calculated field: `SUM([sales])`
- Format as currency
- Add to dashboard as text

**Sheet 2: KPI - Total Profit**
- Create calculated field: `SUM([profit])`
- Format as currency (red if negative)

**Sheet 3: KPI - Average Profit per Order**
- Create calculated field: `AVG([profit])`
- Format as currency

**Sheet 4: Profit by Region (Bar Chart)**
- Drag `region` to Columns
- Drag `profit` to Rows
- Sort descending
- Color: green for positive, red for negative

**Sheet 5: Sales by Category (Bar Chart)**
- Drag `category` to Columns
- Drag `sales` to Rows
- Sort descending

**Sheet 6: Date Range Filter**
- Drag `order_date` to Filters
- Choose "Range of dates"
- Show filter

**Dashboard 1 Layout:**
```
┌─────────────────────────────────────────────────────┐
│  Executive Dashboard - Q1 2024                      │
├─────────────────────────────────────────────────────┤
│  [Date Range Filter]                                │
├──────────────┬──────────────┬──────────────────────┤
│  Total Sales │ Total Profit │ Avg Profit/Order     │
│   $XXX,XXX   │   $XX,XXX    │      $XX.XX          │
├──────────────┴──────────────┴──────────────────────┤
│                                                     │
│  Profit by Region           Sales by Category      │
│  ┌─────────────────┐        ┌─────────────────┐    │
│  │ ████ North      │        │ ████ Electronics│    │
│  │ ███ West        │        │ ███ Furniture   │    │
│  │ ██ East         │        │ ██ Office       │    │
│  │ █ South (loss)  │        │                 │    │
│  └─────────────────┘        └─────────────────┘    │
│                                                     │
└─────────────────────────────────────────────────────┘
```

#### Dashboard Page 2: Deep Dive

**Sheets to create:**

**Sheet 7: Profit Over Time (Line Chart)**
- Drag `order_date` to Columns → right-click → Month
- Drag `profit` to Rows
- Add `category` to Color

**Sheet 8: Sales vs Profit (Scatter Plot)**
- Drag `sales` to Columns
- Drag `profit` to Rows
- Drag `region` to Color
- Drag `quantity` to Size

**Sheet 9: Profit Heatmap by Region & Category**
- Drag `region` to Rows
- Drag `category` to Columns
- Drag `profit` to Color (as SUM)
- Change mark type to Square

**Sheet 10: Region Filter**
- Drag `region` to Filters
- Show as dropdown

**Dashboard 2 Layout:**
```
┌─────────────────────────────────────────────────────┐
│  Deep Dive Analysis                                 │
├─────────────────────────────────────────────────────┤
│  [Region Filter ▼]                                  │
├─────────────────────────────────────────────────────┤
│                                                     │
│  Profit Over Time by Category                       │
│  ┌─────────────────────────────────────────────┐   │
│  │     ── Electronics                           │   │
│  │    ── Furniture                              │   │
│  │   ── Office Supplies                         │   │
│  └─────────────────────────────────────────────┘   │
│                                                     │
│  Sales vs Profit                Profit Heatmap      │
│  ┌──────────────────┐          ┌──────────────┐    │
│  │  •  •            │          │ North  ████  │    │
│  │    •    •        │          │ East   ██    │    │
│  │  •    •          │          │ West   ███   │    │
│  └──────────────────┘          └──────────────┘    │
│                                                     │
└─────────────────────────────────────────────────────┘
```

**Add Dashboard Action:**
1. Dashboard → Actions → Add Action → Filter
2. Source: Profit by Region (Sheet 4)
3. Target: All sheets on Page 2
4. Run action on: Select

**Publish:**
- File → Save to Tableau Public As...
- Name: `YourName_Capstone_Dashboard`
- Copy the share URL

---

### Step 8: Record Loom Video

**Video structure (3-5 minutes total):**

**Segment 1: Cleaned Data (30 seconds)**
```
"Here's my cleaned dataset. I started with 5,000 rows and 200 missing profit values. 
I filled missing profits with the median profit for each category, fixed 50 date errors, 
and removed 20 rows with invalid quantities. The final cleaned data has X rows."
```
- Show the CSV file open in Excel or Jupyter

**Segment 2: Python Code (1-2 minutes)**
```
"Let me show my Python code for Question 2. I filtered to Electronics only, 
then grouped by customer segment to calculate average profit. 
The Corporate segment has the highest average at $87.50 per order."
```
- Show your Jupyter notebook
- Point to specific lines of code
- Explain what the code does (don't just read it)

**Segment 3: Tableau Dashboard (1-2 minutes)**
```
"Here's my Tableau dashboard. On Page 1, you can see profit by region – 
North is highest at $45,000. When I click on North, the charts on Page 2 update. 
On the scatter plot, you can see that higher sales don't always mean higher profit."
```
- Open your published dashboard
- Demonstrate a filter or action
- State one specific insight

**Segment 4: Reflection (30 seconds)**
```
"If I had one more week, I would analyze why the South region is losing money, 
and look at product-level profitability to identify specific items to discontinue."
```

**Recording tips:**
- Practice once before recording
- Speak clearly and slowly
- Use a script if nervous
- Close other tabs/applications
- Test your microphone first

---

### Step 9: Submit via GitHub

**Step-by-step submission:**

```bash
# 1. Navigate to your repo folder
cd data-analytics-pilot

# 2. Copy your files to submission_template
cp yourname_capstone.ipynb week4-capstone/submission_template/
cp cleaned_online_orders.csv week4-capstone/submission_template/
echo "https://public.tableau.com/views/YourDashboard" > week4-capstone/submission_template/tableau_link.txt
echo "https://www.loom.com/share/your-video-id" > week4-capstone/submission_template/loom_link.txt

# 3. Add files to git
git add week4-capstone/submission_template/*

# 4. Commit
git commit -m "submit capstone - Your Name"

# 5. Push to your fork
git push origin main

# 6. Open Pull Request on GitHub
# - Go to original repo
# - Click Pull Requests → New Pull Request
# - Compare across forks
# - Choose your fork and branch
# - Add Loom link in description
# - Submit
```

---

## Grading Rubric

### Total Points: 40

| Category | Points | Excellent (full) | Satisfactory (partial) | Missing (0) |
|----------|--------|------------------|------------------------|-------------|
| **Data Cleaning** | 10 | All 5 issues fixed, no data loss | 3-4 issues fixed | 2 or fewer fixed |
| **Q1: Regional Profit** | 5 | Bar chart + correct interpretation | Chart only | Missing |
| **Q2: Category/Segment** | 5 | Bar chart + table + interpretation | Chart only | Missing |
| **Q3: Time Trend** | 5 | Line plot + trend line + conclusion | Plot only | Missing |
| **Tableau Dashboard** | 10 | 2 pages, filters, actions, professional | 1 page or missing filters | Dashboard missing |
| **Loom Video** | 5 | Covers 4 segments, clear audio, 3-5 min | Covers 2-3 segments | Video missing |

**Passing threshold:** 28/40 (70%)

---

## Common Pitfalls & How to Avoid Them

### Pitfall #1: Over-cleaning (spending 4 hours on perfect data)

**Problem:** Trying to handle every edge case, every missing value perfectly.

**Solution:** 
- If <5% of rows have an issue → drop them
- If >20% have issues → fill with median/mode
- **Done is better than perfect**

### Pitfall #2: Forgetting to export cleaned CSV

**Problem:** You clean the data in Python but Tableau uses the original messy file.

**Solution:** 
```python
df_clean.to_csv('cleaned_online_orders.csv', index=False)
```
Do this IMMEDIATELY after cleaning, before analysis.

### Pitfall #3: Tableau dashboard too cluttered

**Problem:** 10 sheets, 8 filters, 5 colors – users are overwhelmed.

**Solution:**
- 3-5 sheets per dashboard max
- 2-3 filters max
- One clear insight per chart
- **Less is more**

### Pitfall #4: Loom video too long or too short

**Problem:** 10-minute ramble or 1-minute rushed video.

**Solution:**
- Write a script (60-90 seconds per segment)
- Practice once
- Aim for 4 minutes (safe zone)
- **Time yourself**

### Pitfall #5: Missing profit filled incorrectly

**Problem:** Filling all missing profit with overall median (ignores category differences).

**Solution:**
```python
# Correct - by category
df['profit'] = df.groupby('category')['profit'].transform(
    lambda x: x.fillna(x.median())
)

# Wrong - overall median
df['profit'] = df['profit'].fillna(df['profit'].median())
```

### Pitfall #6: Not handling negative profit in charts

**Problem:** South region has negative profit, but bar chart shows it as positive bar going up.

**Solution:**
```python
colors = ['green' if x > 0 else 'red' for x in profit_by_region]
profit_by_region.plot(kind='bar', color=colors)
plt.axhline(y=0, color='black')
```

### Pitfall #7: Forgetting to set index=False when exporting

**Problem:** CSV has an extra "Unnamed: 0" column.

**Solution:**
```python
df.to_csv('clean.csv', index=False)  # Always add index=False
```

---

## Sample Solutions

### Sample Q1 Answer

**Python output:**
```
=== PROFIT BY REGION ===
region
North     $45,200
West      $32,500
East      $18,300
South     -$2,100
Name: profit, dtype: int64
```

**Interpretation:**
> The North region generates the highest total profit at $45,200, which is 39% higher than the second-ranked West region ($32,500). The South region shows a net loss of -$2,100, driven by high shipping costs and lower average order values compared to other regions.

You are correct again – the response was **cut off mid-sentence**. Let me complete **Sample Q2 Answer** and finish the rest of the Week 4 Class Notes properly.

---

### Sample Q2 Answer 

**Python output:**
```
=== AVERAGE PROFIT BY SEGMENT (Electronics Only) ===
customer_segment
Corporate       $87.50
Consumer        $42.30
Home Office     $38.20
Name: profit, dtype: float64
```

**Interpretation:**
> Within the Electronics category, the Corporate segment has the highest average profit per order at $87.50. This is 107% higher than the Consumer segment ($42.30) and 129% higher than the Home Office segment ($38.20). Corporate customers likely purchase higher-end electronics in larger quantities, driving higher per-order profitability.

---

### Sample Q3 Answer

**Python output:**
```
📈 Profit trend is upward with slope of $12.45 per day

First month (Jan) profit: $8,450.00
Last month (Mar) profit: $12,890.00
Change: +52.5%
```

**Interpretation:**
> Over the 3-month period from January to March 2024, profit shows an upward trend with a slope of $12.45 per day. Total profit increased from $8,450 in January to $12,890 in March, representing a 52.5% growth. This positive trend may be attributed to increased marketing spend in Q1 or seasonal demand for electronics.

---

### Sample Loom Video Script

**Segment 1: Cleaned Data (30 seconds)**
> "Here's my cleaned dataset. I started with 5,000 rows of messy order data. The main issues were 200 missing profit values, 50 incorrectly formatted dates, inconsistent category names, and 20 rows with negative quantities. I fixed these by filling missing profits with the median profit for each category, converting all dates to datetime format, standardizing category names to title case, and removing invalid quantity rows. The final cleaned dataset has 4,850 rows ready for analysis."

**Segment 2: Python Code (90 seconds)**
> "Let me show my Python code for Question 2, which asks which customer segment has the highest average profit for Electronics. First, I filtered the DataFrame to only Electronics category using `df[df['category'] == 'Electronics']`. Then I used `groupby('customer_segment')['profit'].mean()` to calculate average profit per segment. The result shows Corporate customers average $87.50 per order, which is much higher than Consumer at $42.30. I also created a bar chart with error bars to visualize the differences and show variability within each segment."

**Segment 3: Tableau Dashboard (90 seconds)**
> "Here's my Tableau dashboard published online. Page 1 is the Executive Summary. The key takeaway is that North region generates $45,200 in profit, while South shows a loss. The KPI cards show total sales of $412,000 and average profit per order of $28.50. When I use the date filter, all charts update. Page 2 is the Deep Dive. I've added a region filter here – when I select North, you can see the profit trend line spikes in February. The scatter plot shows that higher sales don't always mean higher profit – some high-sales orders actually lost money."

**Segment 4: Reflection (30 seconds)**
> "If I had one more week with this data, I would analyze why the South region is losing money. I'd look at shipping costs by region and product-level profitability to identify specific items to discontinue or reprice. I'd also build a forecasting model to predict next quarter's profit based on this upward trend."

---

## Time Management Plan

### 8-Hour Capstone Schedule

| Day | Time | Task | Estimated Hours |
|-----|------|------|-----------------|
| **Tuesday** | Evening | Attend kickoff, download data, initial exploration | 1.5 |
| **Wednesday** | Morning/Afternoon | Data cleaning (Cells 4-13) | 2 |
| **Thursday** | Morning | Answer Q1 and Q2 (Cells 14-21) | 1.5 |
| **Thursday** | Afternoon | Answer Q3 (Cells 22-25) + export CSV | 1 |
| **Friday** | Evening | Build Tableau dashboard (Page 1) | 1 |
| **Saturday** | Morning | Build Tableau dashboard (Page 2) + actions | 1 |
| **Saturday** | Afternoon | Record Loom video (practice + final) | 0.5 |
| **Sunday** | Morning | Final checks, submit via GitHub | 0.5 |
| **Total** | | | **9 hours** |

**Pro tip:** Don't leave Tableau for Sunday night. Start Friday evening so you can ask questions in Saturday office hours.

---

## Final Checklist

### Before You Submit (Go Through This!)

#### Python Notebook
- [ ] Kernel restarted and "Run All" completes without errors
- [ ] All 3 questions have code + chart + interpretation sentence
- [ ] Missing profit values filled by category (not overall median)
- [ ] Dates converted to datetime with `pd.to_datetime()`
- [ ] Categories standardized (all title case)
- [ ] Negative/zero quantity rows removed
- [ ] `cleaned_online_orders.csv` exported with `index=False`
- [ ] Reflection section has 3-5 sentences
- [ ] AI/code sources cited (if used)

#### Tableau Dashboard
- [ ] Dashboard has 2 pages (named "Executive Summary" and "Deep Dive")
- [ ] Page 1 has: 3 KPI cards + 2 bar charts + 1 date filter
- [ ] Page 2 has: 1 line chart + 1 scatter plot + 1 heatmap + 1 region filter
- [ ] At least 1 dashboard action works (click bar → filter other charts)
- [ ] Dashboard is published to Tableau Public
- [ ] Link works in incognito mode (no login required)
- [ ] Link saved in `tableau_link.txt`

#### Loom Video
- [ ] Video length: 3-5 minutes (not 2, not 6+)
- [ ] Covers: cleaned data (30s) + Python code (1-2 min) + Tableau (1-2 min) + reflection (30s)
- [ ] Audio is clear (no background noise)
- [ ] Link is "Unlisted" (not "Public" and not "Private")
- [ ] Link opens correctly
- [ ] Link saved in `loom_link.txt`

#### Submission
- [ ] All files in `submission_template/` folder:
  - `yourname_capstone.ipynb` (replace "yourname" with actual name)
  - `cleaned_online_orders.csv`
  - `tableau_link.txt` (contains one URL)
  - `loom_link.txt` (contains one URL)
- [ ] Git commit message: `"submit capstone - Your Name"`
- [ ] Pull Request opened against original repo
- [ ] PR description contains your Loom link (so instructor can watch without downloading)

---

## Key Takeaways from the Pilot

### What You've Accomplished

**Week 1: Python Fundamentals**
- ✅ Write Python code from scratch
- ✅ Use variables, lists, loops, and functions
- ✅ Read and process CSV files

**Week 2: Data Manipulation with Pandas**
- ✅ Load and explore any dataset
- ✅ Clean messy data (missing values, inconsistent text, wrong types)
- ✅ Group, aggregate, and merge data
- ✅ Export clean data for visualization

**Week 3: Visualization & Tableau**
- ✅ Create professional charts in Python (Matplotlib/Seaborn)
- ✅ Build interactive dashboards in Tableau
- ✅ Publish and share work online

**Week 4: Capstone Project**
- ✅ Apply all skills to a real-world messy dataset
- ✅ Work independently from vague requirements
- ✅ Present findings to stakeholders (via Loom)
- ✅ Create a portfolio piece

### The Data Analytics Workflow (You Now Know)

```
Step 1: Get Data
    ↓ (CSV, Excel, database)
Step 2: Clean Data (Pandas)
    ↓ (handle missing, fix types, remove duplicates)
Step 3: Explore & Analyze (Pandas + Python plots)
    ↓ (groupby, aggregate, find patterns)
Step 4: Visualize & Present (Tableau)
    ↓ (dashboards, filters, actions)
Step 5: Share Insights (Loom, email, presentation)
    ↓
Your Manager Makes a Decision
```

### What's Next After the Pilot?

**Your Academy's Paid Programs:**

| Course | Topics | Prerequisite |
|--------|--------|--------------|
| **Data Analytics Pro** (6 weeks) | SQL, advanced statistics, A/B testing, Tableau LOD | This pilot |
| **Applied Data Science** (8 weeks) | Machine learning, scikit-learn, regression, classification | Data Analytics Pro |
| **Data Engineering** (10 weeks) | ETL pipelines, Airflow, dbt, cloud (AWS/GCP) | Applied Data Science |

**20% discount** for all pilot graduates.

### Final Words from Instructor

> "You started Week 1 not knowing what a variable was. You now clean messy datasets, write Python scripts, build Tableau dashboards, and present insights like a junior analyst.

> **That's not nothing. That's a career skill.**

> The capstone isn't just a grade – it's your first portfolio piece. Put the dashboard link on your LinkedIn. Talk about it in interviews. 'I took a messy dataset of 5,000 orders, cleaned it, found that the Corporate segment drives 60% of Electronics profit, and built an interactive dashboard for management.'

> **You belong in this field.**

> Thank you for being part of the pilot. Your feedback will shape this course for future students. Now go submit that capstone – and then celebrate. You've earned it."

---

## Office Hours & Support (Final Week)

- **Slack:** `#capstone-help` (instructor response within 4 hours)
- **Office hours:** Saturday 11 AM–1 PM ET (extended for capstone)
- **Emergency:** augamos@live.com (only for tech issues)

---

**End of Week 4 Class Notes**

*Save this document. Then go finish your capstone.*

---

## Complete Week 4 Notes Summary

| Section | Key Topics |
|---------|------------|
| Course Review (Weeks 1-3) | Python, Pandas, Matplotlib, Seaborn, Tableau |
| Capstone Overview | Scenario, dataset, 3 questions, 4 deliverables |
| The New Dataset | 5,000 rows, 8 columns, known issues |
| Step-by-Step Guide | 9 steps from setup to submission |
| Grading Rubric | 40 points, 70% to pass |
| Common Pitfalls | 7 mistakes and how to avoid them |
| Sample Solutions | Q1, Q2, Q3 answers + video script |
| Time Management | 9-hour plan across 5 days |
| Final Checklist | 30+ items to verify before submitting |
| Key Takeaways | What you learned + what's next |

**Total length:** ~6,000 words, ~50 code blocks, complete capstone guide

---

**Would you like me to generate any of the following to complete your course materials:**

1. **Exercise notebooks for Week 3** (`exercise1_charts_from_cleaned_data.ipynb`)
2. **Tableau Guide** (`tableau_guide.md` with step-by-step screenshots described)
3. **Sample `online_orders.csv`** (the messy dataset for Week 4 capstone)
4. **Instructor Grading Guide** (with answer key and common student mistakes)
5. **Certificate of Completion template** (for pilot graduates)

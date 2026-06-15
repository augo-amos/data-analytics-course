# Week 4 Class Notes: Capstone Project

**Course:** Decodemy – Foundations of Data Analytics (Pilot)  
**Week:** 4 of 4 (Final Week)  
**Prerequisites:** Weeks 1, 2, and 3 completed  
**Instructor:** [Your Name]

---

## Table of Contents

1. [Course Review: Weeks 1-3](#course-review-weeks-1-3)
2. [Capstone Project Overview](#capstone-project-overview)
3. [The New Dataset (5,000 Rows)](#the-new-dataset-5000-rows)
4. [Step-by-Step Capstone Guide](#step-by-step-capstone-guide)
   - [Step 1: Setup & Initial Exploration](#step-1-setup--initial-exploration)
   - [Step 2: Data Cleaning (Anticipating Issues)](#step-2-data-cleaning-anticipating-issues)
   - [Step 3: Answer Question 1 (Regional Performance)](#step-3-answer-question-1-regional-performance)
   - [Step 4: Answer Question 2 (Category & Segment Analysis)](#step-4-answer-question-2-category--segment-analysis)
   - [Step 5: Answer Question 3 (Time Trend)](#step-5-answer-question-3-time-trend)
   - [Step 6: Export Cleaned Data](#step-6-export-cleaned-data)
   - [Step 7: Build Tableau Dashboard](#step-7-build-tableau-dashboard)
   - [Step 8: Record Video Presentation](#step-8-record-video-presentation)
   - [Step 9: Submit via GitHub](#step-9-submit-via-github)
5. [Grading Rubric](#grading-rubric)
6. [Common Pitfalls & How to Avoid Them](#common-pitfalls--how-to-avoid-them)
7. [Expected Outputs & Sample Solutions](#expected-outputs--sample-solutions)
8. [Time Management Plan](#time-management-plan)
9. [Final Checklist](#final-checklist)
10. [Key Takeaways from the Pilot](#key-takeaways-from-the-pilot)

---

## Course Review: Weeks 1-3

Before diving into the capstone, let's review what you've learned. **You will need all of these skills this week.**

### Week 1: Python Fundamentals

**What you learned:**
- Variables and data types (int, float, str, bool)
- Lists and list operations
- Loops (`for` and `while`)
- Conditionals (`if`/`elif`/`else`)
- Functions (`def`, parameters, `return`)
- Reading CSV files with Python's `csv` module

**Why this matters for the capstone:** You'll write functions to organize your cleaning code.

### Week 2: Data Manipulation with Pandas

**What you learned:**
- Series and DataFrames
- Reading data: `pd.read_csv()`
- Exploring data: `.head()`, `.info()`, `.describe()`
- Selecting columns and filtering rows
- Handling missing values: `.isnull()`, `.fillna()`, `.dropna()`
- Grouping and aggregation: `.groupby()`, `.agg()`
- Exporting data: `.to_csv()`

**Why this matters for the capstone:** **This is the most important week for the capstone.** You'll spend 60% of your time cleaning the new dataset with Pandas.

### Week 3: Visualization & Tableau

**What you learned:**
- Matplotlib and Seaborn for Python charts
- Tableau for interactive dashboards
- Building bar charts, line charts, scatter plots
- Creating calculated fields and filters
- Publishing dashboards to Tableau Public

**Why this matters for the capstone:** You'll create Python charts for exploration and a Tableau dashboard for the final deliverable.

---

## Capstone Project Overview

### The Scenario

You are a junior data analyst at **ShopFast**, an online retailer selling electronics, furniture, and office supplies. Your manager needs a clear picture of sales performance across regions and customer segments.

### The Dataset

You receive `online_orders.csv` with **5,000 orders**. The data is **intentionally messy** – just like real employer data.

| Issue | Expected Count | How to Identify |
|-------|----------------|-----------------|
| Missing profit values | ~200 | `df['profit'].isnull().sum()` |
| Wrong date format | ~50 | Dates like `01/16/2024` instead of `2024-01-16` |
| Missing region values | ~15 | Empty string in region column |
| Negative/zero quantity | ~20 | `df['quantity'] <= 0` |
| "Small Business" segment | ~5 | `df['customer_segment'] == 'Small Business'` |
| Inconsistent category casing | ~100 | Mix of "Electronics", "electronics", "ELECTRONICS" |

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
| 4 | Video Presentation (3-5 min) | URL | 20% |

---

## The New Dataset (5,000 Rows)

### File Location
```
week4-capstone/data/online_orders.csv
```

### Column Descriptions

| Column | Type | Description | Issues to Expect |
|--------|------|-------------|------------------|
| `order_id` | int | Unique ID | None |
| `order_date` | object | Order date | 50 rows in MM/DD/YYYY format |
| `region` | object | North, South, East, West | 15 missing (empty strings) |
| `category` | object | Electronics, Furniture, Office Supplies | Inconsistent casing |
| `customer_segment` | object | Consumer, Corporate, Home Office | 5 "Small Business" values |
| `sales` | float | Total sale amount | None |
| `profit` | float | Profit (can be negative) | 200 missing (NaN) |
| `quantity` | int | Number of items | 20 rows with ≤ 0 |

### First Look (Run This Yourself)

```python
import pandas as pd

df = pd.read_csv('../data/online_orders.csv')

print(f"Shape: {df.shape}")
print(f"\nMissing values:\n{df.isnull().sum()}")
print(f"\nFirst 5 rows:\n{df.head()}")
print(f"\nUnique categories:\n{df['category'].unique()}")
```

**Expected output after running:**
```
Shape: (5000, 8)

Missing values:
order_id             0
order_date           0
region              15
category             0
customer_segment     0
sales                0
profit             200
quantity             0

Unique categories:
['Electronics' 'electronics' 'ELECTRONICS' 'Furniture' 'Office Supplies']
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

print("Libraries imported successfully!")
```

**Cell 2: Load data**
```python
df = pd.read_csv('../data/online_orders.csv')
print(f"Data loaded: {df.shape[0]} rows, {df.shape[1]} columns")
```

**Cell 3: Initial exploration**
```python
# First 5 rows
print("=== FIRST 5 ROWS ===")
print(df.head())

# Data types and missing values
print("\n=== DATA TYPES & MISSING VALUES ===")
print(df.info())

# Missing values count
print("\n=== MISSING VALUES COUNT ===")
print(df.isnull().sum())

# Statistical summary
print("\n=== STATISTICAL SUMMARY ===")
print(df.describe())

# Unique values in categorical columns
print("\n=== UNIQUE VALUES ===")
print(f"Regions: {df['region'].unique()[:10]}")  # Show first 10
print(f"Categories: {df['category'].unique()}")
print(f"Segments: {df['customer_segment'].unique()}")
```

**What students should discover:**
- 5,000 rows, 8 columns
- 200 missing profit values (4% of data)
- 15 missing region values
- Inconsistent category casing (3 variations of "Electronics")
- "Small Business" segment (not in standard list)
- Date column is object type (needs conversion)

---

### Step 2: Data Cleaning (Anticipating Issues)

**Cell 4: Create working copy**
```python
df_clean = df.copy()
print(f"Starting with {len(df_clean)} rows")
```

**Issue 1: Column names with spaces (if any)**
```python
# Check for spaces in column names
print("Original column names:", df_clean.columns.tolist())

# Fix: replace spaces with underscores and lowercase
df_clean.columns = df_clean.columns.str.lower().str.replace(' ', '_')
print("Fixed column names:", df_clean.columns.tolist())
```

**Issue 2: Wrong date formats (~50 rows)**
```python
# Check current date format sample
print("Sample dates before conversion:")
print(df_clean['order_date'].head(10))

# Convert to datetime (errors become NaT)
df_clean['order_date'] = pd.to_datetime(df_clean['order_date'], errors='coerce')

# Count how many failed
failed_dates = df_clean['order_date'].isnull().sum()
print(f"Failed date conversions: {failed_dates}")

# Drop rows where date conversion failed (the ~50 wrong format rows)
df_clean = df_clean.dropna(subset=['order_date'])
print(f"Rows after fixing dates: {len(df_clean)}")

# Verify dates are now correct
print("Sample dates after conversion:")
print(df_clean['order_date'].head(10))
```

**What students will see:**
- Some dates like `01/16/2024` will fail conversion
- Approximately 50 rows will be dropped
- Remaining dates are in proper datetime format

**Issue 3: Missing region values (~15 rows)**
```python
# Check missing regions
missing_before = df_clean['region'].isnull().sum()
print(f"Missing regions before: {missing_before}")

# Show sample of missing region rows
print("\nRows with missing region:")
print(df_clean[df_clean['region'].isnull()].head())

# Option 1: Fill with 'Unknown' (recommended for only 15 rows)
df_clean['region'] = df_clean['region'].fillna('Unknown')

# Verify
print(f"\nMissing regions after: {df_clean['region'].isnull().sum()}")
print(f"Unique regions now: {df_clean['region'].unique()}")
```

**Issue 4: Inconsistent category casing (~100 rows)**
```python
# Check unique categories before fixing
print("Unique categories BEFORE:")
print(df_clean['category'].unique())

# Show sample of inconsistent categories
print("\nSample of inconsistent category rows:")
print(df_clean[df_clean['category'].str.contains('Electronics', case=False, na=False)].head(10))

# Fix: convert to title case (first letter capital, rest lowercase)
df_clean['category'] = df_clean['category'].str.title()

# Verify
print("\nUnique categories AFTER:")
print(df_clean['category'].unique())
```

**Issue 5: "Small Business" segment (~5 rows)**
```python
# Check segments before
print("Unique segments BEFORE:")
print(df_clean['customer_segment'].unique())

# Count Small Business rows
small_biz_count = (df_clean['customer_segment'] == 'Small Business').sum()
print(f"Rows with 'Small Business': {small_biz_count}")

# Show sample
print("\nSample of Small Business rows:")
print(df_clean[df_clean['customer_segment'] == 'Small Business'].head())

# Create mapping dictionary
segment_map = {
    'Consumer': 'Consumer',
    'Corporate': 'Corporate',
    'Home Office': 'Home Office',
    'Small Business': 'Corporate'  # Map to Corporate
}

# Apply mapping
df_clean['customer_segment'] = df_clean['customer_segment'].map(segment_map)

# Verify
print("\nUnique segments AFTER:")
print(df_clean['customer_segment'].unique())
```

**Issue 6: Negative or zero quantity (~20 rows)**
```python
# Check quantity issues
print(f"Rows with quantity <= 0: {(df_clean['quantity'] <= 0).sum()}")

# Show sample of bad quantity rows
print("\nSample of rows with quantity <= 0:")
print(df_clean[df_clean['quantity'] <= 0].head(10))

# Remove bad quantity rows
df_clean = df_clean[df_clean['quantity'] > 0]

print(f"\nRows after removing bad quantity: {len(df_clean)}")
```

**Issue 7: Missing profit values (~200 rows) – MOST IMPORTANT**
```python
# Check missing profit
missing_profit_before = df_clean['profit'].isnull().sum()
print(f"Missing profit values before: {missing_profit_before}")

# Show sample of missing profit rows
print("\nSample of rows with missing profit:")
print(df_clean[df_clean['profit'].isnull()].head(10))

# Calculate median profit by category (for filling)
category_medians = df_clean.groupby('category')['profit'].median()
print("\nMedian profit by category:")
print(category_medians)

# Fill missing profit with median profit of that category
df_clean['profit'] = df_clean.groupby('category')['profit'].transform(
    lambda x: x.fillna(x.median())
)

# Verify no more missing
print(f"\nMissing profit after fill: {df_clean['profit'].isnull().sum()}")
```

**Issue 8: Duplicate rows (if any)**
```python
# Check for duplicates
duplicates = df_clean.duplicated().sum()
print(f"Duplicate rows: {duplicates}")

if duplicates > 0:
    df_clean = df_clean.drop_duplicates()
    print(f"Rows after deduplication: {len(df_clean)}")
else:
    print("No duplicates found.")
```

**Cell 13: Verify cleaning was successful**
```python
print("=== CLEANING VERIFICATION ===")
print(f"Original rows: {len(df)}")
print(f"Final rows: {len(df_clean)}")
print(f"Rows removed: {len(df) - len(df_clean)}")

print("\n=== MISSING VALUES AFTER CLEANING ===")
print(df_clean.isnull().sum())

print("\n=== DATA TYPES AFTER CLEANING ===")
print(df_clean.dtypes)

print("\n=== UNIQUE VALUES AFTER CLEANING ===")
print(f"Regions: {df_clean['region'].unique()}")
print(f"Categories: {df_clean['category'].unique()}")
print(f"Segments: {df_clean['customer_segment'].unique()}")

print("\n=== SAMPLE OF CLEANED DATA ===")
df_clean.head()
```

**Expected cleaning results:**
- Original: 5,000 rows
- After removing bad dates (~50), bad quantity (~20), duplicates (~5): ~4,925 rows
- No missing values in any column
- All categories in title case
- All segments standardized
- All dates in datetime format

---

### Step 3: Answer Question 1 (Regional Performance)

**Question:** Which region has the highest total profit? Which has the lowest?

**Cell 14: Calculate total profit by region**
```python
# Group by region and sum profit, sort descending
profit_by_region = df_clean.groupby('region')['profit'].sum().sort_values(ascending=False)

print("=== PROFIT BY REGION ===")
print(profit_by_region)

# Identify highest and lowest
highest_region = profit_by_region.index[0]
highest_profit = profit_by_region.iloc[0]
lowest_region = profit_by_region.index[-1]
lowest_profit = profit_by_region.iloc[-1]

print(f"\n🏆 Highest profit: {highest_region} with ${highest_profit:,.2f}")
print(f"⚠️ Lowest profit: {lowest_region} with ${lowest_profit:,.2f}")
```

**Cell 15: Create bar chart (Matplotlib)**
```python
# Create bar chart with custom colors
plt.figure(figsize=(10, 6))

# Color bars: green for positive, red for negative
colors = ['green' if x > 0 else 'red' for x in profit_by_region.values]

# Create bars
bars = plt.bar(profit_by_region.index, profit_by_region.values, color=colors)

# Add horizontal line at zero
plt.axhline(y=0, color='black', linestyle='-', linewidth=1)

# Labels and title
plt.title('Total Profit by Region', fontsize=16, fontweight='bold')
plt.xlabel('Region', fontsize=12)
plt.ylabel('Total Profit ($)', fontsize=12)

# Add value labels on bars
for i, (region, profit) in enumerate(profit_by_region.items()):
    y_offset = 500 if profit > 0 else -3000
    plt.text(i, profit + y_offset, f'${profit:,.0f}', 
             ha='center', fontweight='bold', fontsize=10)

plt.tight_layout()
plt.show()
```

**Alternative: Create bar chart (Seaborn)**
```python
# Alternative using seaborn
plt.figure(figsize=(10, 6))
sns.barplot(x=profit_by_region.index, y=profit_by_region.values, 
            palette=['green' if x > 0 else 'red' for x in profit_by_region.values])

plt.title('Total Profit by Region', fontsize=16, fontweight='bold')
plt.xlabel('Region', fontsize=12)
plt.ylabel('Total Profit ($)', fontsize=12)
plt.axhline(y=0, color='black', linestyle='-', linewidth=0.5)

# Add value labels
for i, profit in enumerate(profit_by_region.values):
    plt.text(i, profit + (500 if profit > 0 else -3000), f'${profit:,.0f}', 
             ha='center', fontweight='bold')

plt.tight_layout()
plt.show()
```

**Cell 16: Write interpretation (Markdown cell)**
```markdown
## Q1 Interpretation

The **North** region generates the highest total profit at **$45,200**, 
which is 39% higher than the second-ranked West region ($32,500).

The **South** region shows a net loss of **-$2,100**, 
the only region with negative total profit. 

**Possible reasons for South region loss:**
- Higher shipping costs to this region
- Different product mix with lower margins
- More promotional discounts or returns

**Recommendation:** Investigate South region operations to identify 
profitability drivers and loss sources before expanding further.
```

---

### Step 4: Answer Question 2 (Category & Segment Analysis)

**Question:** Within the Electronics category only, which customer segment has the highest average profit per order?

**Cell 17: Filter to Electronics category**
```python
# Filter to Electronics only
electronics_df = df_clean[df_clean['category'] == 'Electronics'].copy()

print(f"Total orders: {len(df_clean)}")
print(f"Electronics orders: {len(electronics_df)}")
print(f"Electronics as % of total: {len(electronics_df)/len(df_clean)*100:.1f}%")
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

print(f"\n🏆 Highest average profit: {highest_segment} with ${highest_avg_profit:.2f} per order")
```

**Cell 19: Create bar chart with error bars (Matplotlib)**
```python
# Calculate statistics for error bars
segment_stats = electronics_df.groupby('customer_segment')['profit'].agg(['mean', 'std', 'count']).reset_index()

# Create bar chart with error bars
plt.figure(figsize=(10, 6))

# Create bars
bars = plt.bar(segment_stats['customer_segment'], segment_stats['mean'], 
               yerr=segment_stats['std'], capsize=5, 
               color=['#2ecc71', '#3498db', '#9b59b6'])

# Labels and title
plt.title('Average Profit per Order by Customer Segment\n(Electronics Only)', 
          fontsize=14, fontweight='bold')
plt.xlabel('Customer Segment', fontsize=12)
plt.ylabel('Average Profit ($)', fontsize=12)

# Add value labels
for i, row in segment_stats.iterrows():
    plt.text(i, row['mean'] + 2, f'${row["mean"]:.2f}', 
             ha='center', fontweight='bold', fontsize=11)

plt.tight_layout()
plt.show()
```

**Alternative: Create bar chart with error bars (Seaborn)**
```python
# Alternative using seaborn
plt.figure(figsize=(10, 6))

sns.barplot(data=electronics_df, x='customer_segment', y='profit', 
            errorbar='sd', capsize=5, palette='viridis')

plt.title('Average Profit per Order by Customer Segment\n(Electronics Only)', 
          fontsize=14, fontweight='bold')
plt.xlabel('Customer Segment', fontsize=12)
plt.ylabel('Average Profit ($)', fontsize=12)

plt.tight_layout()
plt.show()
```

**Cell 20: Create summary table**
```python
# Create detailed summary table
summary_table = electronics_df.groupby('customer_segment').agg({
    'profit': ['mean', 'median', 'count', 'sum', 'std']
}).round(2)

# Rename columns for readability
summary_table.columns = ['Avg Profit', 'Median Profit', 'Order Count', 'Total Profit', 'Std Dev']

# Format as currency
summary_table['Avg Profit'] = summary_table['Avg Profit'].apply(lambda x: f'${x:.2f}')
summary_table['Median Profit'] = summary_table['Median Profit'].apply(lambda x: f'${x:.2f}')
summary_table['Total Profit'] = summary_table['Total Profit'].apply(lambda x: f'${x:,.2f}')

print("=== DETAILED SUMMARY TABLE (Electronics Only) ===")
print(summary_table)
```

**Cell 21: Write interpretation (Markdown cell)**
```markdown
## Q2 Interpretation

Within the Electronics category, the **Corporate** segment has the highest 
average profit per order at **$87.50**.

**Key findings:**
- Corporate customers ($87.50) spend **107% more** per order than Consumer ($42.30)
- Corporate customers ($87.50) spend **129% more** per order than Home Office ($38.20)
- Corporate segment also has the highest total profit ($12,250) and largest order count (140)

**Why Corporate customers are more profitable:**
- Likely purchasing higher-end electronics (laptops, monitors)
- Buying in bulk (higher quantity per order)
- Less price-sensitive than consumers

**Recommendation:** 
1. Develop targeted marketing campaigns for Corporate customers
2. Consider a Corporate loyalty program
3. Investigate what drives Corporate purchases to replicate for other segments
```

---

### Step 5: Answer Question 3 (Time Trend)

**Question:** Over the 3-month period, is profit trending upward, downward, or flat?

**Cell 22: Prepare time series data**
```python
# Ensure order_date is datetime (should be after cleaning)
print(f"order_date type: {df_clean['order_date'].dtype}")

# Set date as index for time series operations
df_time = df_clean.set_index('order_date')

# Group by date and sum profit
daily_profit = df_time.groupby(df_time.index)['profit'].sum()

print(f"Date range: {daily_profit.index.min()} to {daily_profit.index.max()}")
print(f"Number of days with data: {len(daily_profit)}")
print(f"Total profit over period: ${daily_profit.sum():,.2f}")
```

**Cell 23: Create line plot with trend line**
```python
from scipy import stats

plt.figure(figsize=(12, 6))

# Plot daily profit (semi-transparent)
plt.plot(daily_profit.index, daily_profit.values, 
         alpha=0.3, label='Daily Profit', linewidth=1, color='blue')

# Add 7-day rolling average
rolling_avg = daily_profit.rolling(window=7).mean()
plt.plot(rolling_avg.index, rolling_avg.values, 
         color='red', linewidth=2, label='7-Day Rolling Average')

# Add trend line (linear regression)
x_numeric = np.arange(len(daily_profit))
slope, intercept, r_value, p_value, std_err = stats.linregress(x_numeric, daily_profit.values)
trend_line = intercept + slope * x_numeric
plt.plot(daily_profit.index, trend_line, 'g--', linewidth=2, 
         label=f'Trend Line (slope: ${slope:.2f}/day)')

# Formatting
plt.title('Profit Trend Over Time (January - March 2024)', fontsize=16, fontweight='bold')
plt.xlabel('Date', fontsize=12)
plt.ylabel('Daily Profit ($)', fontsize=12)
plt.legend(loc='upper left')
plt.axhline(y=0, color='gray', linestyle='-', linewidth=0.5)
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Determine trend direction
if slope > 0:
    trend_direction = "upward 📈"
elif slope < 0:
    trend_direction = "downward 📉"
else:
    trend_direction = "flat ➡️"

print(f"Trend direction: {trend_direction}")
print(f"Slope: ${slope:.2f} per day")
print(f"R-squared: {r_value**2:.3f} ({(r_value**2)*100:.1f}% of variance explained)")
```

**Cell 24: Calculate monthly comparison**
```python
# Extract month from date
df_clean['month'] = df_clean['order_date'].dt.month

# Calculate monthly profit
monthly_profit = df_clean.groupby('month')['profit'].sum()
month_names = {1: 'January', 2: 'February', 3: 'March'}

print("=== MONTHLY PROFIT COMPARISON ===")
for month in [1, 2, 3]:
    if month in monthly_profit.index:
        profit_value = monthly_profit[month]
        print(f"{month_names[month]}: ${profit_value:,.2f}")

# Calculate percentage change (Jan to Mar)
if 1 in monthly_profit.index and 3 in monthly_profit.index:
    jan_profit = monthly_profit[1]
    mar_profit = monthly_profit[3]
    percent_change = ((mar_profit - jan_profit) / jan_profit) * 100
    print(f"\nJanuary to March change: {percent_change:+.1f}%")
```

**Cell 25: Write interpretation (Markdown cell)**
```markdown
## Q3 Interpretation

Over the 3-month period from January to March 2024, profit shows an **upward trend** 
with a slope of **$12.45 per day**.

**Key metrics:**
- January profit: $8,450
- March profit: $12,890
- Total growth: **+52.5%**

**Observations:**
- The 7-day rolling average shows increasing momentum after mid-February
- The trend line explains approximately 68% of the variance (R² = 0.68)
- Daily profit became consistently positive after February 20th

**Potential drivers:**
- Post-holiday sales recovery
- Successful marketing campaigns launched in February
- Seasonal demand for Electronics (new product releases)

**Recommendation:** Continue the momentum by analyzing what changed in February 
and replicating those strategies in other regions or product categories.
```

---

### Step 6: Export Cleaned Data

**Cell 26: Save cleaned CSV for Tableau**
```python
# Export to CSV (no index column)
df_clean.to_csv('cleaned_online_orders.csv', index=False)
print("✅ Cleaned data saved to 'cleaned_online_orders.csv'")
print(f"Export shape: {df_clean.shape}")
print(f"Export columns: {df_clean.columns.tolist()}")
```

---

### Step 7: Build Tableau Dashboard

Now switch to **Tableau Public**. Use the exported `cleaned_online_orders.csv`.

#### Dashboard Page 1: Executive Summary

**Sheets to create:**

| Sheet Name | Instructions |
|------------|--------------|
| **KPI - Total Sales** | Create calculated field: `SUM([sales])` → Format as currency → Add to dashboard |
| **KPI - Total Profit** | Create calculated field: `SUM([profit])` → Format as currency |
| **KPI - Avg Profit/Order** | Create calculated field: `AVG([profit])` → Format as currency |
| **Profit by Region** | Drag `region` to Columns, `profit` to Rows → Sort descending → Color: green if positive, red if negative |
| **Sales by Category** | Drag `category` to Columns, `sales` to Rows → Sort descending |
| **Date Range Filter** | Drag `order_date` to Filters → Range of dates → Show filter |

**Dashboard 1 Layout:**
```
┌─────────────────────────────────────────────────────────────────┐
│  📊 Executive Dashboard - Q1 2024                               │
├─────────────────────────────────────────────────────────────────┤
│  [Date Range Filter: Jan 1, 2024  ────────────  Mar 31, 2024]  │
├───────────────────┬───────────────────┬─────────────────────────┤
│                   │                   │                         │
│   Total Sales     │   Total Profit    │   Avg Profit/Order      │
│    $412,500       │     $58,450       │       $28.50            │
│                   │                   │                         │
├───────────────────┴───────────────────┴─────────────────────────┤
│                                                                 │
│  Profit by Region                    Sales by Category          │
│  ┌─────────────────────────┐          ┌─────────────────────┐    │
│  │ North     ████████ $45K │          │ Elect. ████████ $180K│    │
│  │ West      ██████   $32K │          │ Furn.  ██████   $120K│    │
│  │ East      ████     $18K │          │ Office ████     $90K │    │
│  │ South     █ (red) -$2K  │          │                     │    │
│  └─────────────────────────┘          └─────────────────────┘    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

#### Dashboard Page 2: Deep Dive Analysis

**Sheets to create:**

| Sheet Name | Instructions |
|------------|--------------|
| **Profit Over Time** | Drag `order_date` to Columns → right-click → Month → Drag `profit` to Rows → Add `category` to Color |
| **Sales vs Profit** | Drag `sales` to Columns, `profit` to Rows → Drag `region` to Color → Drag `quantity` to Size |
| **Profit Heatmap** | Drag `region` to Rows, `category` to Columns → Drag `profit` to Color (as SUM) → Change mark type to Square |
| **Region Filter** | Drag `region` to Filters → Show as dropdown |

**Dashboard 2 Layout:**
```
┌─────────────────────────────────────────────────────────────────┐
│  🔍 Deep Dive Analysis                                          │
├─────────────────────────────────────────────────────────────────┤
│  [Region Filter: All ▼]                                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Profit Over Time by Category                                   │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │     ▲                                                   │   │
│  │  $60│    ── Electronics                                │   │
│  │  $40│   ── Furniture                                    │   │
│  │  $20│  ── Office Supplies                              │   │
│  │    $└──────────────────────────────────────────────→   │   │
│  │      Jan    Feb    Mar                                 │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  Sales vs Profit                        Profit Heatmap          │
│  ┌─────────────────────────┐            ┌─────────────────┐    │
│  │    •  •                 │            │      Elect Furn Off│    │
│  │  •     •                │            │ North ███ ██  █   │    │
│  │ •   •    •              │            │ East  ██  ███ █   │    │
│  │•        •               │            │ West  ███ ██  ██  │    │
│  └─────────────────────────┘            └─────────────────┘    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Add Dashboard Action (Interactivity):**
1. Dashboard → Actions → Add Action → Filter
2. Name: `Filter by Region`
3. Source Sheet: Profit by Region (from Page 1)
4. Target Sheets: All sheets on Page 2
5. Run action on: Select
6. Click OK

**Publish to Tableau Public:**
1. File → Save to Tableau Public As...
2. Name: `YourName_Capstone_Dashboard`
3. Click Save
4. Copy the share URL (looks like: `https://public.tableau.com/views/YourName_Capstone_Dashboard/...`)

---

### Step 8: Record Video Presentation

**Video structure (3-5 minutes total):**

**Segment 1: Cleaned Data (30 seconds)**
> "Here's my cleaned dataset for the ShopFast capstone project. I started with 5,000 rows of messy order data. The main issues were 200 missing profit values, 50 incorrectly formatted dates, inconsistent category names, 15 missing regions, and 20 rows with negative quantities. After cleaning, I have approximately 4,925 rows. I fixed missing profits by filling with the median profit for each category, converted all dates to datetime format, standardized categories to title case, and removed invalid quantity rows."

**Segment 2: Python Code for Q2 (90 seconds)**
> "Let me show my Python code for Question 2, which asks which customer segment has the highest average profit for Electronics. First, I filtered the DataFrame to only Electronics category using `df[df['category'] == 'Electronics']`. Then I used `groupby('customer_segment')['profit'].mean()` to calculate average profit per segment. The result shows Corporate customers average $87.50 per order, which is 107% higher than Consumer at $42.30. I also created a bar chart with error bars to visualize the differences and show variability within each segment. The error bars show that Corporate profits are more consistent, while Consumer has wider variation."

**Segment 3: Tableau Dashboard (90 seconds)**
> "Here's my Tableau dashboard published online. Page 1 is the Executive Summary. The key takeaway is that the North region generates $45,200 in profit – the highest – while South shows a loss of $2,100. The KPI cards show total sales of $412,000 and average profit per order of $28.50. When I use the date filter, all charts update dynamically. Page 2 is the Deep Dive. I've added a region filter here – when I select North, you can see the profit trend line spikes in February. The scatter plot shows that higher sales don't always mean higher profit – some high-sales orders in the South actually lost money. The heatmap confirms that Electronics drives profit in North and West, but underperforms in South."

**Segment 4: Reflection (30 seconds)**
> "If I had one more week with this data, I would analyze why the South region is losing money. I'd look at shipping costs by region and product-level profitability to identify specific items to discontinue or reprice. I'd also build a simple forecasting model to predict next quarter's profit based on this upward trend. Overall, this project taught me that cleaning data is 80% of the work, but the insights are worth it."

---

### Step 9: Submit via GitHub

**Step-by-step submission:**

```bash
# 1. Navigate to your repo folder
cd ~/Desktop/data-analytics-pilot

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
# - Go to original repo (github.com/decodemy/data-analytics-pilot)
# - Click Pull Requests → New Pull Request
# - Click "compare across forks"
# - Choose your fork and branch (main)
# - Add title: "Capstone Submission – Your Name"
# - Add description with your Loom video link
# - Click "Create Pull Request"
```

---

## Grading Rubric

### Total Points: 40

| Category | Points | Excellent (full) | Satisfactory (partial) | Missing (0) |
|----------|--------|------------------|------------------------|-------------|
| **Data Cleaning** | 10 | All 6 issues fixed, efficient code | 4-5 issues fixed | 3 or fewer fixed |
| **Q1: Regional Profit** | 5 | Bar chart + correct interpretation | Chart only | Missing |
| **Q2: Category/Segment** | 5 | Bar chart + table + interpretation | Chart only | Missing |
| **Q3: Time Trend** | 5 | Line plot + trend line + conclusion | Plot only | Missing |
| **Tableau Dashboard** | 10 | 2 pages, filters, actions, professional | 1 page or missing filters | Dashboard missing |
| **Video Presentation** | 5 | Covers 4 segments, clear audio, 3-5 min | Covers 2-3 segments | Video missing |

**Passing threshold:** 28/40 (70%)

---

## Common Pitfalls & How to Avoid Them

### Pitfall #1: Missing profit filled incorrectly

**Wrong:**
```python
df['profit'] = df['profit'].fillna(df['profit'].median())
```

**Correct:**
```python
df['profit'] = df.groupby('category')['profit'].transform(
    lambda x: x.fillna(x.median())
)
```

**Why it matters:** Electronics profit margins differ from Office Supplies. Using overall median introduces bias.

### Pitfall #2: Forgetting to handle date conversion errors

**Wrong:**
```python
df['order_date'] = pd.to_datetime(df['order_date'])  # Fails on wrong formats
```

**Correct:**
```python
df['order_date'] = pd.to_datetime(df['order_date'], errors='coerce')
df = df.dropna(subset=['order_date'])
```

### Pitfall #3: Not handling negative profit in charts

**Wrong:** All bars same color (hides loss)

**Correct:**
```python
colors = ['green' if x > 0 else 'red' for x in profit_by_region]
plt.axhline(y=0, color='black')
```

### Pitfall #4: Tableau dashboard too cluttered

**Fix:** 3-5 sheets per dashboard, 2-3 filters max. Less is more.

### Pitfall #5: Forgetting `index=False` when exporting

**Wrong:** `df.to_csv('clean.csv')` → adds extra column

**Correct:** `df.to_csv('clean.csv', index=False)`

### Pitfall #6: Not handling "Small Business" segment

**Wrong:** Leaving as-is or dropping rows

**Correct:** Map to 'Corporate' or create new category

---

## Expected Outputs & Sample Solutions

### Expected Q1 Output

| Region | Total Profit |
|--------|--------------|
| North | $45,200 |
| West | $32,500 |
| East | $18,300 |
| South | -$2,100 |

### Expected Q2 Output

| Segment | Avg Profit | Median Profit | Order Count | Total Profit |
|---------|------------|---------------|-------------|--------------|
| Corporate | $87.50 | $72.00 | 140 | $12,250 |
| Consumer | $42.30 | $38.00 | 210 | $8,883 |
| Home Office | $38.20 | $32.50 | 95 | $3,629 |

### Expected Q3 Output

| Metric | Value |
|--------|-------|
| Slope | $12.45 per day |
| January profit | $8,450 |
| March profit | $12,890 |
| Percent change | +52.5% |
| Trend direction | Upward 📈 |

---

## Time Management Plan

| Day | Time | Task | Hours |
|-----|------|------|-------|
| **Tuesday** | Evening | Attend kickoff, download data, initial exploration | 1.5 |
| **Wednesday** | Morning/Afternoon | Data cleaning (all 6 issues) | 2 |
| **Thursday** | Morning | Answer Q1 and Q2 | 1.5 |
| **Thursday** | Afternoon | Answer Q3 + export CSV | 1 |
| **Friday** | Evening | Build Tableau dashboard (Page 1) | 1 |
| **Saturday** | Morning | Build Tableau dashboard (Page 2) + actions | 1 |
| **Saturday** | Afternoon | Record video (practice + final) | 0.5 |
| **Sunday** | Morning | Final checks, submit via GitHub | 0.5 |
| **Total** | | | **9 hours** |

---

## Final Checklist

### Python Notebook
- [ ] Kernel restarted and "Run All" completes without errors
- [ ] Missing profit values filled by category (not overall median)
- [ ] Dates converted to datetime with `errors='coerce'`
- [ ] Categories standardized to title case
- [ ] "Small Business" mapped to "Corporate"
- [ ] Negative/zero quantity rows removed
- [ ] Missing regions filled with "Unknown"
- [ ] All 3 questions have code + chart + interpretation
- [ ] `cleaned_online_orders.csv` exported with `index=False`

### Tableau Dashboard
- [ ] Dashboard has 2 pages
- [ ] Page 1: 3 KPI cards + 2 bar charts + date filter
- [ ] Page 2: line chart + scatter plot + heatmap + region filter
- [ ] At least 1 dashboard action works
- [ ] Dashboard published to Tableau Public
- [ ] Link saved in `tableau_link.txt`

### Video Presentation
- [ ] Length: 3-5 minutes
- [ ] Covers: cleaned data + Python code + Tableau + reflection
- [ ] Audio clear, no background noise
- [ ] Link saved in `loom_link.txt`

### Submission
- [ ] All files in `submission_template/` folder
- [ ] Pull Request opened with Loom link in description

---

## Key Takeaways from the Pilot

### What You've Accomplished

| Week | Skills Gained |
|------|---------------|
| 1 | Python fundamentals (variables, loops, functions, CSV reading) |
| 2 | Pandas (data cleaning, grouping, aggregation, merging) |
| 3 | Visualization (Matplotlib, Seaborn, Tableau dashboards) |
| 4 | End-to-end project on real messy data |

### The Data Analytics Workflow (You Now Know)

```
Get Data → Clean Data → Explore → Visualize → Present → Decision
```

### What's Next After the Pilot?

| Course | Topics | Duration |
|--------|--------|----------|
| Data Analytics Pro | SQL, advanced statistics, A/B testing | 6 weeks |
| Applied Data Science | Machine learning, scikit-learn | 8 weeks |
| Data Engineering | ETL pipelines, Airflow, cloud | 10 weeks |



**End of Week 4 Class Notes**

*Save this document. Then go finish your capstone. You've got this!* 🚀

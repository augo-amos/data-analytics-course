# Week 2 Class Notes: Data Manipulation with Pandas

**Course:** Foundations of Data Analytics (Pilot)  
**Week:** 2 of 4  
**Prerequisite:** Week 1 completed (variables, lists, loops, functions, CSV reading)  
**Instructor:** Amos Augo

---

## Table of Contents

1. [What is Pandas?](#what-is-pandas)
2. [Series & DataFrames: The Building Blocks](#series--dataframes-the-building-blocks)
3. [Reading Data into Pandas](#reading-data-into-pandas)
4. [Exploring Your Data](#exploring-your-data)
5. [Selecting & Filtering Data](#selecting--filtering-data)
6. [Data Cleaning](#data-cleaning)
7. [Grouping & Aggregation](#grouping--aggregation)
8. [Merging DataFrames](#merging-dataframes)
9. [Exporting Data](#exporting-data)
10. [Common Errors & Debugging](#common-errors--debugging)
11. [Practice Problems](#practice-problems)
12. [Cheat Sheet](#cheat-sheet)

---

## What is Pandas?

### The Problem Pandas Solves

**Week 1 approach (manual loops):**
```python
import csv

total = 0
with open('sales.csv', 'r') as file:
    reader = csv.reader(file) #csv.reader() function reads an open file object line by line, and splits each line into a list of strings based on the commas
    next(reader) # skip the header row
    for row in reader:
        total += float(row[2]) * int(row[1])
print(total)
```

**Week 2 approach (Pandas):**
```python
import pandas as pd

df = pd.read_csv('sales.csv')
total = (df['quantity'] * df['price_per_unit']).sum()
print(total)
```

**Pandas does in 2 lines what took 8 lines in Week 1.**

### What Makes Pandas Powerful?

| Feature | Why It Matters |
|---------|----------------|
| **Vectorized operations** | Math on entire columns at once (fast in C, not Python) |
| **Missing data handling** | Built-in methods for NaN, null, empty values |
| **Group by operations** | SQL-style aggregations in 1 line |
| **Merge/join** | Combine datasets like database joins |
| **Time series** | Built-in date handling (resampling, rolling windows) |
| **Industry standard** | Every data job expects Pandas knowledge |

### The 80/20 Rule for Pandas

**20% of Pandas features handle 80% of real-world work:**

| Feature | Frequency of Use |
|---------|------------------|
| `pd.read_csv()` / `df.to_csv()` | Daily |
| `df.head()` / `df.info()` / `df.describe()` | Daily |
| Filtering: `df[df['col'] > x]` | Daily |
| `df.groupby()` + `.agg()` | Daily |
| `df.isnull()` / `df.fillna()` | Weekly |
| `pd.merge()` | Weekly |
| Everything else | Occasionally |

> **Focus on these 7 things.** The rest you can Google when needed.

---

## Series & DataFrames: The Building Blocks

### What is a Series?

A **Series** is a single column of data (with an index).

```python
import pandas as pd

# Create a Series from a list
prices = pd.Series([100, 250, 75, 400, 120])
print(prices)

# Output:
# 0    100
# 1    250
# 2     75
# 3    400
# 4    120
# dtype: int64
```

**Key concepts:**
- Left column = **index** (like row numbers, starting at 0)
- Right column = **values**
- `dtype` = data type of values

### What is a DataFrame?

A **DataFrame** is a table (multiple columns). Think of it as a spreadsheet in Python.

```python
# Create a DataFrame from a dictionary
df = pd.DataFrame({
    'product': ['Laptop', 'Mouse', 'Keyboard', 'Monitor'],
    'price': [899.99, 24.99, 49.99, 249.99],
    'quantity': [2, 5, 3, 1]
})

print(df)

# Output:
#    product   price  quantity
# 0   Laptop  899.99         2
# 1    Mouse   24.99         5
# 2  Keyboard   49.99         3
# 3  Monitor  249.99         1
```

**Visualizing a DataFrame:**

```
        DataFrame
    ┌─────────────────────────┐
    │  product    price  qty  │ ← Column names
    ├─────────────────────────┤
    │  Laptop    899.99   2   │ ← Row 0
    │  Mouse      24.99   5   │ ← Row 1
    │  Keyboard   49.99   3   │ ← Row 2
    │  Monitor   249.99   1   │ ← Row 3
    └─────────────────────────┘
         ↑         ↑      ↑
      Column 0  Col 1  Col 2   (also called df['product'])
```

### Series vs DataFrame: When to Use Each

| Use a Series when... | Use a DataFrame when... |
|---------------------|------------------------|
| You have one column of data | You have multiple columns |
| Result of `.groupby().sum()` | Result of `pd.read_csv()` |
| A single calculation output | Most real-world data |

---

## Reading Data into Pandas

### Reading CSV Files (90% of your use)

```python
import pandas as pd

# Basic read
df = pd.read_csv('data/messy_orders.csv')

# With common parameters (use these always)
df = pd.read_csv(
    'data/messy_orders.csv',
    encoding='utf-8',      # Handles special characters
    na_values=['', 'NA', 'NULL'],  # Treat these as missing
    parse_dates=['order_date']      # Convert date column to datetime
)

# Preview what you loaded
print(f"Rows: {len(df)}, Columns: {len(df.columns)}")
```

### Common `pd.read_csv()` Parameters

| Parameter | What it does | Example |
|-----------|--------------|---------|
| `filepath` | Path to file | `'data/orders.csv'` |
| `encoding` | Character encoding | `'utf-8'`, `'latin1'` |
| `na_values` | Values to treat as missing | `['', 'NA', 'NULL']` |
| `parse_dates` | Convert to datetime | `['order_date']` |
| `nrows` | Read only first N rows | `nrows=100` (for testing) |
| `usecols` | Read only specific columns | `['order_id', 'sales']` |

### Reading Excel Files

```python
# Need to install: conda install openpyxl
df = pd.read_excel('data/orders.xlsx', sheet_name='Sheet1')
```

### Reading from URL (APIs)

```python
# Read directly from a CSV on the web
url = 'https://raw.githubusercontent.com/.../data.csv'
df = pd.read_csv(url)
```

### Your First Read: Messy Orders

```python
import pandas as pd

# Load the dataset for this week
df = pd.read_csv('week2-pandas/data/messy_orders.csv')

# See what you have
print(type(df))      # <class 'pandas.core.frame.DataFrame'>
print(df.shape)      # (rows, columns) e.g., (1200, 8)
```

---

## Exploring Your Data

### The Essential 5 Methods

```python
# 1. First 5 rows (always do this first)
df.head()

# 2. Last 5 rows
df.tail()

# 3. Column names, non-null counts, data types
df.info()

# 4. Statistical summary (mean, std, min, max for numeric columns)
df.describe()

# 5. Random sample (better than head() for large data)
df.sample(5)
```

### Understanding `df.info()` Output

```python
df.info()

# Output:
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 1200 entries, 0 to 1199
# Data columns (total 8 columns):
#  #   Column         Non-Null Count  Dtype  
# ---  ------         --------------  -----  
#  0   order id       1200 non-null   object 
#  1   region         1195 non-null   object   ← 5 missing!
#  2   category       1200 non-null   object 
#  3   sales          1200 non-null   float64
#  4   profit         1050 non-null   float64 ← 150 missing!
#  5   quantity       1200 non-null   int64  
#  6   order_date     1200 non-null   object ← should be datetime
#  7   customer_id    1200 non-null   int64  
# dtypes: float64(2), int64(2), object(4)
# memory usage: 75.0 KB
```

**What to look for:**
- **Non-null count < total rows** → missing values
- **Dtype = object** → likely text (or mixed types)
- **Dtype should be datetime but is object** → need to convert

### Understanding `df.describe()`

```python
df.describe()

# Output:
#            sales      profit    quantity   customer_id
# count  1200.000  1050.00000  1200.00000   1200.000000
# mean    125.430     12.34500     2.10000    500.123456
# std      89.234     45.67890     1.50000    288.675134
# min       5.990   -200.00000     0.00000      1.000000
# 25%      45.500     -5.00000     1.00000    250.000000
# 50%      98.750     10.00000     2.00000    500.000000
# 75%     189.990     30.00000     3.00000    750.000000
# max      999.990    200.00000    10.00000   1000.000000
```

**What to look for:**
- **min** negative for profit? (losses exist)
- **25%/50%/75%** = quartiles (spread of data)
- **count** different between columns? (missing data)

### Other Useful Exploration Methods

```python
# Column names as list
df.columns.tolist()

# Unique values in a column
df['region'].unique()

# Count of each unique value
df['region'].value_counts()

# Check for duplicates
df.duplicated().sum()

# Memory usage (important for large datasets)
df.memory_usage(deep=True)
```

---

## Selecting & Filtering Data

### Selecting a Single Column (Returns Series)

```python
# Two ways (both work, same result)
df['sales']      # Preferred (safe for all column names)
df.sales         # Shorter but fails if column name has spaces

# Example
sales_column = df['sales']
print(type(sales_column))  # <class 'pandas.core.series.Series'>
```

### Selecting Multiple Columns (Returns DataFrame)

```python
# List of column names inside double brackets
df[['product', 'sales', 'profit']]

# Example
subset = df[['order_id', 'region', 'sales']]
```

### Selecting Rows by Position (iloc)

```python
# iloc = integer location (works like list indexing)

# First row (index 0)
df.iloc[0]

# First 5 rows
df.iloc[0:5]      # Same as df.head()

# Rows 10-19 (10 rows total)
df.iloc[10:20]

# Specific row and column (row 5, column 2)
df.iloc[5, 2]

# All rows, specific columns (rows :, columns 0, 2, 3)
df.iloc[:, [0, 2, 3]]
```

### Selecting Rows by Label (loc)

```python
# loc = label location (uses index values, not positions)

# Row with index label 5 (if index is default 0,1,2...)
df.loc[5]

# Multiple rows
df.loc[[1, 3, 5]]

# Range of rows (inclusive of end!)
df.loc[5:10]      # Includes row 10 (different from iloc!)
```

### Filtering Rows by Condition (Most Common!)

```python
# Basic filter: sales > 1000
high_sales = df[df['sales'] > 1000]

# Filter with multiple conditions (AND: &)
# Both conditions must be true
high_sales_north = df[(df['sales'] > 1000) & (df['region'] == 'North')]

# Filter with multiple conditions (OR: |)
# At least one condition true
large_or_small = df[(df['sales'] > 1000) | (df['sales'] < 10)]

# Filter with NOT condition (~)
not_north = df[~ (df['region'] == 'North')]

# String methods (contains, startswith, etc.)
electronics = df[df['category'].str.contains('Electronics', case=False)]

# Multiple values in a list (isin)
east_west = df[df['region'].isin(['East', 'West'])]
```

### The `.copy()` Rule (Important!)

```python
# WITHOUT .copy() - creates a VIEW (can cause warnings)
filtered_view = df[df['sales'] > 1000]

# WITH .copy() - creates an independent copy (safer)
filtered_copy = df[df['sales'] > 1000].copy()

# When to use .copy():
# - You will modify the filtered data
# - You want to avoid SettingWithCopyWarning
# - You're unsure (just use .copy())
```

### Filtering Examples

```python
# Example 1: High-value customers (sales > $500)
high_value = df[df['sales'] > 500]

# Example 2: Loss-making orders (profit < 0)
losses = df[df['profit'] < 0]

# Example 3: Electronics in the North region
electronics_north = df[(df['category'] == 'Electronics') & (df['region'] == 'North')]

# Example 4: Orders with quantity > 5
bulk_orders = df[df['quantity'] > 5]

# Example 5: Orders between $100 and $200
middle_orders = df[(df['sales'] >= 100) & (df['sales'] <= 200)]
```

---

## Data Cleaning

### Finding Missing Values

```python
# Count missing per column
df.isnull().sum()

# Percentage missing
(df.isnull().sum() / len(df)) * 100

# Check if ANY missing in a specific column
df['profit'].isnull().any()

# Rows with ANY missing
df[df.isnull().any(axis=1)]

# Rows with ALL columns missing (rare)
df[df.isnull().all(axis=1)]
```

### Handling Missing Values: Options

| Strategy | When to use | Code |
|----------|-------------|------|
| Drop rows | Few missing (<5%) | `df.dropna()` |
| Fill with constant | Placeholder needed | `df.fillna(0)` |
| Fill with mean | Normal distribution | `df.fillna(df['col'].mean())` |
| Fill with median | Skewed data | `df.fillna(df['col'].median())` |
| Fill forward | Time series | `df.fillna(method='ffill')` |

### Filling Missing Profit (Real Example)

```python
# Problem: 150 missing profit values
# Strategy: Fill with median profit OF THE SAME CATEGORY

# Step 1: Calculate median profit for each category
category_median = df.groupby('category')['profit'].median()

# Step 2: Fill missing using these medians
df['profit'] = df.groupby('category')['profit'].transform(
    lambda x: x.fillna(x.median())
)

# Verify it worked
print(df['profit'].isnull().sum())  # Should be 0
```

### Fixing Inconsistent Text (Categories)

```python
# Problem: 'Electronics', 'electronics', 'ELECTRONICS'
# Solution: Convert to title case (first letter capital, rest lower)

df['category'] = df['category'].str.title()

# Other useful string methods:
df['product'].str.lower()      # all lowercase
df['product'].str.upper()      # all UPPERCASE
df['product'].str.strip()      # remove leading/trailing spaces
df['product'].str.replace(' ', '_')  # replace spaces with underscores
```

### Fixing Data Types

```python
# Problem: Order date is string (object), should be datetime

# Convert to datetime (invalid dates become NaT)
df['order_date'] = pd.to_datetime(df['order_date'], errors='coerce')

# Drop rows where date conversion failed
df = df.dropna(subset=['order_date'])

# Check the change
df.info()  # order_date should now be datetime64
```

### Removing Duplicates

```python
# Check for duplicates
duplicate_count = df.duplicated().sum()

# Remove duplicates (keeps first occurrence)
df = df.drop_duplicates()

# Remove duplicates based on specific columns
df = df.drop_duplicates(subset=['order_id', 'customer_id'])

# Keep last occurrence instead
df = df.drop_duplicates(keep='last')
```

### Renaming Columns

```python
# Problem: Column names have spaces ('order id')
# Solution: Rename to lowercase with underscores

df = df.rename(columns={
    'order id': 'order_id',
    'customer id': 'customer_id',
    'order date': 'order_date'
})

# Alternative: Set all column names at once
df.columns = ['order_id', 'region', 'category', 'sales', 'profit', 
              'quantity', 'order_date', 'customer_id']

# Make all column names lowercase
df.columns = df.columns.str.lower().str.replace(' ', '_')
```

### Removing Outliers (When Appropriate)

```python
# Remove negative quantities (data error)
df = df[df['quantity'] > 0]

# Remove extreme sales (99.9th percentile)
upper_limit = df['sales'].quantile(0.999)
df = df[df['sales'] <= upper_limit]

# Keep rows where profit is within 3 standard deviations
mean = df['profit'].mean()
std = df['profit'].std()
df = df[(df['profit'] >= mean - 3*std) & (df['profit'] <= mean + 3*std)]
```

### Complete Data Cleaning Pipeline

```python
def clean_orders(df):
    """Clean messy orders DataFrame"""
    
    # Make a copy (don't modify original)
    df = df.copy()
    
    # 1. Fix column names
    df.columns = df.columns.str.lower().str.replace(' ', '_')
    
    # 2. Convert date to datetime
    df['order_date'] = pd.to_datetime(df['order_date'], errors='coerce')
    df = df.dropna(subset=['order_date'])
    
    # 3. Fill missing profit with category median
    df['profit'] = df.groupby('category')['profit'].transform(
        lambda x: x.fillna(x.median())
    )
    
    # 4. Standardize categories
    df['category'] = df['category'].str.title()
    
    # 5. Remove negative quantity
    df = df[df['quantity'] > 0]
    
    # 6. Remove duplicates
    df = df.drop_duplicates()
    
    return df

# Use the function
clean_df = clean_orders(df)
```

---

## Grouping & Aggregation

### What is Grouping?

**Concept:** Split data into groups, apply a function, combine results.

```
Original Data          Group By Region           Aggregate (Sum Profit)
┌─────────────┐        ┌─────────────┐           ┌─────────────┐
│ Region Profit│        │ North       │           │ North: $12K │
│ North   $100 │   →    │   $100      │   →       │ South: $8K  │
│ South    $50 │        │   $50       │           │ East:  $6K  │
│ North   $200 │        │   $200      │           └─────────────┘
│ East     $75 │        │ South       │
└─────────────┘        │   $50       │
                       │ East        │
                       │   $75       │
                       └─────────────┘
```

### Basic GroupBy

```python
# Group by one column, aggregate another
profit_by_region = df.groupby('region')['profit'].sum()
print(profit_by_region)

# Output (Series):
# region
# East     6500
# North   12450
# South   -2100
# West     8900
# Name: profit, dtype: int64
```

### Common Aggregation Functions

| Function | What it does |
|----------|--------------|
| `.sum()` | Total |
| `.mean()` | Average |
| `.median()` | Middle value |
| `.count()` | Number of non-null values |
| `.min()` | Smallest value |
| `.max()` | Largest value |
| `.std()` | Standard deviation |
| `.var()` | Variance |

### Multiple Aggregations

```python
# One column, multiple aggregations
result = df.groupby('region')['profit'].agg(['sum', 'mean', 'count'])
print(result)

# Output (DataFrame):
#         sum   mean  count
# region                   
# East    6500  65.00    100
# North  12450 124.50    100
# South  -2100 -21.00    100
# West    8900  89.00    100
```

### Multiple Columns, Multiple Aggregations

```python
# Different aggregations for different columns
result = df.groupby('region').agg({
    'sales': 'sum',
    'profit': ['sum', 'mean'],
    'quantity': 'count'
})

print(result)
```

### Custom Aggregations

```python
# Define your own function
def range_width(x):
    return x.max() - x.min()

# Use it in agg
result = df.groupby('region')['profit'].agg(['sum', 'mean', range_width])
```

### GroupBy with Multiple Columns

```python
# Group by region AND category
result = df.groupby(['region', 'category'])['profit'].sum()
print(result)

# Output (MultiIndex Series):
# region  category      
# East    Electronics    4000
#         Furniture      1500
#         OfficeSupplies 1000
# North   Electronics    8000
# ...
```

### Resetting the Index

```python
# GroupBy result has region as index
profit_by_region = df.groupby('region')['profit'].sum()
print(profit_by_region.index)  # Index(['East', 'North', 'South', 'West'])

# Convert index to regular column
profit_by_region = profit_by_region.reset_index()
print(profit_by_region.columns)  # ['region', 'profit']
```

### Pivot Tables (Alternative to GroupBy)

```python
# Pivot table: rows = region, columns = category, values = profit
pivot = pd.pivot_table(
    df,
    values='profit',
    index='region',
    columns='category',
    aggfunc='sum'
)

print(pivot)

# Output:
# category  Electronics  Furniture  Office Supplies
# region                                           
# East            4000       1500             1000
# North           8000       3000             1450
# South           -500       -800             -800
# West            6000       1500             1400
```

---

## Merging DataFrames

### Why Merge?

Data often lives in multiple files. You need to combine them.

**Example:**
- `orders.csv` has `customer_id` but no customer name
- `customers.csv` has `customer_id` and `customer_name`
- **Merge** combines them on `customer_id`

### Types of Merges (Joins)

```
Left Join (keep all left)    Right Join (keep all right)   Inner Join (keep intersection)
┌─────┬─────┐                ┌─────┬─────┐                ┌─────┬─────┐
│ A   │ B   │                │ A   │ B   │                │ A   │ B   │
├─────┼─────┤                ├─────┼─────┤                ├─────┼─────┤
│ 1   │ x   │                │ 1   │ x   │                │ 1   │ x   │
│ 2   │ y   │                │ 3   │ z   │                │ 3   │ z   │
│ 3   │ NULL│                │ 4   │ w   │                └─────┴─────┘
│ 5   │ NULL│                └─────┴─────┘                
└─────┴─────┘                
```

### Basic Merge

```python
# Load both datasets
orders = pd.read_csv('data/orders.csv')
customers = pd.read_csv('data/customers.csv')

# Merge on customer_id (inner join by default)
merged = pd.merge(orders, customers, on='customer_id')

# Preview
merged.head()
```

### Merge Parameters

```python
# Specify join type
merged = pd.merge(
    orders,           # left DataFrame
    customers,        # right DataFrame
    on='customer_id', # column to join on
    how='inner'       # 'inner', 'left', 'right', 'outer'
)

# Merge on different column names
merged = pd.merge(
    orders,
    customers,
    left_on='cust_id',
    right_on='customer_id',
    how='left'
)

# Merge on multiple columns
merged = pd.merge(
    orders,
    customers,
    on=['region', 'date'],
    how='inner'
)
```

### Checking Merge Quality

```python
# Before merging, check for duplicates
orders['customer_id'].nunique()      # Unique customers in orders
customers['customer_id'].nunique()    # Unique customers in customers

# After merging, check row count
print(f"Original orders: {len(orders)}")
print(f"Merged rows: {len(merged)}")

# If merged rows > original orders → duplicates in right table
# If merged rows < original orders → missing matches (left join needed)

# Check for unmatched rows
unmatched = orders[~orders['customer_id'].isin(merged['customer_id'])]
print(f"Unmatched orders: {len(unmatched)}")
```

### Real Example: Enriching Order Data

```python
# orders.csv has: order_id, customer_id, sales, profit
# customers.csv has: customer_id, segment, region

orders = pd.read_csv('data/orders.csv')
customers = pd.read_csv('data/customers.csv')

# Merge to add customer info to orders
enriched = pd.merge(orders, customers, on='customer_id', how='left')

# Now you can analyze sales by segment
segment_sales = enriched.groupby('segment')['sales'].sum()
print(segment_sales)
```

---

## Exporting Data

### Save to CSV (Most Common)

```python
# Basic save
df.to_csv('cleaned_orders.csv')

# Better practice (no index column)
df.to_csv('cleaned_orders.csv', index=False)

# With encoding
df.to_csv('cleaned_orders.csv', index=False, encoding='utf-8')
```

### Other Export Formats

```python
# Excel
df.to_excel('output.xlsx', index=False)

# JSON (for APIs)
df.to_json('output.json', orient='records')

# Parquet (faster, smaller, for big data)
df.to_parquet('output.parquet', index=False)
```

---

## Common Errors & Debugging

### Error #1: SettingWithCopyWarning

**What it looks like:**
```
SettingWithCopyWarning: A value is trying to be set on a copy of a slice from a DataFrame.
```

**What it means:** You filtered the data without `.copy()`, and Pandas isn't sure if you want to modify the original.

**Fix:**
```python
# Wrong
filtered = df[df['sales'] > 1000]
filtered['new_col'] = 0  # Warning!

# Correct
filtered = df[df['sales'] > 1000].copy()
filtered['new_col'] = 0  # No warning
```

### Error #2: KeyError

**What it looks like:**
```
KeyError: 'Sales'
```

**What it means:** The column name doesn't exist (check spelling/case).

**Fix:**
```python
# Check actual column names
print(df.columns.tolist())

# Use exact spelling (case-sensitive)
df['sales']  # not 'Sales' or 'SALES'
```

### Error #3: TypeError (String + Number)

**What it looks like:**
```
TypeError: unsupported operand type(s) for +: 'float' and 'str'
```

**What it means:** A column has mixed types (e.g., numbers and text).

**Fix:**
```python
# Check the problem column
print(df['sales'].unique())

# Convert to numeric (errors become NaN)
df['sales'] = pd.to_numeric(df['sales'], errors='coerce')

# Then handle the NaN values
df = df.dropna(subset=['sales'])
```

### Error #4: Merge Producing Too Many Rows

**What it looks like:** Merged DataFrame has more rows than original.

**What it means:** The key column in the right DataFrame has duplicates.

**Fix:**
```python
# Check for duplicates in right table
duplicates = customers[customers.duplicated(subset=['customer_id'], keep=False)]
print(f"Duplicate customers: {len(duplicates)}")

# Option 1: Deduplicate before merge
customers_dedup = customers.drop_duplicates(subset=['customer_id'])

# Option 2: Use left join and accept duplicates if intentional
merged = pd.merge(orders, customers, on='customer_id', how='left')
```

### Error #5: MemoryError (Large Dataset)

**What it looks like:**
```
MemoryError: Unable to allocate ...
```

**What it means:** The dataset is too large for your computer's RAM.

**Fix:**
```python
# Read in chunks
chunk_size = 10000
for chunk in pd.read_csv('large_file.csv', chunksize=chunk_size):
    process(chunk)  # Process each chunk separately

# Or read only needed columns
df = pd.read_csv('large_file.csv', usecols=['col1', 'col2', 'col3'])

# Or read first N rows for testing
df = pd.read_csv('large_file.csv', nrows=1000)
```

---

## Practice Problems

### Beginner (Do these first)

**Problem 1:** Load `messy_orders.csv` and answer:
- How many rows and columns?
- What are the column names?
- Which columns have missing values?


<details>
<summary>Click to reveal the solution</summary>

```python
# Solution
import pandas as pd

df = pd.read_csv('week2-pandas/data/messy_orders.csv')
print(f"Shape: {df.shape}")
print(f"Columns: {df.columns.tolist()}")
print(f"Missing:\n{df.isnull().sum()}")
```
</details>

**Problem 2:** Filter to show only orders from the 'North' region with sales > $200.

<details>
<summary>Click to reveal the solution</summary>

```python
# Solution
north_high = df[(df['region'] == 'North') & (df['sales'] > 200)]
print(f"Found {len(north_high)} orders")
north_high.head()
```
</details>

**Problem 3:** Calculate total sales and average profit by category.

<details>
<summary>Click to reveal the solution</summary>
    
```python
# Solution
category_stats = df.groupby('category').agg({
    'sales': 'sum',
    'profit': 'mean'
})
print(category_stats)
```

</details>

### Intermediate

**Problem 4:** Clean the `messy_orders.csv` dataset:
- Fill missing profit with the median profit for that category
- Convert `order_date` to datetime
- Remove rows with negative quantity

<details>
<summary>Click to reveal the solution</summary>
    
```python
# Solution
def clean_dataset(df):
    df = df.copy()
    
    # Fill missing profit by category median
    df['profit'] = df.groupby('category')['profit'].transform(
        lambda x: x.fillna(x.median())
    )
    
    # Convert date
    df['order_date'] = pd.to_datetime(df['order_date'], errors='coerce')
    df = df.dropna(subset=['order_date'])
    
    # Remove negative quantity
    df = df[df['quantity'] > 0]
    
    return df

clean_df = clean_dataset(df)
print(f"Cleaned: {len(clean_df)} rows")
print(f"Missing profit: {clean_df['profit'].isnull().sum()}")
```
</details>

**Problem 5:** Merge orders with customers and find total sales by customer segment.

<details>
<summary>Click to reveal the solution</summary>
    
```python
# Solution
orders = pd.read_csv('week2-pandas/data/messy_orders.csv')
customers = pd.read_csv('week2-pandas/data/customers.csv')

# Clean orders first (use Problem 4 function)
orders_clean = clean_dataset(orders)

# Merge
merged = pd.merge(orders_clean, customers, on='customer_id', how='left')

# Sales by segment
segment_sales = merged.groupby('segment')['sales'].sum().sort_values(ascending=False)
print(segment_sales)
```

</details>

**Problem 6:** Find the top 3 products by total quantity sold.

<details>
<summary>Click to reveal the solution</summary>
    
```python
# Solution (assuming a 'product' column exists)
product_quantity = df.groupby('product')['quantity'].sum().sort_values(ascending=False)
top_3 = product_quantity.head(3)
print(top_3)

# Alternative: If no product column, use category
category_quantity = df.groupby('category')['quantity'].sum().sort_values(ascending=False)
top_3_categories = category_quantity.head(3)
print(top_3_categories)
```
</details>

### Challenge (Optional)

**Problem 7:** Create a summary report DataFrame with:
- Region
- Total sales
- Total profit
- Profit margin (profit/sales)
- Order count
- Average order value

<details>
<summary>Click to reveal the solution</summary>
    
```python
# Solution
summary = df.groupby('region').agg({
    'sales': 'sum',
    'profit': 'sum',
    'order_id': 'count'
}).rename(columns={'order_id': 'order_count'})

# Calculate additional metrics
summary['profit_margin'] = summary['profit'] / summary['sales']
summary['avg_order_value'] = summary['sales'] / summary['order_count']

# Format percentages
summary['profit_margin'] = summary['profit_margin'].apply(lambda x: f"{x:.1%}")

# Reset index to make region a column
summary = summary.reset_index()

print(summary)
```

</details>

## Cheat Sheet

### Reading & Writing
```python
pd.read_csv('file.csv')                    # Read CSV
pd.read_excel('file.xlsx')                 # Read Excel
df.to_csv('output.csv', index=False)       # Write CSV
df.to_excel('output.xlsx', index=False)    # Write Excel
```

### Exploring Data
```python
df.head()                      # First 5 rows
df.tail()                      # Last 5 rows
df.info()                      # Column types + missing
df.describe()                  # Statistics
df.shape                       # (rows, cols)
df.columns.tolist()            # Column names
df['col'].unique()             # Unique values
df['col'].value_counts()       # Count of each value
```

### Selecting & Filtering
```python
df['col']                      # Single column (Series)
df[['col1', 'col2']]           # Multiple columns
df.iloc[0]                     # First row by position
df.iloc[0:5]                   # First 5 rows
df[df['col'] > 10]             # Filter rows
df[(df['a'] > 1) & (df['b'] < 5)]  # Multiple conditions
df[df['col'].isin(['x','y'])]  # Filter by list
```

### Data Cleaning
```python
df.isnull().sum()              # Count missing per column
df.dropna()                    # Drop rows with missing
df.fillna(0)                   # Fill missing with 0
df.fillna(df['col'].mean())    # Fill with mean
df.drop_duplicates()           # Remove duplicates
df.rename(columns={'old':'new'})  # Rename column
```

### Grouping & Aggregation (continued from Cheat Sheet)

```python
df.groupby('col')['value'].sum()              # Group by one column, sum another
df.groupby('col').agg({'a':'sum', 'b':'mean'}) # Multiple aggregations
df.groupby(['col1', 'col2']).size()           # Count per group
df.pivot_table(values='profit', index='region', columns='category', aggfunc='sum')  # Pivot table
```

### Merging DataFrames

```python
pd.merge(df1, df2, on='key')                  # Inner join
pd.merge(df1, df2, on='key', how='left')      # Left join
pd.merge(df1, df2, left_on='a', right_on='b') # Different column names
```

### Useful One-Liners

```python
df['new_col'] = df['a'] + df['b']             # Create new column from calculation
df['col'].astype('int')                       # Change data type
df.sort_values('col', ascending=False)        # Sort DataFrame
df.reset_index(drop=True)                     # Reset index to 0,1,2...
df.sample(10)                                 # Random 10 rows
df['col'].rank()                              # Rank values (1 = smallest)
df['col'].cumsum()                            # Cumulative sum
```

---

## Key Takeaways

By the end of Week 2, you should understand:

1. **Pandas has two core structures** – Series (one column) and DataFrame (table)
2. **Always explore first** – `.head()`, `.info()`, `.describe()`
3. **Filtering is the most common operation** – `df[df['col'] > value]`
4. **Data cleaning is 80% of real work** – missing values, inconsistent text, wrong types
5. **GroupBy is for questions like "by region, what is total profit?"**
6. **Merge combines multiple files** – like SQL joins
7. **Use `.copy()` when filtering to avoid warnings**
8. **The 20% of features you learn first handle 80% of tasks**

**What comes next:** In Week 3, you'll take your cleaned data and create visualizations:
- Python charts with Matplotlib and Seaborn
- Interactive dashboards with Tableau

**You now have the data manipulation skills to clean any messy dataset.**

---

## Additional Resources

### Pandas Documentation (Bookmark These)
- [Pandas Cheat Sheet (PDF)](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- [10 Minutes to Pandas](https://pandas.pydata.org/docs/user_guide/10min.html)
- [Cookbook (Examples)](https://pandas.pydata.org/docs/user_guide/cookbook.html)

### Practice Datasets (Kaggle)
- [Titanic Dataset](https://www.kaggle.com/c/titanic/data) – Perfect for practicing cleaning + groupby
- [Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) – Real messy data

### Common Pandas Patterns (Keep This List)

```python
# Pattern 1: Load, Clean, Analyze
df = pd.read_csv('data.csv')
df = df.dropna()                           # Clean
result = df.groupby('category')['sales'].sum()  # Analyze

# Pattern 2: Filter then Calculate
high_sales = df[df['sales'] > 1000]
total = high_sales['profit'].sum()

# Pattern 3: Fix Missing Values by Group
df['profit'] = df.groupby('category')['profit'].transform(
    lambda x: x.fillna(x.median())
)

# Pattern 4: Merge then Aggregate
merged = pd.merge(orders, customers, on='id')
summary = merged.groupby('segment')['sales'].sum()

# Pattern 5: Create New Column from Existing
df['profit_margin'] = df['profit'] / df['sales']
df['high_value'] = df['sales'] > 500
```

---

## Office Hours & Support

- **Slack:** `#python-help` (24hr response)
- **Office hours:** Saturday 11 AM–12 PM ET
- **GitHub Issues:** For code submission problems

**Remember:** Pandas has a steep learning curve. If you're frustrated on Wednesday, that's normal. By Saturday, the patterns will click.

> "Every data analyst felt confused their first week with Pandas. The ones who succeed are the ones who kept typing anyway."

---

**End of Week 2 Class Notes**

*Save this document. You'll reference it in Weeks 3 and 4, and in your first data job.*

---

## Complete Table of Contents for Week 2 Notes (Full Document)

1. What is Pandas?
2. Series & DataFrames: The Building Blocks
3. Reading Data into Pandas
4. Exploring Your Data
5. Selecting & Filtering Data
6. Data Cleaning
7. Grouping & Aggregation
8. Merging DataFrames
9. Exporting Data
10. Common Errors & Debugging
11. Practice Problems
12. Cheat Sheet
13. Key Takeaways
14. Additional Resources

**Total length:** ~3,500 words, ~150 code examples

**File to save as:** `week2-pandas/class_notes.md`

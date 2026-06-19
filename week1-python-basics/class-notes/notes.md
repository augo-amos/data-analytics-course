# Week 1 Class Notes: Python Fundamentals for Data

**Course:** Foundations of Data Analytics (Pilot)  
**Week:** 1 of 4  
**Instructor:** Amos Augo  
**Format:** Read alongside Tuesday lecture + Thursday lab

---

## Table of Contents

1. [Why Python for Data?](#why-python-for-data)
2. [Your First Python Code](#your-first-python-code)
3. [Working with Lists](#working-with-lists)
4. [Loops & Conditionals](#loops--conditionals)
5. [Functions](#functions)
6. [Reading CSV Files](#reading-csv-files)
7. [Common Errors & Debugging](#common-errors--debugging)
8. [Practice Problems](#practice-problems)
9. [Cheat Sheet](#cheat-sheet)

---

## Why Python for Data?

### What Makes Python Special?

| Feature | Why It Matters |
|---------|----------------|
| **Free & open source** | No license fees – ever |
| **Beginner-friendly** | Reads like English (almost) |
| **Huge ecosystem** | 300,000+ libraries for data, ML, AI |
| **Industry standard** | Netflix, NASA, Spotify, Instagram use it |

### Python vs Excel: A Honest Comparison

| Task | Excel | Python |
|------|-------|--------|
| 100 rows | Easy | Easy |
| 1 million rows | Slow, crashes | Fast |
| Repeat same analysis weekly | Manual (click) | One script, 2 seconds |
| Machine learning | Impossible | 5 lines of code |
| Cost | $70/month (Microsoft 365) | Free |

**Bottom line:** Excel is fine for one-time small tasks. Python is for serious, repeatable, large-scale data work.

### How This Week Fits Together

```
Week 1 (You are here)
    ↓
Python basics (variables, loops, functions)
    ↓
Week 2: Pandas (automates everything from Week 1)
    ↓
Week 3: Visualization + Tableau
    ↓
Week 4: Capstone (put it all together)
```

> **Instructor note:** Week 1 is the hardest because everything is new. By Friday, patterns will click.

---

## Your First Python Code

### What is a Variable?

A **variable** is a named box that stores a value.

```python
# Variable = value
name = "Alex"
sales_amount = 250
tax_rate = 0.08
```

**Rules for variable names:**
- Use lowercase letters, numbers, underscores: `total_sales`
- No spaces: `total sales` → ❌
- Cannot start with a number: `1st_place` → ❌
- Case-sensitive: `Sales` and `sales` are different

### Data Types (The 4 You Need to Know)

| Type | What it stores | Example |
|------|---------------|---------|
| **int** | Whole numbers | `age = 25`, `quantity = 3` |
| **float** | Decimal numbers | `price = 19.99`, `profit = -5.50` |
| **str** (string) | Text (in quotes) | `name = "Data"`, `region = 'North'` |
| **bool** | True/False | `is_active = True`, `on_sale = False` |

**Check a variable's type:**
```python
price = 19.99
print(type(price))  # <class 'float'>
```

### Basic Math Operations

```python
# Addition
total = 100 + 250        # 350

# Subtraction
difference = 500 - 75    # 425

# Multiplication
double = 50 * 2          # 100

# Division
half = 100 / 2           # 50.0 (always float)

# Exponentiation (power)
squared = 5 ** 2         # 25

# Modulo (remainder)
remainder = 10 % 3       # 1
```

### The print() Function

```python
# Print a single value
print("Hello")           # Hello

# Print multiple values (comma separates, adds space)
print("Total:", 350)     # Total: 350

# f-strings (formatted strings) – BEST WAY
name = "Alex"
score = 95
print(f"{name} scored {score}%")  # Alex scored 95%
```

**Why f-strings?** They put variables directly inside `{}` within a string. No `+` needed.

### Getting User Input

```python
# Always returns a string
name = input("What is your name? ")
print(f"Hello, {name}!")

# Convert string to number for math
age = input("Enter your age: ")
age = int(age)  # Convert to integer
print(f"Next year you'll be {age + 1}")
```

### Quick Practice: Temperature Converter

```python
# Convert Celsius to Fahrenheit
celsius = 25
fahrenheit = (celsius * 9/5) + 32
print(f"{celsius}°C is {fahrenheit}°F")  # 25°C is 77.0°F
```

**Try it yourself:** Change `celsius` to 0, then to 100. What do you get?

---

## Working with Lists

### What is a List?

A **list** stores multiple values in a single variable. Think of it as a numbered row of boxes.

```python
# Create a list (square brackets, comma-separated)
prices = [100, 250, 75, 400, 120]
names = ["Laptop", "Mouse", "Keyboard"]
mixed = [10, "Apple", 3.5, True]  # Lists can mix types (but rarely do)
```

### Accessing Elements (Indexing)

**Important:** Python counting starts at **0**, not 1.

```python
prices = [100, 250, 75, 400, 120]

# First item (index 0)
print(prices[0])     # 100

# Second item (index 1)
print(prices[1])     # 250

# Last item (index -1)
print(prices[-1])    # 120

# Second-to-last (index -2)
print(prices[-2])    # 400
```

**Visual memory aid:**
```
Index:    0      1     2      3      4
List:   [100,   250,   75,   400,   120]
Index:   -5     -4    -3     -2     -1
```

### Slicing (Getting a Subset)

```python
prices = [100, 250, 75, 400, 120]

# From index 1 up to (but not including) 3 #The length of a sliced sequence is simply the stop index minus the start index (\(start - stop\))
print(prices[1:3])    # [250, 75]

# From start up to index 3 (not including)
print(prices[:3])     # [100, 250, 75]

# From index 2 to end
print(prices[2:])     # [75, 400, 120]

# Copy entire list
copy = prices[:]      # [100, 250, 75, 400, 120]
```

### Modifying Lists

```python
items = ["Laptop", "Mouse", "Keyboard"]

# Add to end
items.append("Monitor")
print(items)          # ['Laptop', 'Mouse', 'Keyboard', 'Monitor']

# Insert at specific position (index 1)
items.insert(1, "USB Cable")
print(items)          # ['Laptop', 'USB Cable', 'Mouse', 'Keyboard', 'Monitor']

# Remove by value (first occurrence)
items.remove("Mouse")
print(items)          # ['Laptop', 'USB Cable', 'Keyboard', 'Monitor']

# Remove by index (pop returns the removed value)
removed = items.pop(0)
print(removed)        # 'Laptop'
print(items)          # ['USB Cable', 'Keyboard', 'Monitor']

# Get length (number of items)
print(len(items))     # 3
```

### Useful List Operations

```python
numbers = [5, 2, 8, 1, 9]

# Sum
total = sum(numbers)      # 25

# Minimum
lowest = min(numbers)     # 1

# Maximum
highest = max(numbers)    # 9

# Sort (creates NEW sorted list)
sorted_numbers = sorted(numbers)  # [1, 2, 5, 8, 9]

# Sort in place (modifies original)
numbers.sort()            # numbers becomes [1, 2, 5, 8, 9]

# Check if value exists
if 5 in numbers:
    print("Found it!")
```

### List Practice: Sales Tracker

```python
# Daily sales for a week
daily_sales = [120, 95, 200, 150, 175, 300, 250]

# Calculate weekly total
weekly_total = sum(daily_sales)
print(f"Weekly total: ${weekly_total}")

# Find best day
best_day = max(daily_sales)
print(f"Best day: ${best_day}")

# Average daily sales (total / number of days)
average = weekly_total / len(daily_sales)
print(f"Average: ${average:.2f}")  # :.2f rounds to 2 decimals
```

---

## Loops & Conditionals

### For Loops (Repeat for each item)

A **for loop** runs the same code for each item in a list.

```python
# Basic for loop
prices = [100, 250, 75, 400, 120]

for price in prices:
    print(price)

# Output:
# 100
# 250
# 75
# 400
# 120
```

**Read it as:** "For each `price` in the list `prices`, do something."

### For Loops with range()

`range(n)` generates numbers from 0 to n-1.

```python
# Repeat 5 times (0, 1, 2, 3, 4)
for i in range(5):
    print(f"Round {i}")

# Output:
# Round 0
# Round 1
# Round 2
# Round 3
# Round 4
```

**range(start, stop, step):**
```python
# From 1 to 10 (not including 11)
for i in range(1, 11):
    print(i)

# Even numbers from 2 to 10
for i in range(2, 11, 2):
    print(i)  # 2, 4, 6, 8, 10
```

### While Loops (Repeat while condition is true)

Use a **while loop** when you don't know how many iterations you need.

```python
# Count down from 5
count = 5
while count > 0:
    print(count)
    count = count - 1  # Decrease count (important!)
print("Blast off!")

# Output:
# 5
# 4
# 3
# 2
# 1
# Blast off!
```

**WARNING:** Without `count = count - 1`, the loop runs forever (infinite loop). Press `Ctrl+C` to stop.

### If/Elif/Else (Conditionals)

```python
score = 85

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print(f"Grade: {grade}")  # Grade: B
```

**Comparison operators:**
| Operator | Meaning | Example |
|----------|---------|---------|
| `==` | Equal to | `if x == 5:` |
| `!=` | Not equal to | `if x != 5:` |
| `>` | Greater than | `if x > 5:` |
| `<` | Less than | `if x < 5:` |
| `>=` | Greater than or equal | `if x >= 5:` |
| `<=` | Less than or equal | `if x <= 5:` |

**Multiple conditions:**
```python
# and (both must be true)
if age >= 18 and citizenship == "US":
    print("Can vote")

# or (at least one must be true)
if temperature > 100 or temperature < 0:
    print("Extreme weather alert")

# not (reverse)
if not is_weekend:
    print("Go to work")
```

### Combining Loops and Conditionals

**Example: Find high-value orders**
```python
order_amounts = [50, 250, 30, 500, 120, 1000]

print("High-value orders (>$200):")
for amount in order_amounts:
    if amount > 200:
        print(f"${amount}")

# Output:
# High-value orders (>$200):
# $250
# $500
# $1000
```

**Example: Calculate total with discount**
```python
prices = [100, 250, 75, 400, 120]
discount_rate = 0.10  # 10% off

total_after_discount = 0

for price in prices:
    discounted = price * (1 - discount_rate)
    total_after_discount = total_after_discount + discounted

print(f"Total after 10% discount: ${total_after_discount:.2f}")
```

**Example: Count how many sales > 100**
```python
sales = [50, 150, 30, 200, 80, 300]
count_high = 0

for sale in sales:
    if sale > 100:
        count_high = count_high + 1

print(f"Sales over $100: {count_high}")  # 3
```

---

## Functions

### What is a Function?

A **function** is a reusable block of code. Define it once, use it many times.

### Defining vs Calling

```python
# DEFINE the function (doesn't run yet)
def greet(name):
    print(f"Hello, {name}!")

# CALL the function (runs the code)
greet("Alex")   # Hello, Alex!
greet("Taylor") # Hello, Taylor!
```

### Parameters and Return Values

```python
# Function with parameter and return value
def calculate_discount(price, discount_rate):
    discounted_price = price * (1 - discount_rate)
    return discounted_price

# Use the function
final_price = calculate_discount(100, 0.20)  # 20% off
print(final_price)  # 80.0

final_price = calculate_discount(250, 0.10)  # 10% off
print(final_price)  # 225.0
```

**Key concepts:**
- **Parameters** = inputs (in parentheses)
- **`return`** = output (what the function gives back)
- Without `return`, the function returns `None`

### Function Examples for Data Work

**Calculate total from list:**
```python
def calculate_total(prices):
    total = 0
    for price in prices:
        total = total + price
    return total

sales = [100, 250, 75, 400, 120]
result = calculate_total(sales)
print(result)  # 945
```

**Calculate average:**
```python
def calculate_average(numbers):
    if len(numbers) == 0:
        return 0  # Avoid division by zero
    total = sum(numbers)
    return total / len(numbers)

test_scores = [85, 92, 78, 90, 88]
avg = calculate_average(test_scores)
print(f"Average: {avg:.1f}")  # Average: 86.6
```

**Check if any item exceeds threshold:**
```python
def has_high_value(items, threshold):
    for item in items:
        if item > threshold:
            return True  # Stop early – found one!
    return False  # Checked all, none found

sales = [50, 75, 200, 30, 90]
print(has_high_value(sales, 100))  # True (200 is >100)
print(has_high_value(sales, 500))  # False
```

### Default Parameters

```python
def apply_discount(price, discount_rate=0.10):
    return price * (1 - discount_rate)

# Use default discount (10%)
print(apply_discount(100))      # 90.0

# Override discount
print(apply_discount(100, 0.25)) # 75.0 (25% off)
```

### Why Use Functions?

| Without Functions | With Functions |
|------------------|----------------|
| Copy-paste same code 5 times | Write once, call 5 times |
| Change 1 formula → fix 5 places | Change 1 function → everywhere updates |
| Hard to test | Easy to test in isolation |
| Long, messy notebooks | Clean, organized code |

> **Rule of thumb:** If you write the same code twice, make it a function.

---

## Reading CSV Files

### What is a CSV?

**CSV** = Comma-Separated Values. A plain text file where each line is a row, and commas separate columns.

**Example `sales.csv`:**
```
product,quantity,price_per_unit
Laptop,2,899.99
Mouse,5,24.99
Keyboard,3,49.99
```

### Reading CSV with Python's `csv` Module

```python
import csv  # Import the module (built-in, no install needed)

# Open and read the file
with open('data/sample_sales.csv', 'r') as file:
    reader = csv.reader(file)
    
    # Skip the header row (first row)
    header = next(reader)
    print(f"Columns: {header}")
    
    # Loop through remaining rows
    for row in reader:
        product = row[0]
        quantity = int(row[1])        # Convert string to int
        price = float(row[2])         # Convert string to float
        revenue = quantity * price
        print(f"{product}: ${revenue:.2f}")
```

**Output:**
```
Columns: ['product', 'quantity', 'price_per_unit']
Laptop: $1799.98
Mouse: $124.95
Keyboard: $149.97
```

### Understanding `with open()`

```python
with open('filename.csv', 'r') as file:
    # Do something with file
    pass
# File automatically closes here

# 'r' = read mode (also 'w' for write, 'a' for append)
```

**Why `with`?** It automatically closes the file, even if errors happen.

### Writing to a CSV

```python
import csv

# Data to write
data = [
    ['product', 'quantity', 'price_per_unit'],
    ['Laptop', 2, 899.99],
    ['Mouse', 5, 24.99]
]

with open('output.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerows(data)  # Write all rows at once
```

### Real Example: Calculate Total Revenue from CSV

```python
import csv

def calculate_total_revenue(csv_filename):
    """Read CSV and return total revenue (quantity * price)"""
    total = 0
    
    with open(csv_filename, 'r') as file:
        reader = csv.reader(file)
        next(reader)  # Skip header
        
        for row in reader:
            quantity = int(row[1])
            price = float(row[2])
            total += quantity * price  # += means "add to total"
    
    return total

# Use the function
revenue = calculate_total_revenue('data/sample_sales.csv')
print(f"Total revenue: ${revenue:.2f}")
```

### Common CSV Issues & Fixes

| Problem | Solution |
|---------|----------|
| `FileNotFoundError` | Check file path. Use `'data/sample_sales.csv'` not `'sample_sales.csv'` |
| `ValueError: invalid literal for int()` | Column contains text. Print the row to see what's there. |
| Extra blank rows when writing | Add `newline=''` to `open()`: `open('file.csv', 'w', newline='')` |
| Special characters (é, ñ) | Add `encoding='utf-8'`: `open('file.csv', 'r', encoding='utf-8')` |

---

## Common Errors & Debugging

### Error #1: NameError

**What it looks like:**
```
NameError: name 'price' is not defined
```

**What it means:** You used a variable before creating it.

**Fix:**
```python
# Wrong
print(price)  # price doesn't exist yet
price = 100

# Correct
price = 100
print(price)
```

### Error #2: TypeError (String + Integer)

**What it looks like:**
```
TypeError: can only concatenate str (not "int") to str
```

**What it means:** You tried to add a string and a number.

**Fix:**
```python
# Wrong
quantity = "5"
total = quantity + 10  # Error!

# Correct – convert string to int
quantity = "5"
total = int(quantity) + 10  # 15

# Or convert number to string for printing
print("Total: " + str(15))  # Total: 15
```

### Error #3: IndentationError

**What it looks like:**
```
IndentationError: expected an indented block
```

**What it means:** Python expects spaces inside a loop/function, but found none.

**Fix:**
```python
# Wrong (no indent)
for price in prices:
print(price)

# Correct (4 spaces or Tab)
for price in prices:
    print(price)
```

### Error #4: IndexError

**What it looks like:**
```
IndexError: list index out of range
```

**What it means:** You tried to access an index that doesn't exist.

**Fix:**
```python
prices = [100, 250, 75]  # Indices: 0, 1, 2

# Wrong
print(prices[3])  # Index 3 doesn't exist

# Correct
print(prices[2])  # 75 (last item)
print(prices[-1]) # 75 (also last item)
```

### Error #5: ZeroDivisionError

**What it looks like:**
```
ZeroDivisionError: division by zero
```

**What it means:** You tried to divide by zero.

**Fix:**
```python
# Wrong
average = total / count  # count might be 0

# Correct – check first
if count > 0:
    average = total / count
else:
    average = 0
```

### Debugging Checklist (Do in Order)

1. **Read the error message** – it tells you the line number and problem type
2. **Check the line above** – often the error is one line before where Python complains
3. **Print your variables** – add `print(variable)` to see what's there
4. **Comment out code** – isolate which line causes the problem
5. **Google the exact error** – someone else has seen it
6. **Ask in Slack** – include the error message AND your code

---

## Practice Problems

### Beginner (Do these first)

**Problem 1:** Create a list of 5 temperatures in Celsius. Convert each to Fahrenheit and print.

```python
# Solution
celsius_temps = [0, 10, 20, 30, 40]

for c in celsius_temps:
    f = (c * 9/5) + 32
    print(f"{c}°C = {f}°F")
```

**Problem 2:** Write a function `is_even(num)` that returns `True` if the number is even, `False` otherwise.

```python
# Solution
def is_even(num):
    return num % 2 == 0

print(is_even(4))   # True
print(is_even(7))   # False
```

**Problem 3:** Given `sales = [120, 95, 200, 150, 175]`, calculate total and average.

```python
# Solution
sales = [120, 95, 200, 150, 175]
total = sum(sales)
average = total / len(sales)
print(f"Total: ${total}, Average: ${average:.2f}")
```

### Intermediate

**Problem 4:** Write a function `filter_high_values(numbers, threshold)` that returns a new list containing only numbers greater than the threshold.

```python
# Solution
def filter_high_values(numbers, threshold):
    result = []
    for num in numbers:
        if num > threshold:
            result.append(num)
    return result

values = [10, 25, 5, 30, 15, 50]
high = filter_high_values(values, 20)
print(high)  # [25, 30, 50]
```

**Problem 5:** Read `sample_sales.csv` and calculate:
- Total revenue
- Average order value
- Count of orders > $500

```python
# Solution
import csv

def analyze_sales(filename):
    total_revenue = 0
    order_count = 0
    high_value_count = 0
    
    with open(filename, 'r') as file:
        reader = csv.reader(file)
        next(reader)  # Skip header
        
        for row in reader:
            quantity = int(row[1])
            price = float(row[2])
            revenue = quantity * price
            
            total_revenue += revenue
            order_count += 1
            
            if revenue > 500:
                high_value_count += 1
    
    avg_order = total_revenue / order_count if order_count > 0 else 0
    
    return {
        'total_revenue': total_revenue,
        'avg_order_value': avg_order,
        'high_value_orders': high_value_count
    }

results = analyze_sales('data/sample_sales.csv')
print(results)
```

### Challenge (Optional)

**Problem 6:** Write a function `analyze_text(filename)` that reads a text file and returns:
- Number of lines
- Number of words
- Longest word

```python
# Solution
def analyze_text(filename):
    with open(filename, 'r') as file:
        lines = file.readlines()
    
    line_count = len(lines)
    word_count = 0
    longest_word = ""
    
    for line in lines:
        words = line.split()  # Split by whitespace
        word_count += len(words)
        
        for word in words:
            if len(word) > len(longest_word):
                longest_word = word
    
    return {
        'lines': line_count,
        'words': word_count,
        'longest_word': longest_word
    }

# Create a test file first
with open('test.txt', 'w') as f:
    f.write("Hello world\n")
    f.write("Python is awesome for data analysis\n")

result = analyze_text('test.txt')
print(result)
```

---

## Cheat Sheet

### Variables & Types
```python
name = "Alex"           # String
price = 19.99           # Float
quantity = 5            # Integer
is_valid = True         # Boolean
```

### Lists
```python
items = [1, 2, 3]                # Create
items[0]                         # Access (first)
items[-1]                        # Access (last)
items.append(4)                  # Add to end
items.remove(2)                  # Remove by value
len(items)                       # Length
```

### Loops
```python
for item in my_list:             # Loop through list
    print(item)

for i in range(5):               # Loop 5 times (0-4)
    print(i)

while condition:                 # Loop while true
    do_something()
```

### Conditionals
```python
if x > 10:
    print("Big")
elif x > 5:
    print("Medium")
else:
    print("Small")
```

### Functions
```python
def my_function(param1, param2):
    result = param1 + param2
    return result

output = my_function(5, 3)        # output = 8
```

### CSV Reading
```python
import csv

with open('file.csv', 'r') as f:
    reader = csv.reader(f)
    next(reader)                   # Skip header
    for row in reader:
        print(row[0])              # First column
```

### Common Built-in Functions
```python
print(x)          # Output to console
type(x)           # Get data type
int(x)            # Convert to integer
float(x)          # Convert to float
str(x)            # Convert to string
len(x)            # Length of list/string
sum(x)            # Sum of list
min(x)            # Minimum of list
max(x)            # Maximum of list
sorted(x)         # New sorted list
```

---

## Key Takeaways

By the end of Week 1, you should understand:

1. **Variables store data** – numbers, text, lists
2. **Lists hold multiple values** – accessed by index (starting at 0)
3. **Loops repeat code** – `for` loops iterate through lists
4. **Conditionals make decisions** – `if/elif/else`
5. **Functions reuse code** – define once, call many times
6. **CSV files store tabular data** – read with `csv` module

**What comes next:** In Week 2, you'll learn **Pandas** – which does everything from Week 1 in 1 line of code. But you'll understand *why* it works because you built the pieces yourself.

---

## Office Hours & Support

- **Slack:** `#python-help` (24hr response)
- **Office hours:** Saturday 11 AM–12 PM ET
- **GitHub Issues:** For code submission problems

**Remember:** Every data professional wrote their first loop exactly where you are now. You belong here.

---

**End of Week 1 Class Notes**

*Save this document. You'll reference it in Weeks 2, 3, and 4.*

---

## How to Use These Notes

| For | Use |
|-----|-----|
| **Live lecture** | Follow slides + refer to these notes for examples |
| **Thursday lab** | Students keep notes open while coding |
| **Self-study** | Complete practice problems at the end |
| **Reference** | Use the cheat sheet for syntax look-up |

**File to save as:** `week1-python-basics/class_notes.md` (or `.pdf` for printing)

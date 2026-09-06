# Syllabus: Data Foundations Program

**Academy:** Decodemy  
**Duration:** 4 weeks  
**Weekly commitment:** 5–6 hours  
**Format:** Live online + hands-on projects  
**Tools:** Python (Pandas, Matplotlib, Seaborn), Jupyter Notebook, Tableau Public, GitHub

---

## Course Overview

This pilot program introduces the core workflow of a data analyst: from cleaning raw data in Python to building interactive dashboards in Tableau. You'll complete one real-world project that you can add to your portfolio.

**This is a pilot** – your feedback will shape the full program. By the end, you'll know if a career in data is right for you, without investing in a full-length course.

---

## Learning Objectives

By the end of Week 4, you will be able to:

- Write Python code to load, clean, and analyze tabular data
- Use Pandas for filtering, grouping, and aggregating data
- Create meaningful charts in Python (Matplotlib/Seaborn)
- Build and share an interactive dashboard in Tableau Public
- Present data-driven insights to a non-technical audience

---

## Prerequisites

- No coding experience required
- Basic computer literacy (file management, installing software)
- Willingness to troubleshoot installation issues (with support)

---

## Weekly Breakdown

### Week 0: Setup & Pre-Work (Before Day 1)

**Due:** First live session  
**Time:** ~1 hour

- Install Anaconda (Python + Jupyter)
- Create Tableau Public account
- Sign up for GitHub (free)
- Join class Slack/Discord
- Complete "Welcome Survey"

**Repo folder:** `resources/setup_guide.md`

---

### Week 1: Python Fundamentals for Data

**Focus:** Programming basics for working with data  

| Topic | Details |
|-------|---------|
| Variables & types | int, float, string, bool |
| Data structures | lists, tuples, dictionaries |
| Control flow | if/elif/else, for loops, while loops |
| Functions | defining, parameters, return values |
| File I/O | reading/writing CSV files with basic Python |
| Environment | Jupyter Notebook shortcuts & cells |

**By Friday you will:**
- Write a script that reads a CSV and computes total sales
- Debug common syntax errors

**Repo folder:** `week1-python-basics/`  
**Exercises:** 2 notebooks  
**Dataset:** `sample_sales.csv` (50 rows)

---

### Week 2: Data Manipulation with Pandas

**Focus:** The workhorse of data analysis in Python  

| Topic | Details |
|-------|---------|
| Reading data | `pd.read_csv()`, `pd.read_excel()` |
| Exploring data | `head()`, `info()`, `describe()`, `isnull()` |
| Selecting data | `loc`, `iloc`, boolean filtering |
| Data cleaning | handling missing values, renaming columns |
| Aggregation | `groupby()`, `agg()`, `sum()`, `mean()` |
| Merging | `pd.merge()` on one key |

**By Friday you will:**
- Clean a messy orders file (fix dates, fill missing values)
- Find total sales by region and product category

**Repo folder:** `week2-pandas/`  
**Exercises:** 2 notebooks  
**Datasets:** `messy_orders.csv`, `customers.csv`

---

### Week 3: Visualization + Tableau

**Focus:** Turning numbers into stories  

#### Part A: Python Plotting (2 days)

| Topic | Details |
|-------|---------|
| Matplotlib | line plots, bar charts, histograms, scatter plots |
| Seaborn | `sns.barplot()`, `sns.histplot()`, `sns.pairplot()` |
| Customization | titles, labels, legends, figure size |

#### Part B: Tableau Public (2 days)

| Topic | Details |
|-------|---------|
| Connect data | CSV, Excel, Google Sheets |
| Interface | dimensions vs measures, marks card |
| Chart types | bar, line, geographic map, scatter |
| Dashboards | combine sheets, add filters, actions |
| Sharing | publish to Tableau Public, embed link |

**By Friday you will:**
- Create 3 charts in Python from a single dataset
- Build a 2-page interactive dashboard in Tableau

**Repo folder:** `week3-visualization-tableau/`  
**Exercises:** 2 Python notebooks + 1 Tableau guide  
**Dataset:** `superstore_sample.csv`

---

### Week 4: Capstone Project

**Focus:** End-to-end analysis + presentation  

**Scenario:**  
You are a junior analyst at an e-commerce company. You receive 5,000 rows of online orders with missing values, inconsistent categories, and no clear insights. Your manager needs a dashboard and a 5-minute presentation by Friday.

**Tasks:**
1. Clean the data using Pandas
2. Answer 3 specific business questions (provided in instructions)
3. Create 3 Python charts that support your answers
4. Build a Tableau dashboard with filters for region and date
5. Record a 5-minute Loom presentation walking through insights

**Deliverables:**
- Jupyter notebook with code & commentary
- Exported cleaned CSV
- Tableau Public dashboard link
- Loom video link (unlisted)

**Repo folder:** `week4-capstone/`  
**Files:** `project_instructions.md`, `rubric.md`, `submission_template.ipynb`  
**Dataset:** `online_orders.csv` (5,000 rows)

---

## Schedule (Weekly Live Sessions)

All times are **Eastern Time (UTC-5)** – recordings posted within 24h.

| Week | Live Lecture (2h) | Live Lab (1h) | Office Hours (1h) |
|------|-------------------|---------------|-------------------|
| 1 | Tuesday 7–9 PM | Thursday 7–8 PM | Saturday 11 AM–12 PM |
| 2 | Tuesday 7–9 PM | Thursday 7–8 PM | Saturday 11 AM–12 PM |
| 3 | Tuesday 7–9 PM | Thursday 7–8 PM | Saturday 11 AM–12 PM |
| 4 | Tuesday 7–9 PM (project kickoff) | No lab (project work) | Saturday 11 AM–12 PM (final Q&A) |

**Capstone presentations:** Week 5 Monday 7–9 PM (optional attendance)

---

## Grading & Completion

This pilot is **pass/fail**. To earn a certificate of completion:

| Requirement | Weight | Details |
|-------------|--------|---------|
| Week 1–3 exercises | 30% | Submitted via GitHub, auto-graded |
| Week 3 Tableau dashboard | 20% | Shared link in class Slack |
| Capstone project | 40% | Notebook + dashboard + video |
| Peer feedback (2 peers) | 10% | Comment on other capstones |

**Minimum passing score:** 70%

*All pilot graduates receive 20% off any future paid academy course.*

---

## Tools & Accounts You Need

| Tool | Purpose | Cost | Setup guide |
|------|---------|------|--------------|
| Anaconda | Python + Jupyter | Free | `resources/setup_guide.md` |
| Tableau Public | Dashboards | Free | `resources/setup_guide.md` |
| GitHub | Code submission | Free | [signup link](https://github.com/join) |
| Slack/Discord | Communication | Free | Invite sent Day 1 |
| Loom | Video recording | Free (5 min limit) | [loom.com](https://loom.com) |

---

## Support & Communication

| Channel | Use for | Response time |
|---------|---------|---------------|
| GitHub Issues | Code problems, bug reports | 24 hours |
| Slack #general | Quick questions, community | Peer help + instructor daily |
| Slack #random | Non-course chat | Anytime |
| Office hours (live) | Debugging, career advice | Weekly (see schedule) |
| Email | Private matters (grades, issues) | 48 hours |

**Emergency contact:** `instructor@youracademy.com` (for urgent tech issues during live sessions)

---

## Policies

### Attendance
- Live sessions are recorded; attendance optional but encouraged
- Active participation in Slack counts toward participation

### Late submissions
- Exercises: 2-day grace period, then 10% deduction per day
- Capstone: 3-day grace period, then 50% deduction (must submit to pass)

### Academic honesty
- You may discuss concepts, but code and dashboards must be your own
- Copying another student's capstone = automatic fail
- Using AI tools (ChatGPT, Copilot) is allowed if you:
  - Document which parts were AI-generated
  - Can explain the code in your own words

---

## How to Use This GitHub Repo

1. **Star & watch** the repo to get notifications
2. Each week, open the corresponding folder
3. Read the `README.md` inside for that week's instructions
4. Complete exercises in order
5. Push your code to **your personal forked repo** (not the main one)
6. Submit exercise links via Google Form (provided Week 1)

**Pro tip:** Bookmark the `resources/cheat_sheets/` folder – it contains Pandas, Python, and Tableau quick references.

---

## Sample Capstone Project Preview

*To help you see the finish line, here is the type of question you'll answer:*

> "Which customer segment has the highest average profit per order? Create a bar chart and a Tableau filter that allows the manager to see this by region."

You will receive the exact dataset and 3 business questions on Day 1 of Week 4.

---

## What This Pilot Does NOT Cover (Saved for Paid Programs)

| Topic | Where it appears |
|-------|------------------|
| SQL (joins, subqueries, window functions) | Data Analytics Pro (6 weeks) |
| Machine learning (regression, classification) | Applied Data Science (8 weeks) |
| Data pipelines, Airflow, dbt | Data Engineering (10 weeks) |
| Git branching, rebasing, merge conflicts | Optional workshop |
| Cloud (AWS, GCP, Snowflake) | Data Engineering Advanced |
| A/B testing, statistical significance | Data Analytics Pro |
| Tableau LOD expressions, parameters | Data Analytics Pro |

---

## First Steps (Right Now)

1. [ ] Read this entire syllabus
2. [ ] Complete `resources/setup_guide.md`
3. [ ] Join Slack using invite link (emailed to you)
4. [ ] Post `#introductions` with: name, goal for this course, one fun fact
5. [ ] Fork this repo to your GitHub account
6. [ ] Clone your fork locally

**First live session:** Tuesday [Date] at 7 PM ET – we will write our first Python script together.

---

*Last updated: 06/01/2026*  
*Instructor reserves the right to adjust schedule with 48 hours notice.*

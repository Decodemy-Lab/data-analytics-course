# Week 2: Data Manipulation with Pandas

**Week starting:** [Date]  
**Live lecture:** Tuesday 7–9 PM ET  
**Live lab:** Thursday 7–8 PM ET  
**Office hours:** Saturday 11 AM–12 PM ET

---

## Learning Objectives

By the end of this week, you will be able to:

- Load CSV/Excel files into Pandas DataFrames
- Inspect and understand any dataset using `.info()`, `.describe()`, `.head()`
- Clean messy data: fix missing values, rename columns, filter rows
- Aggregate data with `groupby()` and `.agg()`
- Merge two datasets on a common key
- Export cleaned data for visualization (Week 3)

**Real-world application:** You'll clean a messy orders file that would take hours in Excel – in minutes with Pandas.

---

## Why Pandas?

Pandas is the #1 tool for data manipulation in Python. It handles datasets from 1,000 to 1 billion rows. Most companies expect analysts to know basic Pandas.

**What you'll learn this week is 80% of what working analysts use daily.**

---

## Week 2 Folder Structure

```
week2-pandas/
│
├── README.md (this file)
├── slides.pdf (or Google Slides link)
├── exercises/
│   ├── exercise1_cleaning_orders.ipynb
│   ├── exercise2_grouping_aggregation.ipynb
│   └── solutions/
│       ├── exercise1_solution.ipynb
│       └── exercise2_solution.ipynb
└── data/
    ├── messy_orders.csv
    └── customers.csv
```

---

## Before You Start (Pre-Lab Checklist)

**Complete these before Tuesday's live session:**

- [ ] Anaconda is installed and launches without errors
- [ ] Jupyter Notebook opens in your browser
- [ ] You can run `import pandas as pd` without error
- [ ] You have forked and cloned the course repo
- [ ] You can navigate to `week2-pandas/data/` in Jupyter

**Test your setup:** Open a new Jupyter notebook, run:
```python
import pandas as pd
print(pd.__version__)  # Should show 2.0.x or higher
```

**Stuck?** Post in `#setup-help` on Slack.

---

## Week 2 Schedule (Detailed)

### Tuesday: Live Lecture (2 hours)
**Topics:**
- What is Pandas? Series vs DataFrame
- Reading data: `pd.read_csv()` and `pd.read_excel()`
- First look: `.head()`, `.tail()`, `.sample()`
- Data types: `.dtypes` and why they matter
- Selecting columns: `df['column']` vs `df.column`
- Filtering rows with conditions: `df[df['sales'] > 1000]`

**Live coding demo:** Load `messy_orders.csv`, explore it, find the problems.

**Recording available:** Within 2 hours after session.

---

### Thursday: Live Lab (1 hour)
**Hands-on:** Work through `exercise1_cleaning_orders.ipynb` with instructor guidance.

**You'll practice:**
- Finding missing values with `.isnull().sum()`
- Filling missing profits with median
- Fixing inconsistent category names
- Removing duplicate rows
- Renaming columns

**Lab format:** Instructor solves first 15 minutes, then you solve 30 minutes with live help, then review solutions.

---

### Saturday: Office Hours (1 hour)
**Drop-in format:** Bring your stuck code, error messages, or conceptual questions.

**Popular questions from previous cohorts:**
- "Why does my filter return empty DataFrame?"
- "How do I group by two columns?"
- "What's the difference between `.loc` and `.iloc`?"

**Link:** Posted in `#office-hours` on Slack Friday evening.

---

## Exercises Overview

### Exercise 1: Cleaning Messy Orders (`cleaning_orders.ipynb`)
**Difficulty:** ⭐⭐ (Easy-Medium)  
**Time:** 45–60 minutes

**Scenario:** You receive `messy_orders.csv` with:
- 150 missing profit values
- Category names: "electronics", "Electronics", "ELECTRONICS" (inconsistent)
- Some rows with negative quantity (data error)
- Column names with spaces ("order id" instead of "order_id")

**Tasks:**
1. Load CSV and display first 5 rows
2. Count missing values per column
3. Fill missing profit with median profit of that category
4. Standardize category names to title case (`Electronics`)
5. Remove rows with negative quantity
6. Rename columns to lowercase with underscores
7. Save cleaned data as `cleaned_orders.csv`

**Deliverable:** Completed notebook with all code cells run and visible output.

**Hint:** Use `df['category'].str.title()` for standardization.

---

### Exercise 2: Grouping & Aggregation (`grouping_aggregation.ipynb`)
**Difficulty:** ⭐⭐⭐ (Medium)  
**Time:** 45–60 minutes

**Scenario:** Now that `messy_orders.csv` is clean, you need to answer business questions using `customers.csv` (customer segment info).

**Datasets:**
- `cleaned_orders.csv` (from Exercise 1)
- `customers.csv` (columns: `customer_id`, `segment`, `region`)

**Tasks:**
1. Load both CSVs
2. Merge orders with customers on `customer_id`
3. Calculate total sales by region and segment
4. Find average profit per order for each segment
5. Identify top 3 products by total quantity sold
6. Create a summary DataFrame with:
   - Region
   - Total sales
   - Average profit
   - Order count

**Deliverable:** Completed notebook + exported summary table as `region_summary.csv`.

**Bonus:** Create a bar chart using `df.plot(kind='bar')` for total sales by region (no matplotlib needed – Pandas can plot directly).

---

## Key Concepts Reference

Here are the Pandas methods you'll use most this week. Bookmark this table.

| Task | Code | Notes |
|------|------|-------|
| Load CSV | `df = pd.read_csv('file.csv')` | Use `encoding='latin1'` if special chars fail |
| First 5 rows | `df.head()` | Use `.head(10)` for more rows |
| Data types | `df.dtypes` | Object = string, float64 = number |
| Missing values | `df.isnull().sum()` | Shows count per column |
| Fill missing | `df['col'].fillna(0)` | Replace with 0, mean, median |
| Drop rows with NA | `df.dropna()` | Use `subset=['col']` to target |
| Filter rows | `df[df['sales'] > 1000]` | Multiple conditions: `(df['a']>1) & (df['b']<5)` |
| Group by | `df.groupby('region')['sales'].sum()` | Returns Series |
| Aggregation | `df.groupby('region').agg({'sales':'sum', 'profit':'mean'})` | Multiple metrics |
| Merge | `pd.merge(df1, df2, on='key')` | `how='left'` for left join |
| Rename column | `df.rename(columns={'old':'new'})` | Use `inplace=True` to modify |
| Save to CSV | `df.to_csv('clean.csv', index=False)` | Always set `index=False` |

---

## Common Mistakes & How to Avoid Them

### ❌ Mistake 1: Forgetting `.copy()` when filtering
```python
# This creates a VIEW (can cause warnings)
filtered = df[df['sales'] > 1000]

# Do this instead (creates independent copy)
filtered = df[df['sales'] > 1000].copy()
```

### ❌ Mistake 2: Using `=` instead of `==` in conditions
```python
# Wrong (assigns value, doesn't filter)
df[df['region'] = 'North']

# Correct (checks equality)
df[df['region'] == 'North']
```

### ❌ Mistake 3: Losing the original DataFrame
```python
# This overwrites df permanently
df = df.dropna()

# Better: create new variable
df_clean = df.dropna()
```

### ❌ Mistake 4: Merging without checking keys
```python
# Before merge, check for duplicates
df1['customer_id'].nunique()  # Unique count
df2['customer_id'].nunique()  # Should match if one-to-one
```

---

## Dataset Details

### `messy_orders.csv`
| Column | Type | Issues |
|--------|------|--------|
| order id | string (has space) | Should be `order_id` |
| region | string | Missing values in 5 rows |
| category | string | Inconsistent casing |
| sales | float | OK |
| profit | float | 150 missing (NaN) |
| quantity | integer | 10 negative values |

**Row count:** 1,200

### `customers.csv`
| Column | Type | Notes |
|--------|------|-------|
| customer_id | integer | Unique identifier |
| segment | string | Consumer, Corporate, Home Office |
| region | string | Matches orders.region |

**Row count:** 500 (each customer may have multiple orders)

---

## Success Checklist (End of Week)

By Sunday night, you should have:

- [ ] Completed `exercise1_cleaning_orders.ipynb` (all cells run)
- [ ] Completed `exercise2_grouping_aggregation.ipynb`
- [ ] Exported `region_summary.csv` (from Exercise 2)
- [ ] Pushed both notebooks to your GitHub fork
- [ ] Posted `week2-done` in Slack with a screenshot of your merge output

**If all checkboxes are checked:** You're ready for Week 3 (Visualization & Tableau).

---

## Help & Troubleshooting

### "ModuleNotFoundError: No module named 'pandas'"
**Fix:** Run `conda install pandas -y` in Anaconda Prompt or terminal.

### "FileNotFoundError: [Errno 2] File b'messy_orders.csv'"
**Fix:** Your notebook is in the wrong folder. Check:
```python
import os
print(os.getcwd())  # Should show .../week2-pandas/exercises/
```
Move notebook or adjust path to `../data/messy_orders.csv`

### "SettingWithCopyWarning" (yellow warning message)
**Fix:** Add `.copy()` when filtering:
```python
filtered = df[df['sales'] > 1000].copy()
```

### My merge created duplicate rows
**Fix:** One of your keys has duplicates. Run:
```python
df1['customer_id'].value_counts()  # See which customers repeat
```
Then decide if you need `how='left'` or to deduplicate first.

### Still stuck?
1. **Slack:** Post in `#python-help` with:
   - Error message (copy-paste)
   - Screenshot of your code (3-5 lines before error)
   - What you already tried
2. **GitHub Issue:** Use the template in `.github/ISSUE_TEMPLATE/`
3. **Office hours:** Saturday 11 AM ET – bring your screen share

---

## Preview: How Week 2 Connects to Week 3

In **Week 3**, you'll take your cleaned data and create visualizations:
- Python plots from your `cleaned_orders.csv`
- Tableau dashboard from your `region_summary.csv`

**Save your outputs carefully.** You'll need both files next week.

---

## Additional Resources (Optional)

### Video Tutorials (if you want more practice)
- [Pandas in 10 Minutes (Official)](https://pandas.pydata.org/docs/user_guide/10min.html)
- [Corey Schafer: Pandas Tutorial (1 hour)](https://youtu.be/vmEHCJofslg)
- [Data School: 23 Pandas Tricks (15 min)](https://youtu.be/_T8LGqJtuGc)

### Cheat Sheets (in `resources/cheat_sheets/`)
- `pandas_cheat_sheet.pdf` – All methods on one page
- `data_cleaning_checklist.md` – Step-by-step workflow

### Practice Datasets (Kaggle)
- [Titanic Dataset](https://www.kaggle.com/c/titanic/data) – Classic beginner dataset
- [Hotel Booking Demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand) – More realistic

---

## Week 2 Assignment Submission

**Due:** Sunday 11:59 PM your local time

**Submit via:** GitHub Classroom (link sent Tuesday)

**What to submit:**
1. `exercise1_cleaning_orders.ipynb`
2. `exercise2_grouping_aggregation.ipynb`
3. `region_summary.csv` (from Exercise 2)

**How to submit:**
```bash
# In your terminal (inside repo folder)
git add week2-pandas/exercises/*.ipynb
git add week2-pandas/exercises/region_summary.csv
git commit -m "complete week2 exercises"
git push origin main
```

**Auto-grading:** Your notebook will be checked for:
- No missing values in `cleaned_orders.csv` (for profit column)
- Correct merge output (1,200 rows matched)
- `region_summary.csv` has 4 distinct regions

**Grade release:** Monday by 12 PM ET (via GitHub PR comment)

---

## Live Session Links

| Session | Zoom Link | Recording |
|---------|-----------|-----------|
| Tuesday Lecture | [Link in Slack] | [Available Wed] |
| Thursday Lab | [Link in Slack] | [Available Fri] |
| Saturday Office Hours | [Link in Slack] | [Available Sun] |

**Passcode:** Same for all sessions (posted in `#general`)

---

## Instructor Note

> "Week 2 is the hardest week for most students because Pandas has a steep learning curve. Don't panic if you feel slow. By Saturday, the patterns will click. The students who struggle the most on Tuesday often become the strongest analysts by Week 4."

*If you're stuck after 30 minutes on one problem, take a break, then ask for help. You are not expected to know this beforehand.*

---

**Ready?** Open `exercises/exercise1_cleaning_orders.ipynb` and begin.

**Estimated completion time:** 4–5 hours total this week (including lectures)


---

## How to Use This File

1. **Save as:** `week2-pandas/README.md` in your repo
2. **Replace placeholders:**
   - `[Date]` → actual week starting date
   - Verify Zoom links are added before sharing with students
3. **Optional additions:**
   - Add a screenshot of what the merged DataFrame should look like
   - Embed a 2-minute video preview of Pandas (Loom link)
   - Link to a Google Slides version of your lecture slides

---

## Files You Still Need for Week 2

To make Week 2 complete, you'll also need:

| File | Status | Next step |
|------|--------|------------|
| `exercise1_cleaning_orders.ipynb` | Not generated yet | Request this |
| `exercise2_grouping_aggregation.ipynb` | Not generated yet | Request this |
| `data/messy_orders.csv` | Not generated yet | Request this (I'll create realistic sample data) |
| `data/customers.csv` | Not generated yet | Request this |
| `slides.pdf` | You create | Use Canva/Google Slides |

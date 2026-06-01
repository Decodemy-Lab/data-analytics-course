# Week 1: Python Fundamentals for Data

**Week starting:** [Date]  
**Live lecture:** Tuesday 7–9 PM ET  
**Live lab:** Thursday 7–8 PM ET  
**Office hours:** Saturday 11 AM–12 PM ET

---

## Learning Objectives

By the end of this week, you will be able to:

- Set up and navigate Jupyter Notebook for data analysis
- Write basic Python code using variables, lists, loops, and functions
- Read and process a simple CSV file without external libraries
- Debug common syntax errors independently
- Understand why Python is the #1 language for data careers

**Real-world application:** You'll write a script that reads a sales CSV and calculates total revenue – the foundation of every data analyst's workflow.

---

## Why Python First?

Many bootcamps start with Excel or SQL. We start with Python because:

1. **Python forces you to think logically** (Excel hides the logic in cells)
2. **Python scales** (100 rows or 100 million rows – same code)
3. **Python is free** (no license fees ever)
4. **Python leads to ML & AI** (you can't do machine learning in Excel)

> "The first week is the hardest. By Friday, you'll wonder why you were ever nervous."

---

## Week 1 Folder Structure

```
week1-python-basics/
│
├── README.md (this file)
├── slides.pdf (or Google Slides link)
│
├── exercises/
│   ├── exercise1_variables_loops.ipynb
│   ├── exercise2_functions_csv.ipynb
│   └── solutions/
│       ├── exercise1_solution.ipynb
│       └── exercise2_solution.ipynb
│
├── data/
│   └── sample_sales.csv (10 rows for practice)
│
└── resources/
    └── jupyter_shortcuts.pdf
```

---

## Before You Start (Pre-Lab Checklist)

**Complete before Tuesday's live session:**

- [ ] Anaconda is installed (from `resources/setup_guide.md`)
- [ ] You can launch Jupyter Notebook from Anaconda Navigator
- [ ] You have forked and cloned the course GitHub repo
- [ ] You have joined the class Slack channel
- [ ] You've posted a short intro in `#introductions`

**Test your setup:** Open a new Jupyter notebook, type `print("Hello")`, press Shift+Enter. You should see `Hello` as output.

**Stuck?** Post a screenshot in `#setup-help` on Slack. We'll get you running before Tuesday.

---

## Week 1 Schedule (Detailed)

### Tuesday: Live Lecture (2 hours)

**Part 1: Why Python for Data? (15 min)**
- What makes Python different from Excel
- Python in the real world (Netflix, NASA, Spotify)
- Your career path: Analyst → Data Scientist → Engineer

**Part 2: Your First Python Code (30 min)**
- Variables: `name = "Alex"`, `sales = 250`
- Data types: integers, floats, strings, booleans
- Basic math: `+`, `-`, `*`, `/`, `**` (power)
- Print statements and f-strings: `print(f"Total: ${total}")`

**Part 3: Working with Lists (30 min)**
- Creating lists: `prices = [100, 250, 75, 400]`
- Accessing elements: `prices[0]` (first item), `prices[-1]` (last)
- Adding/removing: `.append()`, `.remove()`
- Slicing: `prices[1:3]`

**Part 4: Loops & Conditionals (30 min)**
- For loops: `for price in prices:`
- If/elif/else: `if price > 200:`
- Combining loops + conditionals

**Part 5: Reading CSV Files (15 min)**
- Python's built-in `csv` module
- Opening files: `with open('file.csv') as f:`
- Looping through rows

**Live coding demo:** Instructor builds a revenue calculator from scratch – you follow along.

**Recording available:** Within 2 hours after session.

**Slides:** `slides.pdf` in this folder.

---

### Thursday: Live Lab (1 hour)

**Hands-on:** Work through `exercise1_variables_loops.ipynb` with instructor guidance.

**You'll practice:**
- Creating variables for sales data
- Writing loops to calculate totals
- Using conditionals to filter high-value orders
- Debugging common errors (NameError, TypeError, IndexError)

**Lab format:** 
- First 20 min: Instructor solves first 3 problems live
- Next 30 min: You solve problems 4-6 independently with live chat support
- Final 10 min: Review solutions and common mistakes

**Recording available:** Within 2 hours after session.

---

### Saturday: Office Hours (1 hour)

**Drop-in format:** Bring any Python question – no question too small.

**Popular questions from previous cohorts:**
- "What's the difference between `=` and `==`?"
- "Why does my loop only run once?"
- "How do I know when to use a list vs a dictionary?"

**Link:** Posted in `#office-hours` on Slack Friday evening.

---

## Exercises Overview

### Exercise 1: Variables & Loops (`exercise1_variables_loops.ipynb`)
**Difficulty:** ⭐ (Easy)  
**Time:** 20–30 minutes

**Topics covered:**
- Creating and updating variables
- Lists: indexing, appending, slicing
- For loops and while loops
- If/elif/else conditionals
- Combining loops with conditionals

**Sample task:**
```python
# Given this list of sales amounts
sales = [100, 250, 75, 400, 120]

# Write a loop that prints only sales greater than 150
# Expected output: 250, 400
```

**Deliverable:** Completed notebook with all code cells filled in and run.

**Solution available:** Sunday in `exercises/solutions/`

---

### Exercise 2: Functions & CSV Files (`exercise2_functions_csv.ipynb`)
**Difficulty:** ⭐⭐ (Easy-Medium)  
**Time:** 30–40 minutes

**Topics covered:**
- Defining functions with `def`
- Parameters and return values
- Reading CSV files with Python's `csv` module
- Calculating totals from CSV data
- Writing results to a new file

**Sample task:**
```python
# Write a function calculate_total(sales_list) that returns the sum
# Then use it on data from sample_sales.csv

def calculate_total(sales_list):
    # YOUR CODE HERE
    pass

# Your function should work with: calculate_total([10, 20, 30]) -> 60
```

**Deliverable:** Completed notebook + exported `total_revenue.txt` file.

**Solution available:** Sunday in `exercises/solutions/`

---

## Python Reference Card (Keep This Open)

### Variables & Data Types

| Concept | Code | Notes |
|---------|------|-------|
| Integer | `x = 10` | Whole number |
| Float | `price = 19.99` | Decimal number |
| String | `name = "Data"` | Text in quotes |
| Boolean | `is_valid = True` | True/False |
| Check type | `type(x)` | Returns `int`, `str`, etc. |

### Lists

| Operation | Code | Example |
|-----------|------|---------|
| Create list | `items = [1, 2, 3]` | |
| First item | `items[0]` | Returns `1` |
| Last item | `items[-1]` | Returns `3` |
| Add item | `items.append(4)` | List becomes `[1,2,3,4]` |
| Remove item | `items.remove(2)` | Removes first `2` |
| Length | `len(items)` | Returns `4` |
| Slice | `items[1:3]` | Returns `[2,3]` |

### Loops

| Type | Code | Use when |
|------|------|----------|
| For loop (list) | `for item in my_list:` | Iterate through items |
| For loop (range) | `for i in range(5):` | Repeat N times (0-4) |
| While loop | `while x < 10:` | Unknown number of iterations |

### Conditionals

| Code | Meaning |
|------|---------|
| `if x > 10:` | Greater than |
| `if x < 10:` | Less than |
| `if x == 10:` | Equal to (NOTE: double equals) |
| `if x != 10:` | Not equal to |
| `if x >= 10:` | Greater than or equal |
| `elif x == 5:` | Else if |
| `else:` | Otherwise |

**Common mistake:** `=` is assignment, `==` is comparison
```python
# Wrong (assigns 10 to x, always True)
if x = 10:

# Correct (checks if x equals 10)
if x == 10:
```

### Functions

| Concept | Code |
|---------|------|
| Define function | `def my_function(param1, param2):` |
| Return value | `return result` |
| Call function | `output = my_function(5, 10)` |

**Example:**
```python
def calculate_discount(price, discount_rate):
    discounted = price * (1 - discount_rate)
    return discounted

final_price = calculate_discount(100, 0.2)  # Returns 80.0
```

### Reading CSV Files

```python
import csv

with open('data/sample_sales.csv', 'r') as file:
    reader = csv.reader(file)
    header = next(reader)  # Skip first row
    for row in reader:
        product = row[0]
        quantity = int(row[1])
        price = float(row[2])
        print(f"{product}: ${quantity * price}")
```

---

## Common Mistakes & How to Fix Them

### ❌ Mistake 1: Indentation Errors
```python
# Wrong (missing indent)
for price in prices:
print(price)

# Correct (indented 4 spaces)
for price in prices:
    print(price)
```
**Fix:** In Jupyter, press Tab after the colon. Use 4 spaces consistently.

### ❌ Mistake 2: Using `=` instead of `==`
```python
# Wrong (assigns value, doesn't compare)
if price = 100:

# Correct (compares)
if price == 100:
```

### ❌ Mistake 3: Forgetting to convert types
```python
# Wrong (string + integer)
quantity = "5"
total = quantity + 10  # Error!

# Correct (convert string to int)
quantity = int("5")
total = quantity + 10  # Works: 15
```

### ❌ Mistake 4: Off-by-one in loops
```python
# Wrong (stops at 4, never prints 5)
for i in range(1, 5):
    print(i)  # Prints 1,2,3,4

# Correct (prints 1 through 5)
for i in range(1, 6):
    print(i)
```

### ❌ Mistake 5: Modifying list while looping
```python
# Wrong (skips items)
for item in my_list:
    if item < 0:
        my_list.remove(item)

# Correct (loop over copy)
for item in my_list[:]:  # [:] creates a copy
    if item < 0:
        my_list.remove(item)
```

---

## Dataset Details

### `sample_sales.csv`
Located in `week1-python-basics/data/`

**Contents:**
```
product,quantity,price_per_unit
Laptop,2,899.99
Mouse,5,24.99
Keyboard,3,49.99
Monitor,1,249.99
USB Cable,10,7.99
```

**Rows:** 10 (5 shown above)  
**Use case:** Exercise 2 – calculate total revenue

---

## Success Checklist (End of Week)

By Sunday night, you should have:

- [ ] Watched Tuesday lecture (live or recording)
- [ ] Attended Thursday lab (or watched recording)
- [ ] Completed `exercise1_variables_loops.ipynb`
- [ ] Completed `exercise2_functions_csv.ipynb`
- [ ] Exported `total_revenue.txt` (from Exercise 2)
- [ ] Pushed both notebooks to your GitHub fork
- [ ] Posted `week1-done` in Slack with a screenshot of your revenue output

**If all checkboxes are checked:** You're ready for Week 2 (Pandas).

---

## Help & Troubleshooting

### "Jupyter won't launch"
**Fix:** 
- Windows: Open Anaconda Prompt, type `jupyter notebook`
- Mac: Open Terminal, type `jupyter notebook`
- If that fails: Reinstall Anaconda

### "NameError: name 'x' is not defined"
**Fix:** You're using a variable before creating it. Check spelling and order of code cells.

### "FileNotFoundError"
**Fix:** Your notebook is in the wrong folder. Use:
```python
import os
print(os.getcwd())  # Shows current directory
```
Then adjust path: `'../data/sample_sales.csv'` (two dots means "go up one folder")

### "IndentationError: unexpected indent"
**Fix:** Mix of tabs and spaces. In Jupyter: Edit → Select All → Format → Untabify Region.

### "TypeError: can only concatenate str to str"
**Fix:** You're adding string to number. Convert: `int(my_string)` or `str(my_number)`

### Still stuck?
1. **Slack:** Post in `#python-help` with:
   - Error message (copy-paste exactly)
   - Your code (paste as text, not screenshot)
   - What you expected to happen
2. **GitHub Issue:** Use the template in `.github/ISSUE_TEMPLATE/`
3. **Office hours:** Saturday 11 AM ET – bring your questions

---

## Preview: How Week 1 Connects to Week 2

In **Week 2**, you'll learn Pandas – a library that automates everything you did manually this week:
- Reading CSV files becomes `pd.read_csv()` (one line)
- Calculating totals becomes `df['sales'].sum()` (one line)
- No more loops over rows (Pandas does it in C speed)

**But Week 1 matters because:** Understanding loops and variables helps you debug when Pandas does something unexpected.

> "You can't drive an automatic car until you understand why a manual transmission works."

---

## Additional Resources (Optional)

### Practice Websites (Free)
- [W3Schools Python](https://www.w3schools.com/python/) – Interactive exercises
- [Python Tutor](https://pythontutor.com/) – Visualize code execution step-by-step
- [Codecademy Python (Free tier)](https://www.codecademy.com/learn/learn-python-3)

### YouTube Videos (If You Want More)
- [Python for Beginners (45 min)](https://youtu.be/kqtD5dpn9C8) – Mosh Hamedani
- [CS50 Python (1 hour)](https://youtu.be/7BQqOqLl9hE) – Harvard's introduction

### Cheat Sheets (in `resources/cheat_sheets/`)
- `python_basics_reference.pdf` – One-page summary
- `jupyter_shortcuts.pdf` – Keyboard shortcuts for speed
- `common_errors.pdf` – Error messages and fixes

---

## Week 1 Assignment Submission

**Due:** Sunday 11:59 PM your local time

**Submit via:** GitHub Classroom (link sent Tuesday)

**What to submit:**
1. `exercise1_variables_loops.ipynb`
2. `exercise2_functions_csv.ipynb`
3. `total_revenue.txt` (exported from Exercise 2)

**How to submit:**
```bash
# In your terminal (inside repo folder)
git add week1-python-basics/exercises/*.ipynb
git add week1-python-basics/exercises/total_revenue.txt
git commit -m "complete week1 exercises"
git push origin main
```

**Auto-grading:** Your notebook will be checked for:
- Code runs without errors
- Variables named correctly
- Output matches expected values

**Manual review:** Instructor will spot-check 5 random submissions for code quality.

**Grade release:** Monday by 12 PM ET (via GitHub PR comment) – Pass/Incomplete only.

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

> "Welcome to Week 1. You're going to feel overwhelmed on Tuesday. That's normal. Every data professional started exactly where you are.

> The difference between those who finish and those who quit is simply this: they kept going when they got stuck.

> **You can do this.** See you in the first lecture."

---

**Ready?** Open `exercises/exercise1_variables_loops.ipynb` in Jupyter and begin.

**Estimated completion time:** 4-5 hours total this week (including lectures)

**Remember:** Week 1 is the foundation. Go slow now to go fast later.

---

## How to Use This File

1. **Save as:** `week1-python-basics/README.md` in your repo
2. **Replace placeholders:**
   - `[Date]` → actual week starting date
   - Verify Zoom links are added before sharing with students
3. **Optional additions:**
   - Add a screenshot of Jupyter Notebook interface
   - Embed a 1-minute "Welcome to Week 1" video
   - Link to a Google Slides version of your lecture slides

---

## What Makes This Week 1 README Better Than the Previous Version

| Improvement | Why It Matters |
|-------------|----------------|
| **Clearer learning objectives** | Students know exactly what "done" looks like |
| **"Why Python first" justification** | Reduces anxiety about not starting with Excel/SQL |
| **Detailed schedule with timing** | Students can plan their week |
| **Reference card (always open)** | Reduces "I forgot the syntax" pauses |
| **Common mistakes table** | Anticipates errors before they happen |
| **Preview of Week 2 connection** | Motivates students to push through difficulty |
| **Instructor note** | Builds psychological safety |

---

## Supporting Files You Still Need for Week 1

To make Week 1 complete, you'll also need:

| File | Status | Next step |
|------|--------|------------|
| `exercise1_variables_loops.ipynb` | Generated previously | Already have it |
| `exercise2_functions_csv.ipynb` | Not generated yet | Request this |
| `data/sample_sales.csv` | Not generated yet | Request this (5-10 rows) |
| `solutions/exercise1_solution.ipynb` | Not generated yet | Request this (instructor-only) |
| `solutions/exercise2_solution.ipynb` | Not generated yet | Request this (instructor-only) |
| `slides.pdf` | You create | Use Canva/Google Slides |
| `resources/jupyter_shortcuts.pdf` | Not generated yet | Request this |

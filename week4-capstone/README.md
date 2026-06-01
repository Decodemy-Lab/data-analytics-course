# Week 4: Capstone Project

**Week starting:** [Date]  
**Live kickoff:** Tuesday 7–9 PM ET (mandatory attendance recommended)  
**No live lab this week** (use time for project)  
**Final office hours:** Saturday 11 AM–1 PM ET (extended for capstone support)

---

## Learning Objectives

By the end of this week, you will be able to:

- Apply everything from Weeks 1-3 to a **new, unseen dataset**
- Independently clean, analyze, and visualize a real-world CSV
- Build a complete Tableau dashboard from scratch
- Present findings in a 5-minute video recording
- Create a portfolio piece to share with employers

**Real-world application:** This project simulates your first week as a junior data analyst. You'll receive messy data, vague questions, and a deadline. How you approach it is exactly what hiring managers want to see.

---

## Why a Capstone?

Weeks 1-3 gave you tools. Week 4 gives you **confidence**.

You'll prove to yourself (and future employers) that you can:
- Handle ambiguity ("Here's a CSV, find insights")
- Work independently without step-by-step instructions
- Communicate findings clearly to non-technical stakeholders

> "The capstone is not a test. It's your first portfolio piece." – Instructor

---

## Week 4 Folder Structure

```
week4-capstone/
│
├── README.md (this file)
├── project_instructions.md (detailed requirements)
├── rubric.md (grading criteria)
├── capstone_kickoff_slides.pdf (Tuesday lecture)
│
├── data/
│   └── online_orders.csv (5,000 rows – new dataset)
│
├── submission_template/
│   ├── README.md (submission instructions)
│   ├── yourname_capstone.ipynb (start here)
│   ├── tableau_link.txt (paste your URL)
│   └── loom_link.txt (paste your video link)
│
├── examples/
│   └── sample_analysis.html (optional – what "good" looks like)
│
└── resources/
    ├── capstone_tips.md (common pitfalls)
    ├── presentation_template.pptx (optional slides)
    └── checklist_before_submit.md
```

---

## Before You Start (Pre-Kickoff Checklist)

**Complete before Tuesday's live session:**

- [ ] Week 3 exercises are complete and pushed to GitHub
- [ ] You have Tableau Public installed and can log in
- [ ] You have a Loom account (free, loom.com)
- [ ] You have 6-8 hours available this week for project work
- [ ] Your GitHub fork is up to date with the main repo

**Critical:** If you haven't completed Weeks 1-3, **do not start Week 4**. The capstone assumes you know:
- Pandas basics (filtering, grouping, merging)
- Matplotlib/Seaborn (bar charts, line plots)
- Tableau (connecting data, building dashboards)

**Need a refresher?** Review `resources/cheat_sheets/` from previous weeks.

---

## Week 4 Schedule (Special Format)

Unlike previous weeks, Week 4 is **project-focused** with fewer live sessions.

### Tuesday: Capstone Kickoff (2 hours – mandatory)
**What we'll cover:**
- Walk through the new dataset (`online_orders.csv`)
- Explain the 3 business questions (see `project_instructions.md`)
- Demo: Solving one question live (so you see the process)
- Time management strategies (don't get stuck)
- Q&A on submission requirements

**Recording:** Available Wednesday morning.

**Slides:** `capstone_kickoff_slides.pdf`

---

### Thursday: No Live Lab
**Instead:** 
- Work on your capstone independently
- Instructor available on Slack `#capstone-help` 2-4 PM ET (office hours by chat)
- Use this time to finish data cleaning and start analysis

---

### Saturday: Extended Office Hours (2 hours – 11 AM–1 PM ET)
**Format:** Drop-in, screen sharing encouraged

**What to bring:**
- Specific question ("My merge isn't working – here's my code")
- A stuck point ("Tableau filter doesn't update all sheets")
- Or just watch others get unstuck (learning by observing)

**Link:** Posted in `#office-hours` Friday evening.

---

### Sunday: Submission Deadline (11:59 PM your local time)
**No extensions** except documented emergencies (contact instructor by Saturday).

**Late policy:** 
- 1-24 hours late: 20% grade deduction
- 24-48 hours late: 50% grade deduction
- >48 hours: Fail (must retake in next cohort)

---

## The New Dataset: `online_orders.csv`

**File location:** `week4-capstone/data/online_orders.csv`

**Rows:** 5,000  
**Columns:** 8  
**Time period:** 3 months (January – March 2024)

| Column | Type | Description | Issues |
|--------|------|-------------|--------|
| `order_id` | integer | Unique ID | None |
| `order_date` | string (YYYY-MM-DD) | Purchase date | 50 rows have wrong format (MM/DD/YYYY) |
| `region` | string | North, South, East, West | 15 rows missing |
| `category` | string | Electronics, Furniture, Office Supplies | Inconsistent casing (mix of lower/title) |
| `customer_segment` | string | Consumer, Corporate, Home Office | 5 rows have "Small Business" (not in expected list) |
| `sales` | float | Total sale amount | None |
| `profit` | float | Profit (can be negative) | 200 rows missing (NaN) |
| `quantity` | integer | Number of items | 20 rows have zero or negative |

**This is intentionally messy** – just like real employer data.

---

## The 3 Business Questions

*(Full details in `project_instructions.md` – this is the summary)*

### Q1: Regional Performance
**Question:** Which region generates the highest total profit? Which region generates the lowest (or most loss)?

**What to deliver:**
- Bar chart (Python or Tableau – your choice)
- One sentence answer

**Hint:** Watch for negative profit (losses). The "lowest" region might be negative.

---

### Q2: Category & Segment Analysis
**Question:** Within the **Electronics** category only, which customer segment has the highest average profit per order?

**What to deliver:**
- Filtered analysis (Electronics only)
- Bar chart with average profit by segment
- Table showing exact averages (formatted to 2 decimals)

**Hint:** Use `.groupby()` and `.agg()`. Remember to handle missing profit values before averaging.

---

### Q3: Time Trend
**Question:** Over the 3-month period, is profit trending upward, downward, or staying flat?

**What to deliver:**
- Line plot with daily or weekly profit
- Add a trend line (rolling average or linear regression)
- One sentence conclusion ("Profit increased 15% from Jan to Mar")

**Hint:** Convert `order_date` to datetime first. Some rows have wrong format – fix or drop them.

---

## Capstone Deliverables (4 Items)

### 1. Jupyter Notebook (`yourname_capstone.ipynb`)
**File path:** `week4-capstone/submission_template/yourname_capstone.ipynb`

**Must include these sections (in order):**

| Section | What to include | Points |
|---------|----------------|--------|
| **1. Setup** | Import libraries, load data | 5% |
| **2. Data Cleaning** | Fix dates, missing profit, inconsistent categories, remove bad rows | 25% |
| **3. Q1 Answer** | Code + chart + interpretation | 15% |
| **4. Q2 Answer** | Code + chart + table + interpretation | 15% |
| **5. Q3 Answer** | Code + line plot + trend line + interpretation | 15% |
| **6. Export** | Save cleaned CSV as `cleaned_online_orders.csv` | 5% |
| **7. Reflection** | 3-5 sentences: What was hardest? What would you do differently? | 10% |
| **8. References** | If you used AI or external code, cite it | 5% |

**Code quality expectations:**
- Every cell runs without errors (Restart Kernel → Run All)
- Comments explain non-obvious steps
- No hardcoded file paths (use relative paths)
- Variables named clearly (`profit_by_region`, not `df3`)

---

### 2. Cleaned CSV (`cleaned_online_orders.csv`)
**Export from your notebook:** `df_clean.to_csv('cleaned_online_orders.csv', index=False)`

**Requirements:**
- No missing profit values (fill with median by category)
- Consistent category names (title case: "Electronics")
- Valid dates (all in YYYY-MM-DD format)
- No negative or zero quantity rows removed

**File location:** Save in same folder as your notebook.

---

### 3. Tableau Dashboard (Public link)
**Build a 2-page dashboard:**

**Page 1: Executive Summary** (for busy managers)
- KPI cards: Total Sales, Total Profit, Average Profit per Order
- Bar chart: Profit by Region (color-coded: positive=green, negative=red)
- Bar chart: Sales by Category
- Filter: Date range (allow manager to select last 2 weeks, last month, etc.)

**Page 2: Deep Dive** (for analysts)
- Line chart: Profit over time (daily or weekly)
- Scatter plot: Sales vs Profit (color by category, size by quantity)
- Heatmap or table: Profit by Region AND Category (pivot table style)
- Filter: Region (affects all charts on Page 2)

**Interactivity requirements:**
- At least 2 filters that affect multiple charts
- At least 1 dashboard action (click a bar → filter other charts)
- Tooltips that show extra information (e.g., "Region: North, Profit: $12,450")

**Publish to Tableau Public** → copy the share URL.

**File to submit:** `tableau_link.txt` with the URL inside.

---

### 4. Loom Video (3-5 minutes)
**Record your screen walking through:**

1. **Your cleaned dataset** (10 seconds)  
   - Open `cleaned_online_orders.csv` in Excel or Jupyter  
   - "I fixed 200 missing profits and 50 date errors"

2. **Your Python code** (1-2 minutes)  
   - Show one of the three questions (your choice)  
   - Explain one interesting line of code  
   - "Here I grouped by region and summed profit"

3. **Your Tableau dashboard** (1-2 minutes)  
   - Open the published dashboard  
   - Demonstrate a filter ("Watch what happens when I select 'North'")  
   - State one insight ("Electronics drives 60% of profit")

4. **Reflection** (30 seconds)  
   - "If I had one more week, I would analyze [X]"

**Technical requirements:**
- Video length: 3-5 minutes (strict)
- Screen recording with your voice (face optional)
- Set Loom to "Unlisted" (not public, but anyone with link can view)
- Test link before submitting (open in incognito window)

**File to submit:** `loom_link.txt` with the URL inside.

---

## Time Management Plan (6-8 hours total)

| Day | Tasks | Time |
|-----|-------|------|
| **Tuesday** | Attend kickoff, download dataset, explore data | 2 hours |
| **Wednesday** | Data cleaning (fix dates, missing profits, categories) | 2 hours |
| **Thursday** | Answer Q1 and Q2 (Python) | 1.5 hours |
| **Friday** | Answer Q3 + export cleaned CSV | 1.5 hours |
| **Saturday** | Build Tableau dashboard (2 pages) | 2 hours |
| **Sunday** | Record Loom video, final checks, submit | 1 hour |

**Pro tip:** Don't leave Tableau for Sunday night. Start Saturday morning so you can ask for help in office hours.

---

## Common Pitfalls (Read This Before Starting)

### ❌ Pitfall 1: Over-cleaning
**Problem:** Spending 4 hours making the data "perfect" (handling every edge case)  
**Reality:** Business decisions use 80% clean data. Drop problematic rows (5% of data) and move on.  
**Fix:** If a column has <5% bad data, drop those rows. If >20% bad, fill with median.

### ❌ Pitfall 2: Ignoring the questions
**Problem:** Creating beautiful charts that don't answer Q1, Q2, Q3  
**Fix:** After every chart, ask: "Does this directly answer one of the three questions?"

### ❌ Pitfall 3: Tableau over-engineering
**Problem:** 10 sheets, 5 dashboards, 20 filters (confusing for manager)  
**Fix:** Stick to 2 pages, 3-4 sheets per page, 2-3 filters total. Less is more.

### ❌ Pitfall 4: Loom video too long/short
**Problem:** 10-minute rambling video or 1-minute rushed video  
**Fix:** Write a 3-bullet script before recording. Practice once (don't wing it).

### ❌ Pitfall 5: Forgetting to export cleaned CSV
**Problem:** Notebook has cleaning code, but you never save the output  
**Fix:** Add `df_clean.to_csv('cleaned_online_orders.csv', index=False)` as the last cell of your cleaning section.

---

## Success Checklist (Before Submitting)

**Run through this list Sunday afternoon:**

### Python Notebook
- [ ] Kernel restarted and "Run All" completes without errors
- [ ] All 3 questions have code + chart + interpretation sentence
- [ ] Missing profit values are filled (not dropped)
- [ ] Dates are converted to datetime
- [ ] Categories are consistent (all title case)
- [ ] `cleaned_online_orders.csv` is exported
- [ ] Reflection section has 3-5 sentences
- [ ] AI/code sources cited (if used)

### Tableau Dashboard
- [ ] Dashboard has 2 pages (named "Executive Summary" and "Deep Dive")
- [ ] Page 1 has: 2 KPI cards + 2 bar charts + 1 filter
- [ ] Page 2 has: 1 line chart + 1 scatter + 1 heatmap + 1 filter
- [ ] At least 1 dashboard action works (click bar → filter)
- [ ] Dashboard is published to Tableau Public
- [ ] Link works in incognito mode (no login required)

### Loom Video
- [ ] Video length: 3 minutes 30 seconds to 5 minutes 30 seconds
- [ ] Covers: cleaned data (10s) + Python code (1-2 min) + Tableau (1-2 min) + reflection (30s)
- [ ] Audio is clear (no background noise)
- [ ] Link is "Unlisted" (not "Public" and not "Private")
- [ ] Link opens correctly

### Submission
- [ ] Files are in `submission_template/` folder:
  - `yourname_capstone.ipynb` (replace "yourname" with actual name)
  - `cleaned_online_orders.csv`
  - `tableau_link.txt` (contains one URL)
  - `loom_link.txt` (contains one URL)
- [ ] Git commit message: `"submit capstone - Your Name"`
- [ ] Pull Request opened against original repo
- [ ] PR description contains your Loom link (so instructor can watch without downloading)

---

## Grading Summary (40 Points Total)

| Category | Points | Passing threshold |
|----------|--------|-------------------|
| Data cleaning | 10 | 7/10 |
| Q1 answer | 5 | 3/5 |
| Q2 answer | 5 | 3/5 |
| Q3 answer | 5 | 3/5 |
| Tableau dashboard | 10 | 7/10 |
| Loom video | 5 | 3/5 |

**Passing score:** 28/40 (70%)

**Full rubric:** See `rubric.md` in this folder.

**What happens if you fail?**  
- You may resubmit once within 14 days (max grade 80%)
- Or retake in next pilot cohort (free)

---

## Resources for Capstone

### Cheat Sheets (in `resources/cheat_sheets/`)
- `pandas_cleaning_checklist.md` – Step-by-step data cleaning
- `matplotlib_common_charts.md` – Copy-paste code for bar, line, scatter
- `tableau_dashboard_checklist.md` – Verify before publishing

### Sample Code Snippets (Use These)

**Fill missing profit with category median:**
```python
df['profit'] = df.groupby('category')['profit'].transform(lambda x: x.fillna(x.median()))
```

**Fix inconsistent categories:**
```python
df['category'] = df['category'].str.title()
```

**Convert mixed-format dates:**
```python
df['order_date'] = pd.to_datetime(df['order_date'], errors='coerce')
df = df.dropna(subset=['order_date'])  # Remove rows where date failed
```

**Weekly profit trend with rolling average:**
```python
weekly_profit = df.resample('W', on='order_date')['profit'].sum()
weekly_profit.rolling(window=2).mean().plot()
```

### Previous Weeks' Solutions
- Need to remember how to group? See Week 2 solution notebook
- Need chart code? See Week 3 `matplotlib_intro.ipynb`
- Need Tableau filter help? See `tableau/tableau_guide.md`

---

## Help During Capstone Week

### Slack Channels
| Channel | Use for | Response time |
|---------|---------|---------------|
| `#capstone-help` | Code errors, debugging | Instructor: 4 hours |
| `#python-help` | Pandas/plotting questions | Peers + instructor |
| `#tableau-help` | Dashboard/filter issues | Peers + instructor |
| `#capstone-discussion` | Strategy, time management, moral support | Peer-to-peer |

### Emergency Protocol
**If you're stuck for >1 hour on one problem:**
1. Take a 15-minute break (walk, water)
2. Post in `#capstone-help` with:
   - What you're trying to do
   - Your code (paste as text, not screenshot)
   - The error message (copy-paste)
   - What you already tried
3. Move to a different question (Q2 while waiting for Q1 help)

**If you won't meet deadline:** Message instructor privately on Slack by Saturday. Extensions granted only for documented emergencies (illness, family, tech failure with proof).

---

## What "Good" Looks Like

### Example Q1 Interpretation (Good)
> "The North region generates $45,200 in total profit, which is 2.5x higher than the next highest region (East at $18,000). The South region shows a net loss of -$3,500 due to high shipping costs and low sales volume."

### Example Q2 Table (Good)
| Customer Segment | Avg Profit per Order (Electronics only) |
|----------------|------------------------------------------|
| Corporate | $87.50 |
| Consumer | $42.30 |
| Home Office | $38.20 |

### Example Loom Video Script (Good)
> "Here's my cleaned dataset – I filled 200 missing profits with the median for each category. Now let me show my Python code for Question 2. I grouped by customer segment and calculated average profit. Corporate customers spend the most on Electronics, at $87 per order. In Tableau, you can see a filter for region – when I click 'West', profit over time drops in January but recovers in March. If I had another week, I'd analyze why the South region is losing money."

---

## Final Words from Instructor

> "You have everything you need. Weeks 1-3 gave you the tools. This week is about trust – trust that you can figure it out without hand-holding. 

> Some of you will feel lost on Wednesday. That's normal. Push through. By Sunday night, you'll have a portfolio piece you're proud of.

> **Don't aim for perfect. Aim for done.** 

> See you at the finish line."

---

## Immediate Next Steps

**Right after reading this:**

1. [ ] Open `project_instructions.md` (detailed version of the 3 questions)
2. [ ] Download `online_orders.csv` from `week4-capstone/data/`
3. [ ] Open `submission_template/yourname_capstone.ipynb` in Jupyter
4. [ ] Run `df = pd.read_csv('../data/online_orders.csv')` – does it load?
5. [ ] Run `df.info()` – how many missing values?
6. [ ] Mark your calendar: Saturday office hours (11 AM–1 PM ET)

**Good luck. Start now. You've got this.** 🚀

---

**Estimated completion time:** 6-8 hours total this week

**Worth it?** Yes. This is what goes on your resume.
```

---

## How to Use This File

1. **Save as:** `week4-capstone/README.md` in your repo
2. **Replace placeholders:**
   - `[Date]` → actual week starting date
   - `[Your Name]` → your actual name
   - Verify Zoom links in the schedule section
3. **Optional additions:**
   - Add a GIF of someone finishing the capstone (celebration)
   - Embed a 2-minute "Welcome to Week 4" video
   - Link to a sample past capstone (with permission)

---

## Supporting Files You Still Need for Week 4

To make Week 4 complete, you'll also need:

| File | Status | Next step |
|------|--------|------------|
| `project_instructions.md` | ✅ Generated previously | Already have it |
| `rubric.md` | Not generated yet | Request this |
| `data/online_orders.csv` | Not generated yet | Request this (5,000 realistic rows with intentional errors) |
| `submission_template/yourname_capstone.ipynb` | Not generated yet | Request this (empty scaffold notebook) |
| `resources/capstone_tips.md` | Not generated yet | Request this (optional) |
| `capstone_kickoff_slides.pdf` | You create | Use Canva/Google Slides |
```

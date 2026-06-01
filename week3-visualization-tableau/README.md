# Week 3: Visualization + Tableau

**Week starting:** [Date]  
**Live lecture:** Tuesday 7–9 PM ET  
**Live lab:** Thursday 7–8 PM ET  
**Office hours:** Saturday 11 AM–12 PM ET

---

## Learning Objectives

By the end of this week, you will be able to:

- Create professional charts in Python using Matplotlib and Seaborn
- Customize colors, labels, and figure sizes for presentations
- Connect Tableau Public to CSV files
- Build interactive bar charts, line charts, and maps in Tableau
- Create a multi-page dashboard with filters and actions
- Publish and share interactive dashboards online

**Real-world application:** You'll transform your cleaned data from Week 2 into a shareable executive dashboard – the exact deliverable expected of junior analysts.

---

## Why Visualization Matters

Raw numbers don't persuade stakeholders. Charts do. 

**This week bridges the gap:** Python for exploration (quick, flexible) + Tableau for presentation (interactive, shareable).

> "A picture is worth a thousand rows of data." – Every data manager ever

---

## Week 3 Folder Structure

```
week3-visualization-tableau/
│
├── README.md (this file)
├── slides_python.pdf (Matplotlib/Seaborn)
├── slides_tableau.pdf (Tableau basics)
│
├── python_plots/
│   ├── matplotlib_intro.ipynb
│   ├── seaborn_intro.ipynb
│   ├── exercises/
│   │   ├── exercise1_charts_from_cleaned_data.ipynb
│   │   └── solutions/
│   └── data/
│       └── cleaned_orders.csv (from Week 2)
│
├── tableau/
│   ├── tableau_guide.md (step-by-step with screenshots)
│   ├── dashboard_checklist.md
│   └── sample_dashboard.twbx (optional reference)
│
└── tableau_exercises/
    ├── exercise2_basic_charts.md
    ├── exercise3_interactive_dashboard.md
    └── solutions/
```

---

## Before You Start (Pre-Lab Checklist)

**Complete before Tuesday's live session:**

- [ ] Week 2 exercises are complete and pushed to GitHub
- [ ] You have `cleaned_orders.csv` and `region_summary.csv` from Week 2
- [ ] Tableau Public is installed and you can log in
- [ ] Matplotlib and Seaborn are installed: `conda install matplotlib seaborn -y`
- [ ] You can run `import matplotlib.pyplot as plt` without error

**Test your Tableau:** Open Tableau Public → "Connect to Data" → "Text File" → Select any CSV → Should load preview.

**Stuck?** Post in `#setup-help` on Slack.

---

## Week 3 Schedule (Detailed)

### Tuesday: Live Lecture – Python Visualization (2 hours)

**Part 1: Matplotlib Fundamentals (1 hour)**
- Why Matplotlib? The foundation of Python plotting
- Creating figures: `plt.figure()`
- Basic plots: `plt.plot()`, `plt.bar()`, `plt.scatter()`, `plt.hist()`
- Customization: titles, labels, legends, colors, grids
- Subplots: multiple charts in one figure

**Part 2: Seaborn for Statistical Plots (1 hour)**
- Why Seaborn? Beautiful defaults + statistical insight
- `sns.barplot()` with error bars (confidence intervals)
- `sns.histplot()` for distributions
- `sns.scatterplot()` with color mapping
- `sns.pairplot()` for exploring multiple variables
- Combining Matplotlib and Seaborn

**Live coding demo:** Load `cleaned_orders.csv`, create 4 different charts showing sales trends, profit by region, and distribution of order values.

**Recording available:** Within 2 hours after session.

**Slides:** `slides_python.pdf` in this folder.

---

### Thursday: Live Lab – Tableau Dashboarding (1 hour)

**Hands-on:** Build your first Tableau dashboard from scratch.

**You'll learn:**
- Connecting to `region_summary.csv`
- Understanding dimensions (blue) vs measures (green)
- Dragging and dropping: bar chart in 30 seconds
- Adding filters: region selector
- Creating calculated fields: profit margin = profit/sales
- Building a dashboard with 2 sheets and a filter
- Publishing to Tableau Public

**Lab format:** Instructor builds live, you follow along. Last 15 minutes = you add one extra chart on your own.

**Recording available:** Within 2 hours after session.

**Guide:** `tableau/tableau_guide.md` has screenshots for every step.

---

### Saturday: Office Hours (1 hour)
**Drop-in format:** Bring your Python plot errors or Tableau design questions.

**Popular questions from previous cohorts:**
- "How do I save my Matplotlib figure as a high-res PNG?"
- "Why does my Seaborn bar chart have no error bars?"
- "How do I make a map in Tableau with my region names?"

**Link:** Posted in `#office-hours` on Slack Friday evening.

---

## Exercises Overview

### Exercise 1: Python Charts from Cleaned Data (`python_plots/exercises/exercise1_charts_from_cleaned_data.ipynb`)
**Difficulty:** ⭐⭐ (Easy-Medium)  
**Time:** 60–75 minutes

**Scenario:** You cleaned `messy_orders.csv` in Week 2. Now your manager wants 4 charts to understand sales and profit patterns.

**Tasks:**

**Chart 1: Bar Chart – Total Profit by Region**
- Use Seaborn: `sns.barplot(data=df, x='region', y='profit', estimator=sum)`
- Add title: "Total Profit by Region"
- Color: Blue for positive profit, red for negative

**Chart 2: Histogram – Distribution of Order Values**
- Use Matplotlib: `plt.hist(df['sales'], bins=20)`
- Add vertical line at median sales value
- Label axes: "Sales Amount ($)", "Number of Orders"

**Chart 3: Scatter Plot – Sales vs Profit**
- Use Seaborn: `sns.scatterplot(data=df, x='sales', y='profit', hue='region')`
- Add a horizontal line at y=0 (profit/loss threshold)
- Title: "Sales vs Profit by Region"

**Chart 4: Line Chart – Profit Over Time**
- First, convert `order_date` to datetime: `pd.to_datetime()`
- Group by week: `df.resample('W', on='order_date')['profit'].sum()`
- Plot as line with markers
- Add rolling 2-week average as dashed line

**Deliverable:** Completed notebook with all 4 charts, each in its own cell with a 1-sentence interpretation below.

**Bonus:** Create a single figure with 4 subplots (2x2 grid) showing all charts together.

---

### Exercise 2: Tableau Basic Charts (`tableau_exercises/exercise2_basic_charts.md`)
**Difficulty:** ⭐ (Easy)  
**Time:** 30 minutes

**Tasks:**
1. Connect Tableau to `cleaned_orders.csv`
2. Create a bar chart: Total Sales by Category
3. Create a line chart: Profit over time (filter to last 4 weeks)
4. Create a map: Profit by Region (use generated latitude/longitude)
5. Create a scatter plot: Sales vs Profit (color by category)

**Save each as a separate sheet** (tab at bottom of Tableau).

**Deliverable:** Tableau workbook saved to your Tableau Public profile. Share link in Slack `#week3-showcase`.

**Guide:** Follow `tableau/tableau_guide.md` sections 1-4.

---

### Exercise 3: Interactive Dashboard (`tableau_exercises/exercise3_interactive_dashboard.md`)
**Difficulty:** ⭐⭐⭐ (Medium)  
**Time:** 45–60 minutes

**Scenario:** Your manager wants one dashboard where they can filter by region and see all charts update.

**Dashboard Requirements:**

**Page 1: Executive Overview**
- Sheet 1: Bar chart – Profit by Region (from Exercise 2)
- Sheet 2: Bar chart – Sales by Category
- Sheet 3: KPI card – Total Sales (calculated field)
- Sheet 4: KPI card – Average Profit per Order
- **Filter:** Add a region filter that controls Sheets 1, 2, and 3

**Page 2: Deep Dive**
- Sheet 5: Line chart – Profit over time (from Exercise 2)
- Sheet 6: Scatter plot – Sales vs Profit (from Exercise 2)
- Sheet 7: Table – Top 10 products by quantity (requires product column – if missing, use category)
- **Action:** Click on a region in Page 1, Page 2 filters automatically

**Deliverable:** 
- Published Tableau Public dashboard (2 pages)
- URL shared in `#week3-showcase`
- One sentence in Slack: "My biggest insight from this dashboard is..."

---

## Python Plotting Reference

### Matplotlib Quick Reference

| What | Code |
|------|------|
| Basic line | `plt.plot(x, y)` |
| Bar chart | `plt.bar(x, height)` |
| Scatter | `plt.scatter(x, y)` |
| Histogram | `plt.hist(data, bins=20)` |
| Add title | `plt.title('My Title')` |
| X label | `plt.xlabel('X Axis')` |
| Y label | `plt.ylabel('Y Axis')` |
| Legend | `plt.legend()` |
| Grid | `plt.grid(True)` |
| Save figure | `plt.savefig('chart.png', dpi=300)` |
| Show plot | `plt.show()` |
| Subplots | `fig, axes = plt.subplots(2, 2)` |

### Seaborn Quick Reference

| What | Code |
|------|------|
| Bar plot | `sns.barplot(data=df, x='cat', y='num', estimator=sum)` |
| Histogram | `sns.histplot(data=df, x='num', bins=20)` |
| Scatter | `sns.scatterplot(data=df, x='num1', y='num2', hue='cat')` |
| Pairplot | `sns.pairplot(df, hue='region')` |
| Box plot | `sns.boxplot(data=df, x='cat', y='num')` |
| Style | `sns.set_style('whitegrid')` |
| Context | `sns.set_context('talk')` (larger fonts for presentations) |

### Matplotlib vs Seaborn: When to Use Which

| Use Case | Best Tool | Why |
|----------|-----------|-----|
| Quick bar chart | Seaborn | Better defaults + error bars |
| Highly customized plot | Matplotlib | Full control over every element |
| Statistical plot (box, violin) | Seaborn | Built-in statistical transformations |
| Subplots | Matplotlib | More flexible grid layout |
| Pairplot (many variables) | Seaborn | One line of code for 6+ charts |
| Saving for publication | Matplotlib | DPI control + vector formats |

---

## Tableau Reference Guide

### Key Concepts (First 30 Minutes)

| Term | Definition | Example |
|------|------------|---------|
| Dimension | Categorical data (blue) | Region, Category, Date |
| Measure | Numeric data (green) | Sales, Profit, Quantity |
| Sheet | Individual chart or table | Bar chart, line chart |
| Dashboard | Container for multiple sheets | Executive Summary page |
| Filter | Limits data shown | Region = "North" only |
| Calculated Field | New column from formula | Profit Margin = SUM(Profit)/SUM(Sales) |

### Tableau Shortcuts

| Action | Shortcut (Windows) | Shortcut (Mac) |
|--------|-------------------|----------------|
| New sheet | Ctrl + M | Cmd + M |
| New dashboard | Ctrl + Shift + D | Cmd + Shift + D |
| Undo | Ctrl + Z | Cmd + Z |
| Show/Hide cards | Ctrl + 1,2,3,4 | Cmd + 1,2,3,4 |
| Add filter | Right-click dimension → Show Filter | Same |
| Swap rows/cols | Ctrl + W | Cmd + W |

### Dashboard Design Tips (From Real Analysts)

**Do:**
- Use 3-5 sheets per dashboard max (cognitive load)
- Place filters at top or left
- Use consistent colors (e.g., blue = sales, green = profit)
- Add a title and date range context
- Test on a small screen (laptop) – if you have to scroll, it's too wide

**Don't:**
- Use pie charts with >5 categories
- Use red/green alone (colorblind users – add patterns or labels)
- Add every field as a filter (users get overwhelmed)
- Forget to publish (others can't see local work)

---

## Common Mistakes & How to Avoid Them

### Python Plotting

**❌ Mistake 1:** Forgetting `plt.show()` in scripts
```python
# Works in Jupyter, fails in .py file
plt.bar(x, y)  # No output!

# Always add
plt.bar(x, y)
plt.show()  # Forces display
```

**❌ Mistake 2:** Plotting dates without converting
```python
# Wrong (treats dates as strings)
plt.plot(df['order_date'], df['profit'])

# Correct
df['order_date'] = pd.to_datetime(df['order_date'])
plt.plot(df['order_date'], df['profit'])
```

**❌ Mistake 3:** Overlapping subplots
```python
# Wrong (second plot overwrites first)
plt.plot(x1, y1)
plt.plot(x2, y2)
plt.show()

# Correct (subplots or separate cells)
fig, (ax1, ax2) = plt.subplots(1, 2)
ax1.plot(x1, y1)
ax2.plot(x2, y2)
```

### Tableau

**❌ Mistake 1:** Can't find your CSV
- **Fix:** Tableau Public only reads local files. Save CSV to Desktop, reconnect if moved.

**❌ Mistake 2:** Dashboard filters don't work
- **Fix:** Click filter → "Apply to Worksheets" → "Selected Worksheets" → Check which sheets should update.

**❌ Mistake 3:** Map shows "unknown" for regions
- **Fix:** Tableau doesn't know "North" as a location. Use generated latitude/longitude or rename regions to actual city/state names.

**❌ Mistake 4:** Can't save locally
- **Fix:** Tableau Public saves to cloud only. Click "Save to Tableau Public As..." → log in → publish.

---

## Dataset Details

### Using Your Week 2 Outputs

You'll use two files from Week 2:

**`cleaned_orders.csv`** (1,200 rows, cleaned)
- `order_id`, `order_date`, `region`, `category`, `customer_segment`
- `sales`, `profit`, `quantity`

**`region_summary.csv`** (4 rows – one per region)
- `region`, `total_sales`, `average_profit`, `order_count`

**Where to find them:** 
- If you completed Week 2 exercises, they're in `week2-pandas/exercises/`
- If lost, re-download from `week3-visualization-tableau/python_plots/data/`

---

## Success Checklist (End of Week)

By Sunday night, you should have:

- [ ] Completed `exercise1_charts_from_cleaned_data.ipynb` (4 Python charts)
- [ ] Saved 4 charts as PNG files in your repo (optional but recommended)
- [ ] Completed Exercise 2 (5 Tableau sheets)
- [ ] Completed Exercise 3 (2-page published dashboard)
- [ ] Shared Tableau Public link in Slack `#week3-showcase`
- [ ] Pushed all notebooks to GitHub fork
- [ ] Posted `week3-done` in Slack with your biggest insight from the dashboard

**If all checkboxes are checked:** You're ready for Week 4 (Capstone Project).

---

## Help & Troubleshooting

### Python Plotting Issues

**"My plot is tiny and unreadable"**
```python
# Set figure size at beginning
plt.figure(figsize=(12, 6))
# Or for Seaborn
sns.set(rc={'figure.figsize':(12,6)})
```

**"Chinese/missing characters in labels"**
```python
# Add this for Mac/Windows
plt.rcParams['font.sans-serif'] = ['Arial']
```

**"Seaborn says 'No module named seaborn'"**
```bash
conda install seaborn -y
# Or
pip install seaborn
```

**"My dates show as 1970-01-01"**
```python
# Convert to datetime first
df['order_date'] = pd.to_datetime(df['order_date'], errors='coerce')
# Drop rows where conversion failed
df = df.dropna(subset=['order_date'])
```

### Tableau Issues

**"Tableau Public won't open my CSV"**
- Check file is not open in Excel (close Excel first)
- Save CSV as UTF-8 encoding (in Pandas: `df.to_csv('file.csv', encoding='utf-8')`)

**"My map shows dots, not regions"**
- Tableau needs latitude/longitude. Use:
  - If you have city/state names: Assign geographic role
  - If only region names: Use symbol map, not filled map

**"Dashboard is slow to load"**
- Reduce data: Filter to last 3 months
- Use extracts instead of live connections (Data → Extract)

**"Can't publish – 'Tableau Public limit reached'"**
- Free account limit: 10 workbooks. Delete old ones at public.tableau.com

### Still stuck?
1. **Slack:** Post in `#python-help` or `#tableau-help` with:
   - Error message (copy-paste)
   - Screenshot of your code or Tableau view
   - What you already tried
2. **GitHub Issue:** Use the template in `.github/ISSUE_TEMPLATE/`
3. **Office hours:** Saturday 11 AM ET – share your screen

---

## Preview: How Week 3 Connects to Week 4

In **Week 4 (Capstone)**, you'll combine everything:
- Use Pandas to clean a NEW dataset (not seen before)
- Create Python charts to explore
- Build a Tableau dashboard for presentation
- Record a Loom video walking through insights

**Your Week 3 dashboard is a practice run** for the real capstone. Save your Tableau workbook – you'll use similar techniques.

---

## Additional Resources (Optional)

### Python Plotting Tutorials
- [Matplotlib Tutorial (Official)](https://matplotlib.org/stable/tutorials/index.html)
- [Seaborn Gallery](https://seaborn.pydata.org/examples/index.html) – Copy-paste examples
- [Python Data Visualization (Real Python)](https://realpython.com/tutorials/data-viz/)

### Tableau Tutorials (Free)
- [Tableau Public Getting Started (10 min)](https://public.tableau.com/app/learn/)
- [Tableau Makeover Monday](https://makeovermonday.co.uk/) – Practice with real datasets
- [Dashboard Design Principles (YouTube)](https://youtu.be/3qjE-LlZR8E)

### Cheat Sheets (in `resources/cheat_sheets/`)
- `matplotlib_cheat_sheet.pdf`
- `seaborn_cheat_sheet.pdf`
- `tableau_shortcuts.pdf`
- `color_palettes.pdf` (choose accessible colors)

---

## Week 3 Assignment Submission

**Due:** Sunday 11:59 PM your local time

**Submit via:** GitHub Classroom + Slack

**What to submit:**
1. `exercise1_charts_from_cleaned_data.ipynb` (GitHub)
2. `python_plots/exercises/` folder with PNG exports (optional but encouraged)
3. Tableau Public dashboard URL (in Slack `#week3-showcase`)
4. One sentence insight from dashboard (in Slack)

**How to submit (Python code):**
```bash
# In your terminal (inside repo folder)
git add week3-visualization-tableau/python_plots/exercises/*.ipynb
git add week3-visualization-tableau/python_plots/*.png (if you saved)
git commit -m "complete week3 python exercises"
git push origin main
```

**How to submit (Tableau):**
- Publish to Tableau Public (File → Save to Tableau Public As...)
- Copy the share URL (looks like `https://public.tableau.com/views/...`)
- Paste in Slack `#week3-showcase` with a short insight

**Grading:** 
- Python exercises (50%): Auto-graded for plot existence
- Tableau dashboard (50%): Peer + instructor review for completeness
- No numerical grade – just Pass/Incomplete for pilot completion

**Peer feedback:** Review 2 other students' dashboards in Slack. Comment what works and one suggestion.

---

## Live Session Links

| Session | Zoom Link | Recording |
|---------|-----------|-----------|
| Tuesday Lecture (Python) | [Link in Slack] | [Available Wed] |
| Thursday Lab (Tableau) | [Link in Slack] | [Available Fri] |
| Saturday Office Hours | [Link in Slack] | [Available Sun] |

**Passcode:** Same for all sessions (posted in `#general`)

---

## Instructor Note

> "Visualization is where data becomes storytelling. Don't just make charts – make people understand. This week, focus on clarity over complexity. A simple bar chart with a clear title beats a fancy Sankey diagram every time."

> *P.S. – The Tableau dashboard you build this week is portfolio-ready. Share the link on LinkedIn after the course ends.*

---

**Ready?** Open `python_plots/matplotlib_intro.ipynb` to begin, or jump to `tableau/tableau_guide.md` if you prefer starting with Tableau.

**Estimated completion time:** 5–6 hours total this week (including lectures)

**Remember:** Python plots for exploration, Tableau for presentation. Both are valuable. Both are learnable.

---

## How to Use This File

1. **Save as:** `week3-visualization-tableau/README.md` in your repo
2. **Replace placeholders:**
   - `[Date]` → actual week starting date
   - Verify Zoom links are added before sharing with students
3. **Optional additions:**
   - Add a screenshot of an example dashboard (what "good" looks like)
   - Embed a 2-minute Loom tour of Tableau interface
   - Link to a sample Tableau Public dashboard you've made

---

## Supporting Files You Still Need for Week 3

To make Week 3 complete, you'll also need:

| File | Status | Next step |
|------|--------|------------|
| `python_plots/matplotlib_intro.ipynb` | Not generated yet | Request this |
| `python_plots/seaborn_intro.ipynb` | Not generated yet | Request this |
| `python_plots/exercises/exercise1_charts_from_cleaned_data.ipynb` | Not generated yet | Request this |
| `tableau/tableau_guide.md` | Not generated yet | Request this (screenshot-heavy) |
| `tableau_exercises/exercise2_basic_charts.md` | Not generated yet | Request this |
| `tableau_exercises/exercise3_interactive_dashboard.md` | Not generated yet | Request this |
| `tableau/sample_dashboard.twbx` | You create | Optional reference |

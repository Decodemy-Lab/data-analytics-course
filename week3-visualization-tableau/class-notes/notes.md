# Week 3 Class Notes: Visualization & Tableau

**Course:** Foundations of Data Analytics (Pilot)  
**Week:** 3 of 4  
**Prerequisites:** Weeks 1-2 completed (Python basics + Pandas data manipulation)  
**Instructor:** Amos Augo

---

## Table of Contents

1. [Why Visualization Matters](#why-visualization-matters)
2. [Introduction to Matplotlib](#introduction-to-matplotlib)
3. [Introduction to Seaborn](#introduction-to-seaborn)
4. [Matplotlib vs Seaborn: When to Use Which](#matplotlib-vs-seaborn-when-to-use-which)
5. [Chart Types & Use Cases](#chart-types--use-cases)
6. [Customizing Your Plots](#customizing-your-plots)
7. [Advanced Python Plotting](#advanced-python-plotting)
8. [Introduction to Tableau](#introduction-to-tableau)
9. [Tableau: Connecting to Data](#tableau-connecting-to-data)
10. [Tableau: Building Charts](#tableau-building-charts)
11. [Tableau: Dashboards & Interactivity](#tableau-dashboards--interactivity)
12. [Common Errors & Debugging](#common-errors--debugging)
13. [Practice Problems](#practice-problems)
14. [Cheat Sheet](#cheat-sheet)
15. [Key Takeaways](#key-takeaways)

---

## Why Visualization Matters

### The Problem with Numbers

**Raw data (hard to understand):**
```
Region: North, Profit: $12,450
Region: South, Profit: -$2,100
Region: East, Profit: $6,500
Region: West, Profit: $8,900
```

**Visualized (immediately clear):**
```
Profit by Region
North    ████████████████ $12,450
West     ████████████     $8,900
East     ████████         $6,500
South    ███ (negative)   -$2,100
```

> "A picture is worth 1,000 rows of data." – Every data manager ever

### Why Two Tools? (Python + Tableau)

| Tool | Best For | When to Use |
|------|----------|-------------|
| **Python (Matplotlib/Seaborn)** | Exploration, custom charts, automation | You need 50 charts, or need precise control |
| **Tableau** | Dashboards, interactivity, sharing | You need non-technical users to explore data |

**Real-world workflow:**
1. Use Python to **explore and clean** data
2. Use Tableau to **present and share** insights

### The Visualization Hierarchy

```
Level 1: Know your data
    ↓ (Week 2 – Pandas)
Level 2: Explore with basic plots
    ↓ (This week – Python)
Level 3: Present with polished dashboards
    ↓ (This week – Tableau)
Level 4: Tell a story with interactive visuals
    ↓ (Capstone project)
```

---

## Introduction to Matplotlib

### What is Matplotlib?

**Matplotlib** is the foundation of Python visualization. Most other Python plotting libraries are built on top of it.

```python
import matplotlib.pyplot as plt

# Basic line plot
x = [1, 2, 3, 4, 5]
y = [10, 20, 15, 30, 25]

plt.plot(x, y)
plt.show()
```

### The Anatomy of a Matplotlib Figure

```
    Title (plt.title())
        ↑
    ┌─────────────────────────────────┐
    │  Sales Trend 2024               │
    │  ↑                              │
    │  │    *                         │
    │  │   * *                         │
Y axis│  │  *   *                       │
label │  │ *     *                      │
    │  │*       *                     │
    │  └─────────────────────────────→│
    │         X axis label             │
    └─────────────────────────────────┘
         Legend (plt.legend())
```

### Basic Matplotlib Plots

**Line Plot (trends over time):**
```python
import matplotlib.pyplot as plt

# Data
months = ['Jan', 'Feb', 'Mar', 'Apr', 'May']
sales = [100, 120, 90, 150, 180]

# Create plot
plt.plot(months, sales, marker='o', linestyle='-', color='blue')

# Labels and title
plt.xlabel('Month')
plt.ylabel('Sales ($)')
plt.title('Monthly Sales Trend')

# Display
plt.show()
```

**Bar Chart (comparisons):**
```python
# Data
regions = ['North', 'South', 'East', 'West']
profits = [12450, -2100, 6500, 8900]

# Create bar chart
plt.bar(regions, profits, color=['green', 'red', 'blue', 'blue'])

# Add horizontal line at zero
plt.axhline(y=0, color='black', linestyle='-', linewidth=0.5)

plt.xlabel('Region')
plt.ylabel('Profit ($)')
plt.title('Profit by Region')
plt.show()
```

**Scatter Plot (relationship between two variables):**
```python
# Data
sales = [100, 250, 75, 400, 120, 300, 80, 500]
profit = [10, 50, -5, 80, 20, 60, -2, 95]

# Create scatter plot
plt.scatter(sales, profit, alpha=0.7, color='blue')

# Add trend line (simple)
import numpy as np
z = np.polyfit(sales, profit, 1)
p = np.poly1d(z)
plt.plot(sales, p(sales), "r--", alpha=0.5)

plt.xlabel('Sales ($)')
plt.ylabel('Profit ($)')
plt.title('Sales vs Profit')
plt.axhline(y=0, color='gray', linestyle='-', linewidth=0.5)
plt.show()
```

**Histogram (distribution of values):**
```python
# Data (100 random sales amounts)
import numpy as np
np.random.seed(42)
sales = np.random.normal(150, 50, 100)  # Mean 150, std 50, 100 values

# Create histogram
plt.hist(sales, bins=20, edgecolor='black', alpha=0.7)

plt.xlabel('Sales Amount ($)')
plt.ylabel('Frequency')
plt.title('Distribution of Sales Amounts')
plt.axvline(x=sales.mean(), color='red', linestyle='--', label=f'Mean: ${sales.mean():.0f}')
plt.legend()
plt.show()
```

### Multiple Plots in One Figure (Subplots)

```python
# Create a 2x2 grid of plots
fig, axes = plt.subplots(2, 2, figsize=(10, 8))

# Plot 1: Line chart (top-left)
axes[0, 0].plot(months, sales, marker='o')
axes[0, 0].set_title('Sales Trend')
axes[0, 0].set_ylabel('Sales')

# Plot 2: Bar chart (top-right)
axes[0, 1].bar(regions, profits)
axes[0, 1].set_title('Profit by Region')
axes[0, 1].set_ylabel('Profit')

# Plot 3: Scatter plot (bottom-left)
axes[1, 0].scatter(sales, profit)
axes[1, 0].set_title('Sales vs Profit')
axes[1, 0].set_xlabel('Sales')
axes[1, 0].set_ylabel('Profit')

# Plot 4: Histogram (bottom-right)
axes[1, 1].hist(sales, bins=15)
axes[1, 1].set_title('Sales Distribution')
axes[1, 1].set_xlabel('Sales')

# Adjust spacing between plots
plt.tight_layout()
plt.show()
```

### Saving Figures

```python
# Save before plt.show() (important!)
plt.plot(months, sales)
plt.title('Monthly Sales')
plt.savefig('sales_chart.png', dpi=300, bbox_inches='tight')
plt.show()  # Now display

# Other formats
plt.savefig('chart.pdf')      # Vector format (for publications)
plt.savefig('chart.svg')      # Web format
```

---

## Introduction to Seaborn

### What is Seaborn?

**Seaborn** is a statistical visualization library built on Matplotlib. It has:
- Better default colors and styles
- Built-in statistical aggregations
- Easier syntax for complex plots

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Set style (one line makes everything look better)
sns.set_style('whitegrid')

# Basic bar plot (automatically shows confidence intervals)
sns.barplot(data=df, x='region', y='profit', estimator=sum)
plt.show()
```

### Seaborn vs Matplotlib: Same Data, Different Look

**Matplotlib:**
```python
plt.bar(regions, profits)
plt.show()
# Plain gray bars, no error bars, basic look
```

**Seaborn:**
```python
sns.barplot(x=regions, y=profits)
plt.show()
# Styled bars, confidence intervals, better colors
```

### Essential Seaborn Plots

**Bar Plot (with error bars):**
```python
# Load your cleaned data from Week 2
import pandas as pd
df = pd.read_csv('week2-pandas/exercises/cleaned_orders.csv')

# Bar plot with error bars (shows variability)
sns.barplot(data=df, x='region', y='profit', estimator=sum, ci=95)
plt.title('Total Profit by Region with 95% Confidence Interval')
plt.ylabel('Total Profit ($)')
plt.show()
```

**Box Plot (shows distribution):**
```python
# Box plot shows median, quartiles, and outliers
sns.boxplot(data=df, x='region', y='sales')
plt.title('Sales Distribution by Region')
plt.ylabel('Sales ($)')
plt.show()

# What you see in a box plot:
#     Outliers (dots)
#     ┌─ Upper whisker (75th percentile + 1.5*IQR)
#     │ ┌─ 75th percentile
#     │ │ ┌─ Median (50th)
#     │ │ │ ┌─ 25th percentile
#     │ │ │ │ ┌─ Lower whisker
#     ▼ ▼ ▼ ▼ ▼
#     o |---[===|===]---|
```

**Histogram + KDE (distribution):**
```python
# Histogram with Kernel Density Estimate (smooth curve)
sns.histplot(df['sales'], bins=30, kde=True)
plt.title('Sales Distribution with Density Curve')
plt.xlabel('Sales ($)')
plt.show()
```

**Scatter Plot with Regression Line:**
```python
# Scatter with automatic regression line
sns.regplot(data=df, x='sales', y='profit', scatter_kws={'alpha':0.5})
plt.title('Sales vs Profit with Regression Line')
plt.show()
```

**Scatter Plot with Color Mapping:**
```python
# Color points by region
sns.scatterplot(data=df, x='sales', y='profit', hue='region', alpha=0.7)
plt.title('Sales vs Profit by Region')
plt.legend(title='Region')
plt.show()
```

**Pairplot (multiple relationships at once):**
```python
# Shows all pairwise relationships (can be slow for large data)
sns.pairplot(df[['sales', 'profit', 'quantity']])
plt.show()

# Output: Grid of plots
#     sales   profit   quantity
# sales  █       .         .
# profit .       █         .
# quantity .     .         █
```

**Heatmap (correlation matrix):**
```python
# Calculate correlations between numeric columns
correlation = df[['sales', 'profit', 'quantity']].corr()

# Create heatmap
sns.heatmap(correlation, annot=True, cmap='coolwarm', center=0)
plt.title('Correlation Matrix')
plt.show()

# Interpretation:
# 1.0 = perfect positive correlation
# -1.0 = perfect negative correlation
# 0 = no correlation
```

---

## Matplotlib vs Seaborn: When to Use Which

| Use Case | Best Tool | Why |
|----------|-----------|-----|
| Quick bar chart | Seaborn | Better defaults, error bars built-in |
| Highly customized plot | Matplotlib | Full control over every element |
| Statistical plot (box, violin) | Seaborn | Built-in statistical transformations |
| Subplots | Matplotlib | More flexible grid layout |
| Pairplot (many variables) | Seaborn | One line of code for 6+ charts |
| Time series with dates | Matplotlib | More control over date formatting |
| Saving for publication | Matplotlib | DPI control + vector formats |
| Dashboard (interactive) | Tableau (not Python) | Python not built for interactivity |

### Combining Matplotlib and Seaborn

```python
# Seaborn for the plot, Matplotlib for customization
import matplotlib.pyplot as plt
import seaborn as sns

# Seaborn creates the plot
sns.set_style('whitegrid')
plot = sns.barplot(data=df, x='region', y='profit', estimator=sum)

# Matplotlib customizes it
plt.title('Profit by Region', fontsize=16, fontweight='bold')
plt.xlabel('Region', fontsize=12)
plt.ylabel('Total Profit ($)', fontsize=12)
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

---

## Chart Types & Use Cases

### Choosing the Right Chart

| Question You're Answering | Best Chart | Example |
|---------------------------|------------|---------|
| How does this change over time? | Line chart | Monthly sales trend |
| How do categories compare? | Bar chart | Profit by region |
| What is the distribution? | Histogram | Order value spread |
| Are two variables related? | Scatter plot | Sales vs profit |
| What is the composition? | Pie/Bar (avoid pie) | Market share |
| Where is this located? | Map | Sales by state |

### Chart Checklist (Before You Plot)

**Ask yourself:**
1. **Who is my audience?** (Executive? Analyst? Public?)
2. **What is the one insight?** (One chart = one message)
3. **Is this the right chart type?** (Don't force a pie chart)
4. **Can I remove clutter?** (Less ink = more clarity)

### Common Chart Mistakes (And How to Fix)

| Mistake | Why It's Bad | Fix |
|---------|--------------|-----|
| Pie chart with 8 slices | Impossible to compare | Use bar chart |
| Missing axis labels | No context | Add `plt.xlabel()` |
| Too many colors | Confusing | Use sequential palette |
| 3D bar charts | Distorts perception | Use 2D |
| No title | Unclear purpose | Add `plt.title()` |

---

## Customizing Your Plots

### Colors

```python
# Matplotlib color options
plt.plot(x, y, color='red')           # Named color
plt.plot(x, y, color='#FF5733')       # Hex code
plt.plot(x, y, color=(0.2, 0.4, 0.6)) # RGB (0-1 range)

# Seaborn color palettes
sns.set_palette('deep')        # Default
sns.set_palette('pastel')      # Soft colors
sns.set_palette('dark')        # Dark colors
sns.set_palette('colorblind')  # Accessible
sns.set_palette('viridis')     # Sequential (good for heatmaps)

# Custom palette
custom_palette = ['#2ecc71', '#e74c3c', '#3498db', '#f39c12']
sns.set_palette(custom_palette)
```

### Fonts and Labels

```python
plt.title('My Title', fontsize=16, fontweight='bold', fontfamily='Arial')
plt.xlabel('X Axis', fontsize=12, fontstyle='italic')
plt.ylabel('Y Axis', fontsize=12)

# Rotate x-axis labels (prevents overlap)
plt.xticks(rotation=45, ha='right')

# Format y-axis as currency
from matplotlib.ticker import FuncFormatter
def currency(x, p):
    return f'${x:,.0f}'
plt.gca().yaxis.set_major_formatter(FuncFormatter(currency))
```

### Legends and Annotations

```python
# Add legend
plt.plot(x1, y1, label='Series A')
plt.plot(x2, y2, label='Series B')
plt.legend(loc='upper left', frameon=True, fancybox=True)

# Add text annotation
plt.annotate('Highest point', xy=(4, 180), xytext=(3, 200),
             arrowprops=dict(facecolor='black', shrink=0.05))

# Add vertical line
plt.axvline(x=100, color='red', linestyle='--', alpha=0.5)

# Add horizontal line
plt.axhline(y=0, color='gray', linestyle='-', linewidth=0.5)

# Add text box
plt.text(1, 150, 'Note: Data from Jan-Mar', fontsize=8, 
         bbox=dict(facecolor='white', alpha=0.8))
```

### Figure Size and DPI

```python
# Control figure size (width, height) in inches
plt.figure(figsize=(12, 6))

# Control resolution for saving
plt.savefig('chart.png', dpi=300)  # 300 DPI = print quality

# For presentations (16:9 aspect ratio)
plt.figure(figsize=(12, 6.75))  # 16:9 ratio

# For reports (8.5x11 page)
plt.figure(figsize=(8, 6))
```

---

## Advanced Python Plotting

### Time Series Plotting

```python
# Ensure date is datetime
df['order_date'] = pd.to_datetime(df['order_date'])

# Set date as index
df_time = df.set_index('order_date')

# Daily profit
daily_profit = df_time.groupby(df_time.index)['profit'].sum()

# Plot
plt.figure(figsize=(12, 6))
plt.plot(daily_profit.index, daily_profit.values, marker='.', linestyle='-', alpha=0.7)

# Add rolling average (7-day)
rolling_avg = daily_profit.rolling(window=7).mean()
plt.plot(rolling_avg.index, rolling_avg.values, color='red', linewidth=2, label='7-day avg')

plt.title('Daily Profit Trend')
plt.xlabel('Date')
plt.ylabel('Profit ($)')
plt.legend()
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Multiple Lines on One Plot

```python
# Pivot data to get one line per region
pivot_profit = df.pivot_table(values='profit', index='order_date', columns='region', aggfunc='sum')

# Plot all regions
plt.figure(figsize=(12, 6))
for region in pivot_profit.columns:
    plt.plot(pivot_profit.index, pivot_profit[region], label=region)

plt.title('Profit Trends by Region')
plt.xlabel('Date')
plt.ylabel('Profit ($)')
plt.legend()
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Customizing Seaborn Styles

```python
# Available styles
sns.set_style('whitegrid')     # Default (good for presentations)
sns.set_style('darkgrid')      # Dark background
sns.set_style('white')         # Plain white (good for reports)
sns.set_style('ticks')         # Minimal

# Context (size of elements)
sns.set_context('paper')       # Small (for papers)
sns.set_context('notebook')    # Default
sns.set_context('talk')        # Larger (for presentations)
sns.set_context('poster')      # Largest (for posters)

# Combine style + context
sns.set_style('whitegrid')
sns.set_context('talk')
```

### Plotting from Pandas Directly

```python
# Pandas has built-in plotting (uses Matplotlib)
df.groupby('region')['profit'].sum().plot(kind='bar')
plt.title('Profit by Region')
plt.show()

# Line plot from DataFrame
df.set_index('order_date')['profit'].plot()
plt.show()

# Histogram from Series
df['sales'].hist(bins=30)
plt.show()
```

---

## Introduction to Tableau

### What is Tableau?

**Tableau** is a business intelligence tool for creating interactive dashboards. Unlike Python, Tableau:
- Requires **no coding**
- Creates **interactive** charts (click to filter)
- Publishes **online** for sharing
- Refreshes data automatically

### Tableau Public vs Tableau Desktop

| Feature | Tableau Public (Free) | Tableau Desktop ($70/month) |
|---------|----------------------|------------------------------|
| Cost | Free | $840/year |
| Save locally | ❌ Cloud only | ✅ Yes |
| Share link | ✅ Public | ❌ Private only |
| Data size | 10M rows | Unlimited |
| For this course | ✅ Perfect | ❌ Not needed |

### Tableau Interface Overview

```
┌─────────────────────────────────────────────────────────────┐
│  Menu Bar                                                   │
├─────────────────────────────────────────────────────────────┤
│  Data Pane  │  Canvas (where you build charts)              │
│  ┌────────┐ │  ┌─────────────────────────────────────────┐  │
│  │Columns │ │  │                                         │  │
│  │Regions │ │  │                                         │  │
│  │Sales   │ │  │                                         │  │
│  │Profit  │ │  │                                         │  │
│  └────────┘ │  │                                         │  │
│             │  │                                         │  │
│  Pages Card │  │                                         │  │
│  Filters    │  │                                         │  │
│  Marks Card │  │                                         │  │
│  (Color,    │  │                                         │  │
│   Size,     │  │                                         │  │
│   Label)    │  │                                         │  │
├─────────────┴──┴─────────────────────────────────────────┤  │
│  Sheets Tabs (Sheet 1, Sheet 2, Dashboard 1)              │
└───────────────────────────────────────────────────────────┘
```

### Key Tableau Concepts

| Term | Definition | Python Equivalent |
|------|------------|-------------------|
| **Dimension** | Categorical data (blue) | String/category column |
| **Measure** | Numeric data (green) | Numeric column |
| **Sheet** | Individual chart | One Matplotlib figure |
| **Dashboard** | Collection of sheets | Multiple subplots + interactivity |
| **Filter** | Limits data shown | `df[df['region'] == 'North']` |
| **Calculated Field** | New column from formula | `df['new'] = df['a'] + df['b']` |

**Memory trick:** 
- **Blue (Dimensions)** = "Bins" (categories like Region, Date)
- **Green (Measures)** = "Numbers" (Sales, Profit, Quantity)

---

## Tableau: Connecting to Data

### Step 1: Connect to CSV

1. Open Tableau Public
2. On left sidebar, click **"Connect to Data"**
3. Click **"Text File"** (for CSV)
4. Navigate to `cleaned_orders.csv` (from Week 2)
5. Click **"Open"**

### Step 2: Understand the Data Pane

After connecting, you'll see:

```
Data Pane
├── Dimensions (blue)
│   ├── order_id
│   ├── region
│   ├── category
│   ├── customer_segment
│   └── order_date
│
└── Measures (green)
    ├── sales
    ├── profit
    └── quantity
```

**Drag fields to the canvas to build charts.**

### Step 3: Data Preparation in Tableau (Basic)

```python
# Things you CAN do in Tableau:
# - Hide/rename columns
# - Create calculated fields
# - Split columns
# - Filter data at source

# Things you SHOULD do in Python (before Tableau):
# - Handle missing values
# - Fix inconsistent categories
# - Remove duplicates
# - Create summary aggregations
```

**Rule:** Clean in Python, visualize in Tableau.

---

## Tableau: Building Charts

### Bar Chart (Profit by Region)

**Step-by-step:**
1. Drag **`region`** (dimension) to **Columns**
2. Drag **`profit`** (measure) to **Rows**
3. Tableau automatically creates a bar chart

**To sort:** Hover over axis → click sort icon (descending)

**To add labels:** Drag **`profit`** to **Labels** on Marks card

### Line Chart (Profit Over Time)

**Step-by-step:**
1. Drag **`order_date`** (dimension) to **Columns**
2. Right-click on `order_date` → choose **"Month"** (or "Day", "Week")
3. Drag **`profit`** to **Rows**

**To add multiple lines by region:**
1. Drag **`region`** to **Color** on Marks card
2. You now have one line per region

### Scatter Plot (Sales vs Profit)

**Step-by-step:**
1. Drag **`sales`** to **Columns**
2. Drag **`profit`** to **Rows**
3. Drag **`category`** to **Color** (optional)
4. Drag **`quantity`** to **Size** (larger dots = more quantity)

### Geographic Map (Profit by Region)

**Step-by-step:**
1. Double-click **`region`** (Tableau may generate map)
2. If not automatic: Assign geographic role
   - Right-click `region` → Geographic Role → State/Province
3. Drag **`profit`** to **Color**
4. Tableau creates a filled map

### Creating a Calculated Field

**Scenario:** Calculate profit margin (profit / sales)

**Step-by-step:**
1. Right-click in Data Pane → **"Create Calculated Field"**
2. Name: `Profit Margin`
3. Formula: `SUM(profit) / SUM(sales)`
4. Click OK
5. Drag new field to canvas

### Formatting Your Chart

**To edit axis:**
- Right-click axis → **"Edit Axis"**
- Change range, tick marks, title

**To edit colors:**
- Click **"Color"** on Marks card
- Choose palette, opacity, border

**To edit labels:**
- Drag field to **"Label"** on Marks card
- Click **"Label"** → Format

---

## Tableau: Dashboards & Interactivity

### Creating a Dashboard

**Step-by-step:**
1. Click **"New Dashboard"** (bottom, next to sheets)
2. Drag sheets from left pane onto dashboard
3. Arrange and resize

### Dashboard Layout Tips

```
Executive Dashboard (Good layout)
┌─────────────────────────────────────────┐
│  Title: Sales Dashboard (Q1 2024)       │
├──────────────┬──────────────────────────┤
│  Filters:    │                          │
│  [Region ▼]  │                          │
│  [Date ▼]    │                          │
├──────────────┼──────────────────────────┤
│              │                          │
│  KPI: $45K   │  Bar Chart:              │
│  Total Sales │  Profit by Region        │
│              │                          │
├──────────────┼──────────────────────────┤
│              │                          │
│  Line Chart: │  Table:                  │
│  Trend       │  Top Products            │
│              │                          │
└──────────────┴──────────────────────────┘
```

### Adding Filters

**To filter all charts by region:**
1. Drag **`region`** from Data Pane to **"Filters"** card on dashboard
2. Choose "Single Value (dropdown)"
3. Click dropdown arrow → **"Apply to Worksheets"** → **"All Using This Data Source"**

### Dashboard Actions (Interactivity)

**Action:** Click a bar → filter other charts

**Step-by-step:**
1. Dashboard → **"Actions"** (top menu)
2. **"Add Action"** → **"Filter"**
3. Source Sheet: (the chart you click)
4. Target Sheets: (charts that should update)
5. Click OK

### Publishing Your Dashboard

**Step-by-step:**
1. File → **"Save to Tableau Public As..."**
2. Log in to your account
3. Name your workbook
4. Click **"Save"**
5. Copy the share URL

**Your dashboard is now live at:** `https://public.tableau.com/views/YourDashboard`

---

## Common Errors & Debugging

### Python Plotting

**Error: "ModuleNotFoundError: No module named 'matplotlib'"**
```bash
conda install matplotlib seaborn -y
```

**Error: "KeyError: 'column_name'"**
```python
# Check exact column names
print(df.columns.tolist())
# Use exact spelling (case-sensitive)
```

**Error: "ValueError: could not convert string to float"**
```python
# Column has non-numeric values
print(df['column'].unique())
# Clean the data first
df['column'] = pd.to_numeric(df['column'], errors='coerce')
```

**Error: Chinese/blank characters in plot**
```python
# Set font for Mac/Windows
plt.rcParams['font.sans-serif'] = ['Arial']
```

**Error: Plot is cut off (labels missing)**
```python
plt.tight_layout()  # Add before plt.show()
plt.savefig('chart.png', bbox_inches='tight')  # For saving
```

### Tableau Issues

**Error: "Tableau Public won't open my CSV"**
- Close Excel if file is open
- Save CSV with UTF-8 encoding: `df.to_csv('file.csv', encoding='utf-8')`

**Error: "Map shows 'unknown' for regions"**
- Tableau doesn't recognize "North" as a location
- Fix: Use city/state names, or use symbol map instead of filled map

**Error: "Dashboard is slow to load"**
- Reduce data: Filter to last 3 months
- Create an extract: Data → Extract

**Error: "Can't save dashboard"**
- Tableau Public saves to cloud only
- Use "Save to Tableau Public As..." not "Save As"

**Error: "Filters don't affect all charts"**
- Click filter → "Apply to Worksheets" → "Selected Worksheets"
- Check which sheets should be affected

---

## Practice Problems

### Beginner (Python)

**Problem 1:** Load `cleaned_orders.csv` from Week 2. Create a bar chart of total profit by category using Seaborn.

```python
# Solution
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv('week2-pandas/exercises/cleaned_orders.csv')

sns.barplot(data=df, x='category', y='profit', estimator=sum)
plt.title('Total Profit by Category')
plt.ylabel('Total Profit ($)')
plt.show()
```

**Problem 2:** Create a histogram of sales amounts with 30 bins and a red vertical line at the mean.

```python
# Solution
plt.figure(figsize=(10, 6))
plt.hist(df['sales'], bins=30, edgecolor='black', alpha=0.7)
plt.axvline(x=df['sales'].mean(), color='red', linestyle='--', linewidth=2, label=f'Mean: ${df["sales"].mean():.0f}')
plt.xlabel('Sales Amount ($)')
plt.ylabel('Frequency')
plt.title('Distribution of Sales Amounts')
plt.legend()
plt.show()
```

### Beginner (Tableau)

**Problem 3:** Connect to `cleaned_orders.csv` in Tableau. Create a bar chart showing total sales by region, sorted descending.

**Step-by-step solution:**
1. Connect to CSV
2. Drag `region` to Columns
3. Drag `sales` to Rows
4. Hover over axis → click sort icon (descending)

**Problem 4:** Create a line chart showing profit over time by month. Add a filter for category.

**Step-by-step solution:**
1. Drag `order_date` to Columns → right-click → Month
2. Drag `profit` to Rows
3. Drag `category` to Color
4. Drag `category` to Filters → choose "Electronics" only

### Intermediate (Python)

**Problem 5:** Create a 2x2 subplot figure showing:
- Top-left: Bar chart (profit by region)
- Top-right: Histogram (sales distribution)
- Bottom-left: Scatter plot (sales vs profit)
- Bottom-right: Box plot (sales by category)

```python
# Solution
fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# Top-left: Bar chart
sns.barplot(data=df, x='region', y='profit', estimator=sum, ax=axes[0, 0])
axes[0, 0].set_title('Profit by Region')

# Top-right: Histogram
axes[0, 1].hist(df['sales'], bins=30, edgecolor='black')
axes[0, 1].set_title('Sales Distribution')
axes[0, 1].set_xlabel('Sales')

# Bottom-left: Scatter plot
sns.scatterplot(data=df, x='sales', y='profit', hue='region', ax=axes[1, 0])
axes[1, 0].set_title('Sales vs Profit by Region')

# Bottom-right: Box plot
sns.boxplot(data=df, x='category', y='sales', ax=axes[1, 1])
axes[1, 1].set_title('Sales by Category')
axes[1, 1].set_xticklabels(axes[1, 1].get_xticklabels(), rotation=45)

plt.tight_layout()
plt.show()
```

**Problem 6:** Create a line chart with a 7-day rolling average.

```python
# Solution
# Ensure date is datetime and set as index
df['order_date'] = pd.to_datetime(df['order_date'])
df_daily = df.groupby('order_date')['profit'].sum().reset_index()

# Calculate rolling average
df_daily['rolling_avg'] = df_daily['profit'].rolling(window=7).mean()

# Plot
plt.figure(figsize=(12, 6))
plt.plot(df_daily['order_date'], df_daily['profit'], alpha=0.3, label='Daily')
plt.plot(df_daily['order_date'], df_daily['rolling_avg'], color='red', linewidth=2, label='7-day avg')
plt.xlabel('Date')
plt.ylabel('Profit ($)')
plt.title('Daily Profit with 7-Day Rolling Average')
plt.legend()
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

### Intermediate (Tableau)

**Problem 7:** Build a 2-page dashboard:
- Page 1: Executive Summary (KPI cards + bar charts)
- Page 2: Deep Dive (scatter plot + line chart + filter)

**Step-by-step solution:**
1. Create sheets:
   - Sheet 1: Bar chart (profit by region)
   - Sheet 2: Bar chart (sales by category)
   - Sheet 3: Scatter plot (sales vs profit)
   - Sheet 4: Line chart (profit over time)
   - Sheet 5: KPI – Total Sales (calculated field)
   - Sheet 6: KPI – Total Profit (calculated field)

2. Build Page 1:
   - New Dashboard → drag Sheet 5, Sheet 6 (KPI cards)
   - Add Sheet 1 and Sheet 2
   - Add region filter

3. Build Page 2:
   - New Dashboard → add Sheet 3 and Sheet 4
   - Add category filter
   - Create action: click scatter point → filter line chart

### Challenge (Python)

**Problem 8:** Create a correlation heatmap with annotated values.

```python
# Solution
# Select only numeric columns
numeric_cols = df.select_dtypes(include=['float64', 'int64']).columns

# Calculate correlation
correlation = df[numeric_cols].corr()

# Create heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(correlation, annot=True, cmap='coolwarm', center=0, 
            square=True, fmt='.2f', linewidths=0.5)
plt.title('Correlation Matrix of Numeric Variables')
plt.tight_layout()
plt.show()

# Interpretation of output:
# - Values close to 1.0: strong positive correlation (both increase together)
# - Values close to -1.0: strong negative correlation (one increases, the other decreases)
# - Values close to 0: no linear relationship
```

---

### Challenge (Tableau)

**Problem 9:** Create a dashboard with a parameter that allows the user to switch between viewing SUM(profit) and AVG(profit) in a bar chart.

**Step-by-step solution:**
1. Create a parameter:
   - Right-click in Data Pane → Create → Parameter
   - Name: `Profit Aggregation`
   - Data type: String
   - Allowable values: List
   - Values: `Total Profit`, `Average Profit`

2. Create a calculated field:
   - Right-click → Create Calculated Field
   - Name: `Dynamic Profit`
   - Formula:
     ```
     IF [Profit Aggregation] = 'Total Profit' THEN 
         SUM([profit])
     ELSE 
         AVG([profit])
     END
     ```

3. Build bar chart:
   - Drag `region` to Columns
   - Drag `Dynamic Profit` to Rows
   - Show parameter control: Right-click parameter → Show Parameter Control

4. User can now toggle between total and average profit

---

## Cheat Sheet

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
| Figure size | `plt.figure(figsize=(10, 6))` |
| Rotate x labels | `plt.xticks(rotation=45)` |
| Add horizontal line | `plt.axhline(y=0, color='red')` |
| Add vertical line | `plt.axvline(x=100, color='red')` |

### Seaborn Quick Reference

| What | Code |
|------|------|
| Bar plot | `sns.barplot(data=df, x='cat', y='num', estimator=sum)` |
| Histogram + KDE | `sns.histplot(data=df, x='num', bins=30, kde=True)` |
| Scatter | `sns.scatterplot(data=df, x='num1', y='num2', hue='cat')` |
| Box plot | `sns.boxplot(data=df, x='cat', y='num')` |
| Violin plot | `sns.violinplot(data=df, x='cat', y='num')` |
| Pairplot | `sns.pairplot(df, hue='region')` |
| Heatmap | `sns.heatmap(df.corr(), annot=True)` |
| Regression plot | `sns.regplot(data=df, x='x', y='y')` |
| Set style | `sns.set_style('whitegrid')` |
| Set context | `sns.set_context('talk')` |
| Set palette | `sns.set_palette('viridis')` |

### Tableau Quick Reference

| Action | How to Do It |
|--------|--------------|
| Connect to CSV | Connect → Text File → Select file |
| Create bar chart | Drag dimension to Columns, measure to Rows |
| Create line chart | Same as bar, but change chart type in Marks card |
| Add filter | Drag dimension to Filters card |
| Create calculated field | Right-click Data Pane → Create Calculated Field |
| Create dashboard | Click New Dashboard tab (bottom) |
| Add sheets to dashboard | Drag from left pane onto dashboard |
| Create dashboard action | Dashboard → Actions → Add Action → Filter |
| Publish | File → Save to Tableau Public As... |

### Tableau Dashboard Design Checklist

| Element | Good Practice | Avoid |
|---------|--------------|-------|
| Number of sheets | 3-5 per dashboard | 10+ sheets on one page |
| Filters | Place at top or left | Scattered randomly |
| Colors | Consistent (blue=sales, green=profit) | Rainbow (too many colors) |
| Labels | Clear, readable font | Tiny, overlapping text |
| Title | Descriptive ("Q1 2024 Sales") | Vague ("Dashboard 1") |
| Interactivity | At least 1 filter or action | Static only |

---

## Key Takeaways

By the end of Week 3, you should understand:

### Python Visualization (Matplotlib/Seaborn)

1. **Matplotlib is the foundation** – most Python plotting libraries build on it
2. **Seaborn has better defaults** – use it for quick, beautiful plots
3. **The 4 essential plots** – line (trends), bar (comparisons), scatter (relationships), histogram (distributions)
4. **Customization is key** – titles, labels, colors, and legends make charts understandable
5. **Subplots show multiple views** – use `plt.subplots()` for side-by-side comparisons

### Tableau Visualization

6. **Blue (dimensions) vs Green (measures)** – categories vs numbers
7. **Drag-and-drop interface** – no coding needed for basic charts
8. **Dashboards combine sheets** – multiple views in one page
9. **Filters add interactivity** – users can explore their own questions
10. **Public sharing is easy** – one click to publish online

### The Python → Tableau Workflow

```
Week 2 (Pandas)           Week 3 (Python plots)      Week 3 (Tableau)
     ↓                           ↓                          ↓
Clean messy data    →    Explore with Python      →    Present with Tableau
(handle missing,         (find patterns,           (build interactive
 fix types,               test hypotheses)          dashboard for sharing)
 remove outliers)
```

**What comes next:** In Week 4 (Capstone), you'll combine everything:
- Clean a NEW messy dataset (Pandas)
- Explore with Python plots (Matplotlib/Seaborn)
- Build a Tableau dashboard
- Present findings in a Loom video

---

## Additional Resources

### Python Visualization
- [Matplotlib Gallery](https://matplotlib.org/stable/gallery/index.html) – Copy-paste examples
- [Seaborn Gallery](https://seaborn.pydata.org/examples/index.html) – Beautiful examples with code
- [Python Data Visualization (Real Python)](https://realpython.com/tutorials/data-viz/)

### Tableau Learning (Free)
- [Tableau Public Getting Started](https://public.tableau.com/app/learn/) – Official tutorials
- [Tableau Makeover Monday](https://makeovermonday.co.uk/) – Weekly practice with real datasets
- [Dashboard Design Principles (YouTube)](https://youtu.be/3qjE-LlZR8E) – 10 minutes on best practices

### Color Palettes (Accessible)
- [ColorBrewer](https://colorbrewer2.org/) – Colorblind-friendly palettes
- [Viridis Palette](https://matplotlib.org/stable/users/explain/colors/colormaps.html) – Sequential, perceptually uniform

---

## Office Hours & Support

- **Slack:** `#python-help` (Python plots) and `#tableau-help` (Tableau questions)
- **Office hours:** Saturday 11 AM–12 PM ET
- **GitHub Issues:** For code submission problems

**Remember:** 
- Python plots for **exploration** (you can make 50 charts quickly)
- Tableau for **presentation** (one polished dashboard is better than 50 messy ones)
- The best chart is the one that answers the question

> "Don't make me think. Every chart should have one clear takeaway." – Data visualization best practice

---

**End of Week 3 Class Notes**

*Save this document. You'll use it in Week 4 for your capstone project.*

---

## Complete Week 3 Notes Summary

| Section | Pages (approx) | Key Topics |
|---------|---------------|------------|
| Why Visualization Matters | 1 | Python vs Tableau, hierarchy |
| Matplotlib | 3 | Line, bar, scatter, histogram, subplots |
| Seaborn | 2 | Bar, box, scatter, pairplot, heatmap |
| Chart Types & Use Cases | 1 | Choosing the right chart |
| Customization | 2 | Colors, fonts, legends, annotations |
| Advanced Plotting | 1 | Time series, multiple lines, Pandas plotting |
| Tableau Introduction | 2 | Interface, dimensions vs measures |
| Tableau Building Charts | 2 | Bar, line, scatter, maps, calculated fields |
| Tableau Dashboards | 2 | Layout, filters, actions, publishing |
| Common Errors | 2 | Python + Tableau troubleshooting |
| Practice Problems | 3 | 9 problems with solutions |
| Cheat Sheet | 1 | Quick reference for both tools |
| Key Takeaways | 1 | Summary of what you learned |

**Total length:** ~4,500 words, ~200 code examples, 9 practice problems

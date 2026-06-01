# Tableau Guide: From Zero to Dashboard

**Course:** Foundations of Data Analytics (Pilot)  
**Week:** 3  
**Tool:** Tableau Public (free)  
**Time to complete:** 1-2 hours

---

## Table of Contents

1. [What is Tableau?](#what-is-tableau)
2. [Installing Tableau Public](#installing-tableau-public)
3. [Tableau Interface Overview](#tableau-interface-overview)
4. [Connecting to Data](#connecting-to-data)
5. [Understanding Dimensions vs Measures](#understanding-dimensions-vs-measures)
6. [Building Your First Chart (Bar Chart)](#building-your-first-chart-bar-chart)
7. [Building a Line Chart](#building-a-line-chart)
8. [Building a Scatter Plot](#building-a-scatter-plot)
9. [Building a Geographic Map](#building-a-geographic-map)
10. [Creating Calculated Fields](#creating-calculated-fields)
11. [Adding Filters](#adding-filters)
12. [Building a Dashboard](#building-a-dashboard)
13. [Adding Dashboard Actions (Interactivity)](#adding-dashboard-actions-interactivity)
14. [Publishing to Tableau Public](#publishing-to-tableau-public)
15. [Common Issues & Fixes](#common-issues--fixes)
16. [Keyboard Shortcuts](#keyboard-shortcuts)
17. [Practice Exercises](#practice-exercises)

---

## What is Tableau?

**Tableau** is a business intelligence tool that lets you create interactive dashboards without coding.

| Feature | What It Means |
|---------|---------------|
| Drag-and-drop | Build charts by dragging fields, not writing code |
| Interactive | Users can click, filter, and explore on their own |
| Web-based | Publish once, share a link, anyone can view |
| Free version | Tableau Public (unlimited for public dashboards) |

### Tableau Public vs Tableau Desktop

| Feature | Tableau Public (Free) | Tableau Desktop ($70/month) |
|---------|----------------------|------------------------------|
| Cost | Free | $840/year |
| Save locally | ❌ Cloud only | ✅ Yes |
| Share link | ✅ Public | ❌ Private only |
| Data size | 10 million rows | Unlimited |
| For this course | ✅ Perfect | ❌ Not needed |

---

## Installing Tableau Public

### Step-by-Step Installation

**Windows:**
1. Go to [public.tableau.com](https://public.tableau.com/en-us/s/download)
2. Click **"Download Tableau Public"** (blue button)
3. Run the `.exe` file
4. Click through installation defaults
5. Launch Tableau Public from Start Menu

**Mac:**
1. Go to [public.tableau.com](https://public.tableau.com/en-us/s/download)
2. Click **"Download Tableau Public"**
3. Open the `.dmg` file
4. Drag Tableau Public to Applications folder
5. Launch from Applications

### Create a Free Account

1. Open Tableau Public
2. Click **"Sign Up for Free"** (or "Create Account")
3. Enter your email and create a password
4. Verify your email (check inbox)
5. Log in to Tableau Public

**Save your login credentials** – you'll need them to publish dashboards.

---

## Tableau Interface Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  File  Data  Dashboard  Window  Help                    [Sign In] [Save]    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────────┐  ┌─────────────────────────────────────────────┐  │
│  │ DATA                 │  │  Canvas (where you build charts)            │  │
│  │ ┌─────────────────┐ │  │  ┌─────────────────────────────────────┐    │  │
│  │ │ Connections     │ │  │  │                                     │    │  │
│  │ │ └─ orders.csv   │ │  │  │                                     │    │  │
│  │ └─────────────────┘ │  │  │                                     │    │  │
│  │                     │  │  │                                     │    │  │
│  │ Dimensions (Blue)   │  │  │                                     │    │  │
│  │ ┌─────────────────┐ │  │  │                                     │    │  │
│  │ │ order_id        │ │  │  │                                     │    │  │
│  │ │ region          │ │  │  │                                     │    │  │
│  │ │ category        │ │  │  │                                     │    │  │
│  │ │ order_date      │ │  │  │                                     │    │  │
│  │ └─────────────────┘ │  │  │                                     │    │  │
│  │                     │  │  │                                     │    │  │
│  │ Measures (Green)    │  │  └─────────────────────────────────────┘    │  │
│  │ ┌─────────────────┐ │  │                                             │  │
│  │ │ sales           │ │  │  ┌─────────────────────────────────────┐    │  │
│  │ │ profit          │ │  │  │ Marks Card                          │    │  │
│  │ │ quantity        │ │  │  │ ┌─────┬─────┬─────┬─────┬─────────┐ │    │  │
│  │ └─────────────────┘ │  │  │ │Color│Size │Label│Tooltip│Detail │ │    │  │
│  └─────────────────────┘  │  │ └─────┴─────┴─────┴─────┴─────────┘ │    │  │
│                           │  └─────────────────────────────────────┘    │  │
│                           │                                             │  │
│  Pages │ Filters │ Marks  │  Columns: [region]    Rows: [SUM(profit)]   │  │
│  └─────────────────────┘  └─────────────────────────────────────────────┘  │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│  Sheets: [Sheet 1] [Sheet 2] [Dashboard 1]                        [＋]     │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Key Interface Elements

| Element | Location | Purpose |
|---------|----------|---------|
| **Data Pane** | Left sidebar | All your data fields |
| **Canvas** | Center | Where you build charts |
| **Columns Shelf** | Top of canvas | X-axis (horizontal) |
| **Rows Shelf** | Left of canvas | Y-axis (vertical) |
| **Marks Card** | Below Data Pane | Customize colors, sizes, labels |
| **Filters Card** | Left (below Marks) | Limit data shown |
| **Pages Card** | Left | Animate over time |
| **Sheet Tabs** | Bottom | Switch between sheets/dashboards |

---

## Connecting to Data

### Step 1: Connect to CSV

1. Open Tableau Public
2. On the left sidebar, click **"Connect to Data"** (or File → Open)
3. Click **"Text File"** (for CSV files)
4. Navigate to `cleaned_orders.csv` (from Week 2)
5. Click **"Open"**

### Step 2: Understand the Data Pane

After connecting, you'll see:

```
Data Pane
│
├── Dimensions (blue) ← Categorical / qualitative
│   ├── order_id
│   ├── region
│   ├── category
│   ├── customer_segment
│   └── order_date
│
└── Measures (green) ← Numeric / quantitative
    ├── sales
    ├── profit
    └── quantity
```

**Memory trick:**
- **Blue (Dimensions)** = "Bins" (categories like Region, Date)
- **Green (Measures)** = "Numbers" (Sales, Profit, Quantity)

### Step 3: Preview Your Data

- Hover over any field to see a preview
- Click the dropdown arrow on a field to see options:
  - Show quick filter
  - Change data type
  - Rename
  - Hide

---

## Understanding Dimensions vs Measures

### The Most Important Concept in Tableau

| | Dimension (Blue) | Measure (Green) |
|--|-----------------|-----------------|
| **What it is** | Categories, labels, groups | Numbers, values, metrics |
| **Examples** | Region, Category, Date | Sales, Profit, Quantity |
| **What Tableau does** | Splits data into buckets | Aggregates (SUM, AVG, COUNT) |
| **Where to put** | Columns, Rows, Color, Pages | Columns, Rows, Size, Label |

### Automatic Aggregation

When you drag a **Measure** to the canvas, Tableau automatically applies an aggregation:

| Measure Dragged | Default Aggregation |
|----------------|---------------------|
| sales | SUM(sales) |
| profit | SUM(profit) |
| quantity | SUM(quantity) |
| order_id | COUNT(order_id) |

**To change aggregation:** Right-click the field → Measure → Choose: Sum, Average, Median, Count, Min, Max

### Examples

| What you want | Drag this to... |
|---------------|-----------------|
| Total sales by region | region (Columns), sales (Rows) |
| Average profit by category | category (Columns), profit (Rows) → change to AVG |
| Count of orders by region | region (Columns), order_id (Rows) → changes to COUNT |

---

## Building Your First Chart (Bar Chart)

### Goal: Total Sales by Region

**Step-by-step:**

1. **Drag `region` to Columns** (blue pill appears on top shelf)
   - This creates categories along the bottom (horizontal axis)

2. **Drag `sales` to Rows** (green pill appears on left shelf)
   - Tableau automatically shows SUM(sales) as bars going up

3. **You have a bar chart!**

```
    Columns: [region]
    Rows: [SUM(sales)]
    
    ┌─────────────────────────────────────────┐
    │  SUM(sales)                             │
    │     ▲                                    │
    │  $500│    ┌───┐                         │
    │  $400│    │   │    ┌───┐                │
    │  $300│    │   │    │   │    ┌───┐       │
    │  $200│    │   │    │   │    │   │       │
    │  $100│    │   │    │   │    │   │  ┌───┐│
    │    $0└────┴───┴────┴───┴────┴───┴────┴───┴┘
    │           East  North  South  West        │
    └─────────────────────────────────────────┘
```

### Customizing Your Bar Chart

**Sort bars descending:**
- Hover over the axis (the bar values)
- Click the **sort icon** (AZ↓ or ↑)
- Choose "Descending"

**Add labels on bars:**
- Drag `sales` to **Labels** on the Marks card
- Numbers appear on top of each bar

**Change bar colors:**
- Click **Color** on Marks card
- Choose a different palette
- For profit: use green (positive) / red (negative)

**Add a title:**
- Double-click "Sheet 1" at bottom
- Rename to "Sales by Region"

### Alternative: Horizontal Bar Chart

- Drag `region` to Rows (instead of Columns)
- Drag `sales` to Columns (instead of Rows)

---

## Building a Line Chart

### Goal: Profit Over Time

**Step-by-step:**

1. **Drag `order_date` to Columns**

2. **Right-click on `order_date`** → Choose **"Month"** (or "Day", "Week", "Quarter")
   - This changes granularity of the date

3. **Drag `profit` to Rows**

4. **You have a line chart!**

```
    Columns: [order_date (Month)]
    Rows: [SUM(profit)]
    
    ┌─────────────────────────────────────────┐
    │  SUM(profit)                            │
    │     ▲                                    │
    │  $80│        *                           │
    │  $60│      *   *                         │
    │  $40│    *       *                       │
    │  $20│  *           *                     │
    │   $0└──*─────────────*──────────────────→│
    │        Jan    Feb    Mar    Apr    May   │
    └─────────────────────────────────────────┘
```

### Customizing Line Chart

**Add multiple lines (by region):**
- Drag `region` to **Color** on Marks card
- One line per region appears

**Add labels on last point:**
- Drag `profit` to Labels
- Click Label → Marks to label → "Line Ends"

**Change to area chart:**
- On Marks card, change drop-down from "Automatic" to "Area"

**Add a trend line:**
- Right-click on the chart → **Trend Lines** → **Show Trend Lines**

---

## Building a Scatter Plot

### Goal: Sales vs Profit (by Category)

**Step-by-step:**

1. **Drag `sales` to Columns**

2. **Drag `profit` to Rows**

3. **Drag `category` to Color** (on Marks card)

4. **You have a scatter plot!**

```
    Columns: [SUM(sales)]
    Rows: [SUM(profit)]
    
    ┌─────────────────────────────────────────┐
    │  SUM(profit)                            │
    │     ▲                                    │
    │  $100│       ● (Electronics)             │
    │   $80│     ●                             │
    │   $60│   ●                               │
    │   $40│ ● (Furniture)                     │
    │   $20│●                                  │
    │    $0└─────┬─────┬─────┬─────┬─────┬────→│
    │          $100  $200  $300  $400  $500    │
    │                 SUM(sales)               │
    └─────────────────────────────────────────┘
```

### Customizing Scatter Plot

**Adjust dot size (by quantity):**
- Drag `quantity` to **Size** on Marks card
- Larger dots = more quantity

**Add a reference line:**
- Right-click on axis → **Add Reference Line**
- Choose "Constant" → Value 0

**Add trend line:**
- Right-click on chart → **Trend Lines** → **Show Trend Lines**

**Filter outliers:**
- Drag `sales` to Filters
- Set range (e.g., 0 to 1000)

---

## Building a Geographic Map

### Goal: Profit by Region on a Map

**Step-by-step:**

1. **Double-click `region`** (Tableau tries to map it)

2. **If map doesn't appear:** Assign geographic role
   - Right-click `region` → **Geographic Role** → **State/Province** (US) or **Country/Region**

3. **Drag `profit` to Color** on Marks card

4. **You have a filled map!**

```
    ┌─────────────────────────────────────────┐
    │                                         │
    │      ┌─────┐                            │
    │      │North│ (Green = high profit)      │
    │      └─────┘                            │
    │                                         │
    │  ┌─────┐                                │
    │  │West │  ┌─────┐                       │
    │  └─────┘  │East │                       │
    │           └─────┘                       │
    │      ┌─────┐                            │
    │      │South│ (Red = loss)               │
    │      └─────┘                            │
    │                                         │
    └─────────────────────────────────────────┘
```

### Customizing Maps

**Change map style:**
- Map → Map Layers → Style: Normal, Dark, Light, Satellite

**Add labels:**
- Drag `region` to Label on Marks card

**Change color scheme:**
- Click Color → Edit Colors → Choose diverging palette (Red-Blue)

**Add a symbol map (dots instead of filled areas):**
- Change mark type from "Automatic" to "Circle"

---

## Creating Calculated Fields

### What is a Calculated Field?

A new column you create using a formula. Example: Profit Margin = Profit / Sales

### Step-by-Step: Profit Margin

1. **Right-click anywhere in the Data Pane** (left sidebar)

2. Click **"Create Calculated Field"**

```
┌─────────────────────────────────────────────────┐
│  Calculated Field                               │
│  ┌─────────────────────────────────────────────┐│
│  │ Name: Profit Margin                         ││
│  └─────────────────────────────────────────────┘│
│  ┌─────────────────────────────────────────────┐│
│  │ Formula:                                    ││
│  │ ┌─────────────────────────────────────────┐ ││
│  │ │ SUM(profit) / SUM(sales)                │ ││
│  │ └─────────────────────────────────────────┘ ││
│  └─────────────────────────────────────────────┘│
│                                                 │
│  [OK] [Cancel]                                  │
└─────────────────────────────────────────────────┘
```

3. **Enter Name:** `Profit Margin`

4. **Enter Formula:** `SUM(profit) / SUM(sales)`

5. Click **OK**

6. The new field appears in Measures (green)

### Common Calculated Fields

| What You Want | Formula |
|---------------|---------|
| Profit Margin | `SUM(profit) / SUM(sales)` |
| Sales per Order | `SUM(sales) / COUNTD(order_id)` |
| Discount (if you have list price) | `(SUM(list_price) - SUM(sales)) / SUM(list_price)` |
| High Value Order (flag) | `IF SUM(sales) > 500 THEN "High" ELSE "Regular" END` |
| Year from Date | `YEAR([order_date])` |
| Month Name | `DATENAME('month', [order_date])` |

### Formula Helpers

While typing formulas, Tableau suggests:
- **Functions** (SUM, AVG, IF, YEAR, etc.)
- **Fields** (sales, profit, region, etc.)
- **Parameters** (if you created any)

---

## Adding Filters

### What is a Filter?

A filter limits which data appears in your chart/dashboard.

### Step-by-Step: Add Region Filter

1. **Drag `region` from Data Pane to Filters card** (left side)

2. **Choose how you want to filter:**
   - General (select specific regions)
   - Wildcard (text contains)
   - Condition (based on a measure)
   - Top (top 10 by sales)

3. **Select regions:** Check "North", "South", "East", "West"

4. Click **OK**

5. **To show the filter on the view:**
   - Right-click on `region` in Filters card
   - Click **"Show Filter"**

### Filter Appears as:

```
┌─────────────────┐
│  Region         │
│  ┌───────────┐  │
│  │ ☑ North   │  │
│  │ ☑ South   │  │
│  │ ☑ East    │  │
│  │ ☑ West    │  │
│  └───────────┘  │
└─────────────────┘
```

### Types of Filters

| Filter Type | When to Use | Example |
|-------------|-------------|---------|
| Single value dropdown | One selection at a time | Region = North |
| Multiple value (checkbox) | Select many | Regions = North, East |
| Slider (range) | Numeric range | Sales between $0-$1000 |
| Date picker | Date range | Order Date after Jan 1 |
| Quick filter (automatic) | Quick exploration | All of the above |

### Changing Filter Type

1. Click dropdown arrow on filter
2. **Customize** → **Filter Type**
3. Choose: Single Value (dropdown), Multiple Values (checkbox), Slider, etc.

---

## Building a Dashboard

### What is a Dashboard?

A dashboard is a **collection of sheets** (charts) arranged on one page.

### Step-by-Step: Create Dashboard

1. **Create your sheets first** (bar chart, line chart, map, etc.)

2. **Click "New Dashboard"** at the bottom (next to sheet tabs)

```
Sheet Tabs: [Sales by Region] [Profit Trend] [Profit Map] [Dashboard 1]  [＋]
```

3. **Drag sheets from left pane onto the dashboard**

```
Left Pane:
┌─────────────────┐
│  Sheets         │
│  ┌─────────────┐│
│  │Sales by Reg ││
│  │Profit Trend ││
│  │Profit Map   ││
│  └─────────────┘│
└─────────────────┘
```

### Dashboard Layout Tips

**Good dashboard layout:**
```
┌─────────────────────────────────────────┐
│  Title: Sales Dashboard - Q1 2024       │
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
│  Line Chart: │  Map:                    │
│  Trend       │  Profit by Region        │
│              │                          │
└──────────────┴──────────────────────────┘
```

### Dashboard Layout Options

**Tiled vs Floating**

| Mode | What It Does | When to Use |
|------|--------------|-------------|
| **Tiled** | Sheets snap into grid | Most dashboards (easier) |
| **Floating** | Sheets can overlap | Custom layouts, annotations |

**Switch mode:** Dashboard → Format → Tiled/Floating

### Resizing Sheets

1. Click on a sheet in the dashboard
2. Drag edges to resize
3. Sheets automatically rearrange

### Adding Text and Images

1. From left pane, click **"Objects"**
2. Drag **"Text"** onto dashboard
3. Type your title or annotation
4. Drag **"Image"** to add a logo

---

## Adding Dashboard Actions (Interactivity)

### What is an Action?

An action makes dashboards interactive. Example: Click a bar → filter other charts.

### Step-by-Step: Filter Action

1. **Dashboard** → **Actions** (top menu)

2. **Add Action** → **Filter**

```
┌─────────────────────────────────────────────────┐
│  Add Filter Action                              │
│  ┌─────────────────────────────────────────────┐│
│  │ Name: Filter by Region                      ││
│  └─────────────────────────────────────────────┘│
│                                                 │
│  Source Sheet: Sales by Region                  │
│                                                 │
│  Target Sheets: Profit Trend, Profit Map        │
│                                                 │
│  Run action on: [Select]                        │
│                                                 │
│  [OK] [Cancel]                                  │
└─────────────────────────────────────────────────┘
```

3. **Name:** `Filter by Region`

4. **Source Sheet:** The sheet you click on (e.g., "Sales by Region")

5. **Target Sheets:** Sheets that should update (check all others)

6. **Run action on:** `Select` (click on a bar)

7. Click **OK**

### Testing the Action

1. Click on "North" bar in your bar chart
2. Other charts (line chart, map) should now show ONLY North data
3. Click anywhere outside to clear the filter

### Other Action Types

| Action Type | What It Does | Example |
|-------------|--------------|---------|
| **Filter** | Filter target sheets | Click region → show that region only |
| **Highlight** | Highlight matching marks | Hover over region → highlight dots on scatter plot |
| **URL** | Open a web page | Click order ID → open order details page |

### URL Action Example

1. Dashboard → Actions → Add Action → URL
2. Name: `Open Google`
3. URL: `https://www.google.com`
4. When user clicks, Google opens in new tab

---

## Publishing to Tableau Public

### Step-by-Step: Publish Dashboard

1. **Sign in** to Tableau Public (top right)

2. **File** → **Save to Tableau Public As...**

```
┌─────────────────────────────────────────────────┐
│  Save to Tableau Public                         │
│  ┌─────────────────────────────────────────────┐│
│  │ Name: My Sales Dashboard                    ││
│  └─────────────────────────────────────────────┘│
│                                                 │
│  [Save] [Cancel]                                │
└─────────────────────────────────────────────────┘
```

3. **Name your workbook** (e.g., "Sales Analysis Dashboard")

4. Click **Save**

5. **Wait for upload** (progress bar appears)

6. **Copy the share URL** (appears in browser)

### Your Dashboard is Now Live!

URL will look like:
```
https://public.tableau.com/views/SalesAnalysisDashboard/Dashboard1
```

**Share this link with anyone** – they don't need Tableau to view it.

### Viewing Your Published Dashboard

1. Open incognito/private browser window
2. Paste the URL
3. Verify all filters and actions work

### Updating a Published Dashboard

1. Make changes in Tableau Desktop/Public
2. **File** → **Save to Tableau Public As...**
3. Use the SAME name
4. Click "Overwrite" when prompted

---

## Common Issues & Fixes

### Issue #1: "Can't connect to CSV" / File not found

**Fix:**
- Save CSV to Desktop (Tableau Public can be picky about file paths)
- Close Excel if the file is open there
- Reconnect: Data → Replace Data Source

### Issue #2: Map shows "Unknown" for regions

**Fix:**
- Tableau doesn't know "North" as a location
- Option A: Use actual city/state names
- Option B: Change to symbol map (not filled map)
- Option C: Assign geographic role as "State/Province"

### Issue #3: Filter doesn't affect all charts

**Fix:**
1. Click the filter dropdown arrow
2. **Apply to Worksheets** → **Selected Worksheets**
3. Check which sheets should update
4. Click OK

### Issue #4: Dashboard is slow to load

**Fix:**
- Reduce data: Filter to last 3 months only
- Create an extract: Data → Extract (saves locally)
- Reduce number of marks: Filter to top 1000 rows

### Issue #5: Can't save dashboard locally

**Fix:**
- Tableau Public saves to cloud ONLY
- Use **"Save to Tableau Public As..."** not "Save As"
- No local save option in free version

### Issue #6: Date shows as "Year" only (can't drill down)

**Fix:**
- Right-click on date field
- Choose "Month" or "Day"
- Or click the + icon on the date pill to drill down

### Issue #7: Aggregation is wrong (SUM vs AVG)

**Fix:**
- Right-click on the measure (green pill)
- **Measure** → Choose: Sum, Average, Count, Median, etc.

### Issue #8: Labels overlap on bar chart

**Fix:**
- Click Label on Marks card
- Click the "..." button
- Under "Marks to Label", choose "Show marks at label position"
- Or change label font size

---

## Keyboard Shortcuts

| Action | Windows | Mac |
|--------|---------|-----|
| New sheet | Ctrl + M | Cmd + M |
| New dashboard | Ctrl + Shift + D | Cmd + Shift + D |
| Undo | Ctrl + Z | Cmd + Z |
| Redo | Ctrl + Y | Cmd + Shift + Z |
| Save to Tableau Public | Ctrl + S | Cmd + S |
| Swap rows and columns | Ctrl + W | Cmd + W |
| Show/Hide Data Pane | Ctrl + 1 | Cmd + 1 |
| Show/Hide Filters Card | Ctrl + 2 | Cmd + 2 |
| Show/Hide Marks Card | Ctrl + 3 | Cmd + 3 |
| Show/Hide Pages Card | Ctrl + 4 | Cmd + 4 |
| Zoom in | Ctrl + = | Cmd + = |
| Zoom out | Ctrl + - | Cmd + - |
| Fit to width | Ctrl + Shift + F | Cmd + Shift + F |
| Fit to height | Ctrl + Shift + H | Cmd + Shift + H |

---

## Practice Exercises

### Beginner Exercise 1: Basic Bar Chart

**Goal:** Create a bar chart showing total profit by category

**Steps:**
1. Connect to `cleaned_orders.csv`
2. Drag `category` to Columns
3. Drag `profit` to Rows
4. Sort descending
5. Add labels (drag profit to Labels)
6. Rename sheet "Profit by Category"

---

### Beginner Exercise 2: Line Chart with Trend

**Goal:** Create a line chart of daily profit with 7-day rolling average

**Steps:**
1. Drag `order_date` to Columns → right-click → Day
2. Drag `profit` to Rows
3. Add trend line: Right-click → Trend Lines → Show Trend Lines
4. Rename sheet "Profit Trend"

---

### Intermediate Exercise 3: Scatter Plot Matrix

**Goal:** Create scatter plots for sales vs profit, colored by region

**Steps:**
1. Drag `sales` to Columns
2. Drag `profit` to Rows
3. Drag `region` to Color
4. Drag `quantity` to Size
5. Add reference lines at x=0 and y=0
6. Rename sheet "Sales vs Profit"

---

### Intermediate Exercise 4: Two-Page Dashboard

**Goal:** Build a dashboard with Executive Summary and Deep Dive pages

**Page 1: Executive Summary**
- KPI: Total Sales (calculated field)
- KPI: Total Profit
- Bar chart: Profit by Region
- Bar chart: Sales by Category
- Date range filter (affects all)

**Page 2: Deep Dive**
- Line chart: Profit over time (by category)
- Scatter plot: Sales vs Profit (by region)
- Region filter (dropdown)
- Dashboard action: Click bar on Page 1 → filter Page 2

**Steps:**
1. Create all sheets first
2. New Dashboard → Page 1
3. Add sheets, arrange layout
4. Add filters (drag to dashboard)
5. New Dashboard → Page 2
6. Add remaining sheets
7. Dashboard → Actions → Add Action → Filter
8. Test interactivity

---

### Challenge Exercise: Parameter Switching

**Goal:** Allow user to toggle between SUM(profit) and AVG(profit) in a bar chart

**Steps:**
1. Create parameter: Right-click in Data Pane → Create Parameter
   - Name: `Profit Aggregation`
   - Data type: String
   - Allowable values: List
   - Values: `Total Profit`, `Average Profit`

2. Create calculated field:
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

4. Show parameter control:
   - Right-click parameter → Show Parameter Control

5. User can now toggle between total and average profit

---

## Next Steps

After completing this guide, you should be able to:

- [ ] Connect Tableau to CSV files
- [ ] Create bar charts, line charts, scatter plots, and maps
- [ ] Build calculated fields
- [ ] Add filters and dashboard actions
- [ ] Publish interactive dashboards to Tableau Public

**Ready for more?**
- Complete the Week 3 exercises in your course repo
- Practice with the `superstore_sample.csv` dataset
- Apply these skills to the Week 4 capstone project

---

**End of Tableau Guide**

*Bookmark this guide – you'll reference it throughout Week 3 and Week 4.*

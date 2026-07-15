# Lab 08 - Explore Power BI

Power BI has its own section of the outline: capabilities, data models, and choosing visualizations. Building one small report covers all three.

## Time Needed

25-30 minutes.

## What You Will Learn

- The Desktop-to-service workflow
- How a small data model with a measure works
- Which visual fits which question
- What publishing and dashboards add

## DP-900 Concepts Covered

| Concept              | Where you see it in the lab                    |
| -------------------- | ---------------------------------------------- |
| Power BI Desktop     | You model data and build a report              |
| Semantic model       | You load a table and add a measure             |
| Visualization choice | You compare bar, line, pie, and card visuals   |
| Power BI service     | You publish and view in the browser (optional) |

## Cost Warning

Power BI Desktop is free (Windows only). Publishing to the Power BI service needs a work or school account; a free license is enough for a personal workspace. Nothing bills your Azure subscription.

## Steps

### 1. Install Power BI Desktop

1. Install from the Microsoft Store (search "Power BI Desktop") or from powerbi.microsoft.com/desktop.
2. Open it and skip the sign-in for now (sign-in is only needed to publish).

If you cannot install it (no Windows machine), use the Fabric workspace from Lab 07 and create the report in the browser with the same data.

### 2. Create sample data

1. Create a file named `monthly-sales.csv`:

```text
Month,Region,Sales
Jan,West,120
Jan,East,90
Feb,West,140
Feb,East,110
Mar,West,160
Mar,East,95
```

2. In Power BI Desktop, select **Get data > Text/CSV** and load the file.

### 3. Add a measure to the model

1. Open the **Data** (table) view and look at the loaded table: this is your semantic model.
2. Select **New measure** and enter:

```text
Total Sales = SUM('monthly-sales'[Sales])
```

A measure is a calculation, not a stored column. This is the DAX the study notes mention.

### 4. Try the visuals

Build each of these on the report canvas and ask which question it answers best:

| Visual       | Fields                 | Question it answers |
| ------------ | ---------------------- | ------------------- |
| Column chart | Region and Total Sales | Compare categories  |
| Line chart   | Month and Total Sales  | Trend over time     |
| Pie chart    | Region and Total Sales | Part-to-whole       |
| Card         | Total Sales            | One headline number |

Click a column in the column chart and watch the other visuals filter: visuals on a report page interact.

### 5. Publish (optional)

1. Sign in with a work or school account and select **Publish**.
2. Open app.powerbi.com, find the report, and view it in the browser.
3. Hover a visual and select the pin icon to pin it to a new **dashboard**. Note the dashboard exists only in the service, never in Desktop.

## Clean Up

Delete the report and dashboard from your Power BI workspace if you published. Local files can simply be deleted.

## Success Criteria

You are done when you can explain:

- What Power BI Desktop does vs the Power BI service
- What a measure is and where it lives
- Which visual you would pick for a trend, a comparison, a proportion, and a single number
- How a dashboard differs from the report you built

# Lab 05 - Explore a Model-Driven App

Build a model-driven app over the same Equipment Loan table and compare it with the canvas app from Lab 04. Same data, opposite philosophy: the UI is generated from the data model.

## Time Needed

20-25 minutes.

## What You Will Learn

- How a model-driven app is created from Dataverse tables
- How forms and views become the app UI automatically
- What the sitemap (navigation) is
- When to choose model-driven over canvas

## PL-900 Concepts Covered

| Concept           | Where you see it in the lab                                   |
| ----------------- | ------------------------------------------------------------- |
| Model-driven app  | You generate an app from the data model                       |
| Forms and views   | The same forms and views from Lab 03 appear as the app's UI   |
| Sitemap           | You edit the app navigation                                   |
| Data-first design | You see why layout control is limited but consistency is high |

## Steps

### 1. Create the app

1. In the maker portal, select **Apps** > **New app** > **Model-driven**.
2. Name it `Loan Management`.
3. In the app designer, add a page: choose **Dataverse table** and pick **Equipment Loan** (add Contact too if offered).

### 2. Look at what was generated

1. Preview (play) the app.
2. Notice without any design work you have: a left navigation, a view (grid) of loans, a working main form when you open a row, search, and sorting.
3. Open a loan, edit it, and save.

### 3. Trace the UI back to the data model

| App element you see | Where it came from                |
| ------------------- | --------------------------------- |
| The grid of loans   | The table's default view (Lab 03) |
| The edit screen     | The table's main form (Lab 03)    |
| The Status dropdown | The choice column you created     |
| The Borrower field  | The lookup to Contact             |

### 4. Edit the sitemap

1. Back in the designer, rename the navigation group to "Loans".
2. Notice you arrange navigation and pick tables/pages, but you do not place individual pixels. That is the model-driven trade-off.

### 5. Compare with Lab 04

| Question                          | Canvas app (Lab 04) | Model-driven app (this lab)      |
| --------------------------------- | ------------------- | -------------------------------- |
| Who designed each screen?         | You did             | The platform generated it        |
| Change a header color?            | One click           | Not a per-screen design decision |
| Add related tables and processes? | Manual work         | Natural fit                      |

## Clean Up

Keep the app; Lab 09 removes everything.

## Success Criteria

You are done when you can explain:

- How the app UI was generated from forms and views
- What the sitemap controls
- Why model-driven apps require Dataverse
- A scenario where model-driven beats canvas, and the reverse

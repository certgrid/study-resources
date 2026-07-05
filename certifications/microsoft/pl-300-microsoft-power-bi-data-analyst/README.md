# PL-300: Microsoft Power BI Data Analyst - Study Cheatsheet

The PL-300: Microsoft Power BI Data Analyst exam validates your ability to prepare and model data, then visualize, analyze, deploy, and maintain Power BI assets. It is aimed at data analysts and BI professionals who clean and transform data in Power Query, build models with DAX, design reports, and manage content in the Power BI service. The exam is 120 minutes, has roughly 40-60 questions, and you need a scaled score of 700 (out of 1000) to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | PL-300 |
| Credential | PL-300: Microsoft Power BI Data Analyst |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Prepare the Data | ~27% |
| 2 | Model the Data | ~25% |
| 3 | Visualize and Analyze the Data | ~25% |
| 4 | Deploy and Maintain Assets | ~23% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Prepare the Data

- Query folding pushes Power Query transformations (filters, column selection, joins) back to the source as native SQL; folding happens with relational sources like SQL Server but breaks at steps using custom M functions or unsupported logic, after which everything runs locally in memory.
- Right-click a step and choose View Native Query to confirm whether that step (and the steps before it) folds; if the option is greyed out, folding has stopped.
- Adding a custom column with a complex M expression or a custom function breaks folding at that step and for all subsequent steps, forcing Power Query to pull all rows into memory.
- Unpivot Columns converts wide crosstab data (e.g., separate Jan/Feb/Mar columns) into a normalized two-column attribute/value shape; Pivot Columns does the reverse.
- Split Column by Delimiter divides one column into several using a chosen separator (e.g., a hyphen in '2024-Q1' yields Year and Quarter columns).
- Append Queries stacks rows from tables with the same schema (like SQL UNION); Merge Queries joins tables on matching key columns (like SQL JOIN).

### Domain 2 - Model the Data

- A star schema centers a fact table surrounded by dimension tables joined directly to it; it is the recommended Power BI design because it minimizes joins, improves performance, and simplifies DAX.
- Relationships default to one-to-many, filtering from the one (dimension) side to the many (fact) side with single-direction cross-filtering.
- Only one relationship between two tables can be active at a time; create a second as inactive and activate it inside a measure with USERELATIONSHIP (e.g., to support both OrderDate and ShipDate against the Date table).
- Measures are evaluated at query time against the current filter context and are not stored; calculated columns are computed row by row at refresh and persisted in the model.
- Calculated columns can be used as slicers, filters, and visual axes; measures generally cannot serve as an axis or slicer field.
- A valid date table must contain a contiguous range of dates with no gaps and a column of Date or DateTime type, and should be marked as a date table to enable time intelligence.

### Domain 3 - Visualize and Analyze the Data

- Edit interactions to set a visual's effect on others to None, Filter (default cross-filter for most visuals), or Highlight (default for charts) to control how clicking one visual affects the rest of the page.
- Drillthrough lets users right-click a data point and jump to a destination page automatically filtered to that point's context; configure it by adding the field to the Drillthrough well on the target page.
- The Q&A visual lets report consumers type natural-language questions on the canvas and returns an auto-generated visual answer from the model.
- The Analyze feature (Explain the increase/decrease) uses AI to identify factors that contributed to a change in a data point on supported visuals.
- The Decomposition Tree visual lets users interactively drill into a measure across multiple dimensions and can use AI to find the highest or lowest contributing category at each level.
- The Key Influencers visual identifies which factors most affect a chosen metric or outcome.

### Domain 4 - Deploy and Maintain Assets

- Scheduled refresh applies to Import-mode datasets stored in the service; DirectQuery datasets query the live source on each interaction and do not need scheduled data refresh (though they may refresh tiles/metadata).
- Power BI Pro allows up to 8 scheduled refreshes per day per dataset; Premium and Premium Per User allow up to 48 per day.
- An on-premises data gateway (standard/enterprise mode) is required for scheduled refresh against on-premises sources; install one gateway and add a data source configuration for each source it serves; personal mode is single-user only.
- Incremental refresh loads only new or changed data using RangeStart and RangeEnd parameters defined in Power Query, greatly reducing refresh time for large, mostly historical tables.
- Use the Power BI REST API (e.g., the Refreshes endpoint) to trigger dataset refreshes programmatically on demand, outside the built-in scheduler.
- Distribute content without edit rights by sharing a report with view permission or by publishing an app from a workspace; apps can define audience groups with different content permissions.

## Study tips

- Watch for query folding in scenario questions: any answer adding a custom M function or unsupported transform breaks folding for that and all later steps, so prefer source-native operations (filter, select columns, native SQL) when performance is the goal.
- Master the relationship and DAX context distinctions - active vs inactive relationships with USERELATIONSHIP, single vs bidirectional cross-filter, and measures (query-time, filter context) vs calculated columns (refresh-time, row context).
- Memorize the refresh limits: 8 refreshes/day on Pro, 48/day on Premium/PPU, and that an on-premises gateway is mandatory for on-premises sources while DirectQuery needs no scheduled data refresh.
- Know which feature solves which interaction need: Drillthrough for right-click-to-detail, Edit interactions/None to stop cross-filtering, Sync Slicers for cross-page slicers, Bookmarks for saved state, and Q&A/Analyze/Decomposition Tree/Key Influencers for AI exploration.
- Distinguish the distribution and governance options: report sharing vs apps vs deployment pipelines, shared datasets/live connections for one source of truth, Purview sensitivity labels (inherited downstream), and Entra ID B2B for external guests.

---

Want the full breakdown? See the complete **[PL-300 study guide](https://certgrid.app/study-guide/pl-300-microsoft-power-bi-data-analyst)** and **[free practice questions](https://certgrid.app/practice/pl-300-microsoft-power-bi-data-analyst)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


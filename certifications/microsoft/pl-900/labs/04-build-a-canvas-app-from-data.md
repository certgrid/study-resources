# Lab 04 - Build a Canvas App from Data

Build your first canvas app on top of the Equipment Loan table from Lab 03. You will see why "start from data" is the fastest way to a working three-screen app.

## Time Needed

25-30 minutes.

## What You Will Learn

- How to generate a canvas app from a Dataverse table
- What screens, galleries, forms, and controls are
- Where Power Fx formulas live
- How to test and save an app

## PL-900 Concepts Covered

| Concept             | Where you see it in the lab                              |
| ------------------- | -------------------------------------------------------- |
| Canvas app          | You build a design-first app from data                   |
| Galleries and forms | The generated app uses a browse gallery and an edit form |
| Power Fx            | You read and tweak a formula                             |
| Data source         | The app connects to your Dataverse table                 |

## Steps

### 1. Generate the app

1. In the maker portal, select **Apps** > **New app**, and choose to start with data (or from the Equipment Loan table hub, choose to create an app).
2. Pick the **Equipment Loan** table.
3. Power Apps generates a working app: a browse screen, a detail screen, and an edit screen.

### 2. Run the app

1. Select **Play** (preview).
2. Browse your sample rows, open one, edit it, and save.
3. Add a new loan from inside the app and confirm it appears in Dataverse.

### 3. Read one Power Fx formula

1. Select the browse gallery, then look at the `Items` property in the formula bar.
2. Notice it is a formula (search and sort over the table), similar to an Excel expression.
3. Select a button or icon and look at its `OnSelect` property: that is Power Fx driving navigation.

### 4. Make one visual change

1. Change the screen header text to "Equipment Loans".
2. Change the fill color of the header.
3. This is the canvas value: total layout control.

### 5. Optional: try Copilot

Ask Copilot inside the studio to make a change, for example "add a label showing the number of loans". Review what it edits.

### 6. Save the app

Save it as `Equipment Loans App`. Note that sharing with other users is not the point of a single-user developer environment; in a real tenant you would share the app with security groups.

## Clean Up

Keep the app for now; Lab 09 removes everything.

## Success Criteria

You are done when you can explain:

- How a canvas app is generated from a table
- What the gallery (browse) vs form (edit) controls do
- Where Power Fx appears in a canvas app
- Why canvas apps are called design-first

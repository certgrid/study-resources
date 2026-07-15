# Lab 03 - Create a Dataverse Table

Now build your own table, two ways: manually, and by describing it to Copilot. The table you create here (Equipment Loan) powers the canvas app and flow labs that follow.

## Time Needed

20-25 minutes.

## What You Will Learn

- How to create a custom table and columns
- How choice and lookup columns work
- How Copilot can create or edit a table from a description
- How data entry looks immediately after table creation

## PL-900 Concepts Covered

| Concept                | Where you see it in the lab                    |
| ---------------------- | ---------------------------------------------- |
| Custom table           | You create the Equipment Loan table            |
| Columns and data types | You add text, date, and choice columns         |
| Relationships          | You add a lookup to Contact                    |
| AI to create tables    | You use Copilot to draft or edit the structure |

## Steps

### 1. Create the table with Copilot (option A)

1. In the maker portal **Home**, find the Copilot prompt box.
2. Enter a description like:

```text
Create a table to track equipment loans with the equipment name,
the borrower, the loan date, the due date, and a status of
Requested, Checked Out, or Returned.
```

3. Review what Copilot proposes: table name, columns, and data types.
4. Adjust anything that looks wrong (for example, rename a column), then create it.

### 2. Or create the table manually (option B)

1. Select **Tables** > **New table**.
2. Name it `Equipment Loan`.
3. Add columns:

| Column         | Data type                                  |
| -------------- | ------------------------------------------ |
| Equipment Name | Text (you can use the primary name column) |
| Loan Date      | Date only                                  |
| Due Date       | Date only                                  |
| Status         | Choice: Requested, Checked Out, Returned   |
| Borrower       | Lookup to Contact                          |

### 3. Inspect what you got for free

Open the new table hub and confirm Dataverse auto-created:

- A main form for editing one loan
- A default view listing loans
- System columns such as Created On and Owner

### 4. Enter sample data

Add 3-4 rows with different statuses and dates. You will reuse them in Labs 04, 06, and 07.

### 5. Try an AI edit

Ask Copilot (or use the table designer) to "add a Notes column to the Equipment Loan table" and confirm the column appears.

## Clean Up

Keep the table and its rows; Labs 04-07 depend on them. You will remove everything in Lab 09.

## Success Criteria

You are done when you can explain:

- The steps to create a custom table and columns
- What a choice column and a lookup column each do
- What Dataverse creates automatically alongside a new table
- How Copilot creates or edits tables from natural language

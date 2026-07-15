# Lab 02 - Explore a Dataverse Table

Dataverse ships with standard tables. Exploring one (Contact) is the fastest way to make tables, columns, relationships, forms, and views real before you create your own.

## Time Needed

15-20 minutes.

## What You Will Learn

- How a Dataverse table is structured
- What columns and data types look like
- Where relationships between tables are defined
- The difference between forms and views, seen live

## PL-900 Concepts Covered

| Concept       | Where you see it in the lab                     |
| ------------- | ----------------------------------------------- |
| Table         | You open the standard Contact table             |
| Columns       | You browse column names and data types          |
| Relationships | You see how Contact relates to Account          |
| Forms         | You open the main form used to edit one contact |
| Views         | You open a view that lists many contacts        |

## Steps

### 1. Open the Contact table

1. In the maker portal, select **Tables**.
2. Under the standard tables, open **Contact**.
3. Read the table hub page: columns, relationships, forms, views are all listed as components.

### 2. Browse columns

1. Open **Columns**.
2. Find examples of different data types:

| Column example | Data type to notice          |
| -------------- | ---------------------------- |
| First Name     | Text                         |
| Email          | Email (formatted text)       |
| Birthday       | Date                         |
| Company Name   | Lookup (relationship column) |

### 3. Browse relationships

1. Open **Relationships**.
2. Find a many-to-one relationship from Contact to Account.
3. Note the pattern: the lookup column on the "many" side points to the "one" side.

### 4. Open a form

1. Open **Forms**.
2. Open the main form named "Contact" (read-only is fine).
3. Notice it is a layout for editing ONE record: fields arranged in sections and tabs.

### 5. Open a view

1. Go back and open **Views**.
2. Open a view such as "Active Contacts".
3. Notice it is a filtered, sorted list of MANY records with chosen columns.

### 6. Add a row of data

1. From the table hub, choose to edit data.
2. Add one test contact (for example, first name "Test", last name "Contact").
3. See the row appear in the view.

## Clean Up

Delete the test contact row if you want the table pristine, or keep it for the next labs.

## Success Criteria

You are done when you can explain:

- What a table, column, and row are in Dataverse
- How a lookup column expresses a many-to-one relationship
- The difference between a form and a view
- Why standard tables like Contact save build time

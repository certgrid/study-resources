# Lab 05 - Configure a Budget and Cost Alert

This is one of the most important beginner Azure labs. It helps reduce fear around unexpected cloud spend.

## Time Needed

15-20 minutes.

## What You Will Learn

- Where Azure costs are tracked
- How budgets help monitor spend
- How alerts notify you before costs get out of hand
- Why Cost Management is different from the Pricing Calculator

## AZ-900 Concepts Covered

| Concept         | Where you see it in the lab           |
| --------------- | ------------------------------------- |
| Cost Management | You open actual spend tracking        |
| Budgets         | You create a spend threshold          |
| Alerts          | You configure notification thresholds |
| Governance      | You learn a basic cost-control habit  |

## Steps

### 1. Open Cost Management

1. Go to the Azure portal.
2. Search for **Cost Management + Billing**.
3. Open your subscription scope if prompted.

### 2. Open Budgets

Find **Budgets** under Cost Management.

### 3. Create a budget

Create a small learning budget appropriate for your account.

Use:

- Name: `az900-learning-budget`
- Reset period: Monthly
- Start date: Today
- Expiration: A future date

Choose a budget amount you are comfortable with. Do not copy someone else’s amount blindly.

### 4. Configure alerts

Create alerts such as:

| Threshold | Purpose        |
| --------- | -------------- |
| 50%       | Early warning  |
| 80%       | Strong warning |
| 100%      | Budget reached |

Add your email address for notifications.

### 5. Save the budget

Save and confirm the budget appears in the portal.

## Clean Up

Keep the budget. It is useful while learning.

## Success Criteria

You are done when you can explain:

- What a budget does
- Why a budget is not the same as a hard spending block
- Where actual Azure spend is reviewed
- How Cost Management differs from the Pricing Calculator


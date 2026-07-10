# Lab 06 - Apply Tags to Azure Resources

Tags are simple, but they are heavily used in real Azure environments for cost reporting, automation, and ownership.

## Time Needed

10-15 minutes.

## What You Will Learn

- What tags are
- How tags help organize resources
- How tags support cost reporting
- Why tags are not a security feature

## AZ-900 Concepts Covered

| Concept        | Where you see it in the lab              |
| -------------- | ---------------------------------------- |
| Tags           | You apply name/value metadata            |
| Cost reporting | You prepare resources for cost grouping  |
| Governance     | You learn why organizations require tags |

## Steps

### 1. Open a resource group

Open the resource group created in earlier labs, such as:

```text
rg-az900-labs
```

### 2. Open Tags

Select **Tags** from the left menu.

### 3. Add tags

Add:

| Name        | Value    |
| ----------- | -------- |
| Environment | Lab      |
| Exam        | AZ-900   |
| CostCenter  | Learning |
| Owner       | YourName |

### 4. Save tags

Save the changes.

### 5. Check resource tags

Open a resource inside the resource group and check its tags. Notice that tags may not automatically appear on child resources unless configured by policy or automation.

## Clean Up

No cleanup required. Tags are metadata and do not create charges.

## Success Criteria

You are done when you can explain:

- What a tag is
- Why tags help with cost reporting
- Why tags do not grant permissions
- Why companies often enforce required tags with Azure Policy


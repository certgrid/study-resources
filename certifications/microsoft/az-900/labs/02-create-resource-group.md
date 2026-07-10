# Lab 02 - Create a Resource Group

A resource group is one of the most important Azure basics. Most beginner labs should start with a dedicated resource group so cleanup is easy.

## Time Needed

10-15 minutes.

## What You Will Learn

- What a resource group is
- How region selection works for resource group metadata
- How tags help organize resources
- Why deleting a resource group is useful for cleanup

## AZ-900 Concepts Covered

| Concept        | Where you see it in the lab                 |
| -------------- | ------------------------------------------- |
| Resource group | You create a container for lab assets       |
| Region         | You choose where metadata is stored         |
| Tags           | You add basic organization metadata         |
| Lifecycle      | You learn how resource group deletion works |

## Steps

### 1. Open Resource groups

1. Go to the Azure portal.
2. Search for **Resource groups**.
3. Select **Create**.

### 2. Enter basics

Use a name like:

```text
rg-az900-labs
```

Choose a region close to you or your learning environment.

### 3. Add tags

Add simple tags:

| Name        | Value    |
| ----------- | -------- |
| Environment | Lab      |
| Exam        | AZ-900   |
| Owner       | YourName |

### 4. Review and create

Review the configuration and create the resource group.

### 5. Open the resource group

Notice tabs such as:

- Overview
- Activity log
- Access control (IAM)
- Tags
- Deployments

## Clean Up

If you plan to continue the next labs, keep the resource group. If you are stopping, delete it.

## Success Criteria

You are done when you can explain:

- What a resource group does
- Whether a resource can belong to multiple resource groups
- Why tags are useful
- Why deleting a resource group can remove all resources inside it


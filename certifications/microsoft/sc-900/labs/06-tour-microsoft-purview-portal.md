# Lab 06 - Tour the Microsoft Purview Portal

Microsoft Purview hosts nearly every domain 4 topic. This read-only tour maps the outline's compliance solutions to real portal locations.

## Time Needed

20-30 minutes.

## What You Will Learn

- The layout of the Microsoft Purview portal
- Where Compliance Manager and compliance score live
- Where classification tools (Content explorer, Activity explorer) live
- Where DLP, retention, records, insider risk, eDiscovery, and audit live

## SC-900 Concepts Covered

| Concept                  | Where you see it in the lab                      |
| ------------------------ | ------------------------------------------------ |
| Microsoft Purview portal | The portal itself                                |
| Compliance Manager       | Solution card with assessments and score         |
| Data classification      | Information protection classifiers and explorers |
| Sensitivity labels       | Information protection solution                  |
| DLP                      | Data loss prevention solution                    |
| Retention / records      | Data lifecycle management and records management |
| Insider risk             | Insider risk management solution                 |
| eDiscovery / audit       | eDiscovery and audit solutions                   |

## Access Note

The full experience needs a Microsoft 365 trial tenant (Lab 00). With a bare Azure account some solutions will be locked; still walk the menu and read each solution description, which is enough for SC-900 recognition.

## Steps

### 1. Sign in

1. Go to purview.microsoft.com with your lab account.
2. View the solution gallery. Notice Purview covers BOTH compliance solutions and data governance (Data Map, Data Catalog).

### 2. Compliance Manager

1. Open **Compliance Manager**.
2. Find the compliance score percentage and read how points come from improvement actions.
3. Open **Assessments** and note the default assessment (data protection baseline).
4. Browse **Regulations** to see prebuilt templates (GDPR, ISO 27001, NIST).

### 3. Information protection and classification

1. Open **Information protection**.
2. Find **Sensitivity labels**: read one built-in label's settings if present (encryption, content markings).
3. Open **Classifiers**: see **Sensitive info types** (search for "credit card") and **Trainable classifiers**.
4. Open **Explorers**: locate **Content explorer** (what/where snapshot) and **Activity explorer** (activity history). Access may be role-gated; the location is what matters.

### 4. Data loss prevention

1. Open **Data loss prevention** > **Policies**.
2. Start **Create policy** to view templates (e.g. financial data, health records), then CANCEL without creating.

### 5. Data lifecycle and records management

1. Open **Data lifecycle management**: see retention policies and retention labels.
2. Open **Records management**: see file plan and where an item becomes a record.

### 6. Risk and investigation solutions

1. Open **Insider risk management**: read the policy template names (data theft by departing users, data leaks).
2. Open **eDiscovery**: note Content search vs cases.
3. Open **Audit**: note the search page over activity logs.

## Clean Up

Nothing was created. Cancel any policy wizards you opened.

## Success Criteria

You are done when you can explain:

- The four jobs of Purview: prove trust, know data, protect/govern data, investigate
- Where compliance score is found and what feeds it
- The difference between Content explorer and Activity explorer from their pages
- Which solution you would open for: leaked credit cards in email (DLP), a legal hold (eDiscovery), a resigning employee (insider risk), "who deleted this site" (audit)

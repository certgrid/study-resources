# Lab 05 - Explore Microsoft Sentinel

Microsoft Sentinel is the SIEM/SOAR of the Microsoft stack. This lab is primarily a LOOK, not a build, because Sentinel can generate real costs.

## Time Needed

15-25 minutes (view-only path) or 40 minutes (free trial path).

## What You Will Learn

- What a SIEM and a SOAR do
- How Sentinel attaches to a Log Analytics workspace
- Where data connectors, analytics rules, and playbooks live
- How Sentinel pricing works (why cleanup matters)

## SC-900 Concepts Covered

| Concept          | Where you see it in the lab                   |
| ---------------- | --------------------------------------------- |
| SIEM             | Data connectors + analytics rules + incidents |
| SOAR             | Automation rules and playbooks                |
| Data connectors  | Content hub / connector gallery               |
| Threat detection | Analytics rule templates                      |
| Investigation    | Incidents and hunting pages                   |

## Cost Warning (Read First)

- Sentinel bills for DATA INGESTION into its Log Analytics workspace and for retention. Costs scale with data volume.
- There is a free trial (a daily ingestion allowance for a limited period) on new workspaces, but leaving a workspace running with connectors enabled can create charges after the trial.
- SAFEST PATH: follow the view-only steps (1-3) and skip creation. Only do the optional build if you accept trial limits and commit to Lab 09 cleanup.

## Steps

### 1. Find Sentinel (view-only)

1. Sign in to the Azure portal (portal.azure.com).
2. Search for **Microsoft Sentinel** and open it. Do not add it to a workspace yet.
3. Read the create screen: Sentinel must attach to a **Log Analytics workspace**. That workspace is where all collected logs live.

### 2. Study the concept map (view-only)

Say each mapping out loud:

| Sentinel piece               | Exam concept                                  |
| ---------------------------- | --------------------------------------------- |
| Data connectors              | Collect (SIEM) from Microsoft AND third party |
| Analytics rules              | Detect: correlate events into incidents       |
| Incidents / hunting          | Investigate                                   |
| Automation rules + playbooks | Respond (SOAR, built on Logic Apps)           |

### 3. Browse documentation gallery (view-only)

1. From the Sentinel create screen or Microsoft Learn, look at the list of data connector types: Microsoft 365, Entra ID, AWS, syslog, third-party firewalls.
2. This multi-vendor list is exactly why "third-party logs" questions answer Sentinel, not Defender XDR.

### 4. Optional: create a trial instance (cost-aware path)

1. Create a resource group named **rg-sc900-sentinel**.
2. Create a Log Analytics workspace in it.
3. Add Microsoft Sentinel to the workspace; note the free trial banner and its expiry date.
4. Open **Content hub** and browse solutions; open **Analytics** > **Rule templates** and read two or three template descriptions.
5. Open **Automation** to see where playbooks would attach.
6. Do NOT enable connectors that ingest large data volumes.

## Clean Up

If you built the optional instance: delete the **rg-sc900-sentinel** resource group NOW or at the latest in Lab 09. Deleting the resource group removes Sentinel and the workspace, which stops all ingestion billing.

## Success Criteria

You are done when you can explain:

- SIEM vs SOAR in one sentence each
- Why Sentinel needs a Log Analytics workspace
- Which component collects, which detects, which responds
- Why Sentinel answers "third-party log sources" questions instead of Defender XDR
- What drives Sentinel cost

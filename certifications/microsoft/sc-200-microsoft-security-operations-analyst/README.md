# SC-200: Microsoft Security Operations Analyst - Study Cheatsheet

The SC-200: Microsoft Security Operations Analyst exam validates your ability to run a security operations center using Microsoft Sentinel, Microsoft Defender XDR, and Microsoft Defender for Cloud. It targets SOC analysts who configure protections and detections, triage and respond to incidents, and proactively hunt threats across Microsoft's security stack. Expect 685-style scenario questions covering workspace design, KQL, analytics rules, automation, and the unified Defender portal experience, with a passing score of 700 over 120 minutes.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | SC-200 |
| Credential | SC-200: Microsoft Security Operations Analyst |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Manage a Security Operations Environment | ~27% |
| 2 | Configure Protections and Detections | ~24% |
| 3 | Manage Incident Response | ~26% |
| 4 | Perform Threat Hunting | ~23% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Manage a Security Operations Environment

- Microsoft's recommended Sentinel architecture for multi-subscription, multi-region tenants is a single centralized Log Analytics workspace with Sentinel enabled, simplifying cross-source correlation, RBAC, and analytics.
- Sentinel built-in roles are Reader, Responder (triage/manage incidents and run playbooks), and Contributor (create/edit rules and content); assign the least-privilege role plus Log Analytics roles as needed.
- Retention can be set per table to override the workspace default - for example setting SecurityEvent to 180 days extends only that table without raising cost on every other table.
- The long-term retention (archive) tier stores data cheaply beyond the interactive retention period; you run search jobs or restore archived data to query it.
- The Content Hub is the centralized marketplace for packaged solutions that bundle data connectors, analytics rules, workbooks, hunting queries, and playbooks, deployable in a single action.
- Threat indicators are imported via purpose-built connectors: Microsoft Defender Threat Intelligence (curated Microsoft IOCs) and Threat Intelligence - TAXII (connect to a TAXII 2.x server), landing in the ThreatIntelligenceIndicator table.

### Domain 2 - Configure Protections and Detections

- Scheduled query analytics rules run on a configurable frequency (as short as every 5 minutes) over a lookback window and aggregate with KQL - the right choice for threshold-based detections like brute-force sign-in counts.
- Near-real-time (NRT) analytics rules run automatically once per minute with a fixed one-minute lookback (querying on ingestion time to absorb data-source delay); they are limited to a single query with no scheduling flexibility but minimize detection latency.
- Microsoft Sentinel includes ML-driven anomaly rule templates (impossible travel, unusual data transfer, anomalous sign-ins) that detect outliers without manual query authoring.
- Fusion correlates alerts from multiple data sources into multi-stage attack incidents using machine learning; it is enabled by default and surfaces high-fidelity advanced threats.
- Microsoft Defender for Identity monitors Active Directory authentication (Kerberos and NTLM) to detect lateral movement such as Pass-the-Hash and Pass-the-Ticket; sensors install on domain controllers (or a standalone sensor with port mirroring).
- A honeytoken account is tagged in Defender for Identity settings; any authentication activity against it is suspicious by design and raises an alert.

### Domain 3 - Manage Incident Response

- The Sentinel Investigation Graph visually maps an incident's entities (users, hosts, IPs, files) and the alerts connecting them, letting analysts expand related entities to scope an attack quickly.
- Automation rules evaluate incident properties (severity, MITRE tactic, title) at creation or update and can assign owners, change severity, add tags, close incidents, or run playbooks.
- Within an automation rule, actions execute sequentially in the order they are defined; ordering matters when one action depends on a prior one.
- Playbooks are Azure Logic Apps; the Microsoft Sentinel incident trigger runs them on incident events, the entity trigger runs them on a specific entity, and connectors (Teams, email, ServiceNow) perform the response actions.
- A playbook's Logic App managed identity must hold the Microsoft Sentinel Responder role on the resource group (or workspace) to update incidents it acts on.
- Defender for Endpoint 'Isolate device' cuts network connectivity while preserving the Defender service channel so the analyst can still investigate and run live response.

### Domain 4 - Perform Threat Hunting

- Livestream runs a KQL query continuously and notifies you when results appear, without creating alerts or incidents - ideal for watching an active hunt or emerging campaign in real time.
- Hunting bookmarks preserve interesting query results along with the query and analyst notes; bookmarks can be promoted to incidents or added to existing ones.
- Promising hunting queries can be operationalized by promoting them to a scheduled analytics rule, or to an NRT rule when low detection latency is required.
- The MITRE ATT&CK blade maps active analytics rules and hunting queries to tactics and techniques, visualizing detection coverage and highlighting gaps.
- Threat Intelligence matching analytics rules automatically correlate ThreatIntelligenceIndicator entries against log tables to surface IOC hits; you can also manually join the TI table with log tables.
- Sentinel Jupyter notebooks run on Azure Machine Learning compute instances linked to the workspace, using MSTICPy and Sentinel APIs for advanced Python-based analysis.

## Study tips

- Know exactly which analytics rule type fits a scenario: Scheduled for aggregated thresholds, NRT for ~1-minute low-latency single-query detection, Microsoft incident-creation for provider alerts, and anomaly/Fusion for ML-driven detection.
- Memorize the Defender for Endpoint response actions and what each preserves: Isolate device (keeps Defender connectivity), Collect investigation package (forensics), Run AV scan, and Restrict app execution.
- Practice reading KQL: recognize join, summarize, make-series with series_decompose_anomalies(), project, and the common advanced hunting table names - questions hinge on picking the right table and operator.
- Distinguish the Microsoft security products by what data they protect: Defender for Identity (on-prem AD/Kerberos/NTLM), Defender for Cloud Apps (SaaS/shadow IT), Defender for Office 365 (email/Safe Links/Safe Attachments), Defender for Endpoint (devices).
- Watch for cost and architecture cues - single centralized workspace, per-table retention, archive tier, 'Common' vs 'All Events', and AMA-with-DCR over the deprecated MMA - these phrases signal the intended answer.

---

Want the full breakdown? See the complete **[SC-200 study guide](https://certgrid.app/study-guide/sc-200-microsoft-security-operations-analyst)** and **[free practice questions](https://certgrid.app/practice/sc-200-microsoft-security-operations-analyst)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


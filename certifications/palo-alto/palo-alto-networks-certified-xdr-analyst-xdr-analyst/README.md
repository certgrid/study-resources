# Palo Alto Networks Certified XDR Analyst (XDR-Analyst) - Study Cheatsheet

The Palo Alto Networks Certified XDR Analyst (XDR-Analyst) validates a SOC analyst's ability to operate Cortex XDR day to day: triaging alerts, investigating and responding to incidents, hunting through telemetry with XQL, and managing endpoint security policy. It targets Tier 1 and Tier 2 analysts and threat hunters who work in the Cortex XDR console. The exam covers alert sources and detection rules (Analytics, BIOC, IOC, correlation), causality-based incident analysis and response actions, XQL query construction, and agent and prevention policy administration.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Palo Alto Networks Certified XDR Analyst (XDR-Analyst) |
| Credential | Palo Alto Networks Certified XDR Analyst (XDR-Analyst) |
| Level | Intermediate |
| Practice mock length | ~75 questions |
| Duration | ~90 minutes |
| Passing score | 700 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Alerting and Detection Processes | ~23% |
| 2 | Incident Handling and Response | ~34% |
| 3 | Data Analysis | ~28% |
| 4 | Endpoint Security Management | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Alerting and Detection Processes

- Marking a single alert as a false positive only closes that one alert instance and does not change future detection; to stop recurrence you must tune the correlation rule or create an alert exclusion.
- A correlation rule's alert severity, category, and description are set by the rule author and applied to every alert it generates, not derived from viewer settings or the number of enabled rules.
- IOC rules match known-bad static atomic indicators such as file hashes, domains, and IP addresses (well suited to threat-intel feeds), while BIOC rules match real-time endpoint behavior like process execution, network connections, file, and registry activity.
- Custom BIOC and correlation rules in Cortex XDR are authored using XQL, and mapping a rule to a MITRE ATT&CK technique adds adversary-tactic context to its detections.
- Behavior-based modules catch novel threats: ransomware protection detects the encryption-like pattern itself (and can restore files from pre-encryption copies), behavioral threat protection correlates process lineage across related processes, and exploit prevention watches the exploitation technique rather than a known vulnerability.
- A causality chain traces the parent-to-child process lineage that connects related activity on a host, and Cortex XDR groups alerts by shared host involvement and temporal proximity within that chain.

### Domain 2 - Incident Handling and Response

- Incident severity equals the maximum severity among its alerts, so an incident containing only Low alerts is rated Low; the scale runs Low, Medium, High, up to Critical.
- Cortex XDR automatically correlates alerts that share artifacts such as the same malicious IP address, or the same host and user account, into a single incident without manual analyst action.
- New and Under Investigation both indicate an incident that has not reached a final closed state, with Under Investigation marking one an analyst is actively reviewing, and the alert timeline presents events chronologically to reconstruct how the attack unfolded.
- The causality view's process tree shows full parent-to-child lineage plus associated file, registry, and network activity, revealing everything downstream of the initiating process to gauge impact.
- A causality chain is endpoint-specific, built from activity observed on that host; whether a new event's lineage traces back to the same causality group owner determines chain membership.
- Isolating an endpoint cuts its network connectivity and does not expire automatically; connectivity is restored only by explicitly canceling the isolation in the console.

### Domain 3 - Data Analysis

- XQL queries typically begin with the dataset keyword to specify the data source, and xdr_data is the primary dataset holding raw endpoint telemetry: process, network, file, and registry activity.
- Query Builder searches translate into equivalent XQL behind the scenes, and switching to the XQL view shows the auto-generated query; choose the category by intent, using Process Event filtered by process name to find which endpoints ran a process and Network Event for connections to an external IP.
- Matching network events uses the enum comparison event_type = ENUM.NETWORK, not a quoted text string; using the wrong syntax causes the condition to match no rows.
- causality_actor_process fields trace an event back to the process that started the entire causal chain, while action_process fields describe the process created as a result of the recorded action.
- A by clause listing multiple fields groups rows by every unique combination of those field values, and the union stage can combine results from queries against different datasets, not only identical ones.
- In a join, multiple matching field pairs can be combined with 'and' so all pairs must match, but null values in a join key can prevent rows from matching, producing missing or incomplete results.

### Domain 4 - Endpoint Security Management

- Restrictions profiles govern where and how executable files are permitted to launch; when a trusted app is wrongly blocked, the fix is to narrow or add a targeted exception to the Restrictions rule for its path, not disable unrelated profiles.
- Policy rules define their target endpoints, attached profiles, name, and order position; static groups hold a fixed manually chosen endpoint list while dynamic groups update membership from filter criteria that can combine attributes like operating system and domain.
- An agent upgrade policy controls which endpoints move to a new agent version and on what timeline, letting admins validate a build on a subset before wider rollout; it does not govern content updates, scans, or licensing.
- Local analysis uses a static on-agent machine-learning model to produce an immediate verdict even without cloud connectivity, while WildFire performs deeper cloud static and dynamic analysis that refines the verdict, though requiring a verdict before execution can briefly delay legitimate unknown files.
- Device Control policies restrict removable devices at the device-class level, such as all mass-storage devices, and exceptions should be scoped as narrowly as practical to limit the risk they introduce.
- A device-specific exception lets one approved device through by targeting its identifiers while the broader policy continues blocking similar devices.

## Study tips

- Know the difference between resolving or marking a single alert (per-instance only) versus tuning a rule or creating an exclusion (stops recurrence); the exam repeatedly tests that a false-positive mark does not change future detection.
- Be able to place a detection in the right rule type: IOC for static known-bad indicators, BIOC for real-time endpoint behavior, correlation rules for cross-signal logic, all authored in XQL.
- Memorize how severity rolls up: incident severity equals the highest alert severity plus host/user scope, and correlation-rule alert severity is set by the rule author, not the viewer.
- For XQL questions, remember queries start with dataset, xdr_data holds endpoint telemetry, enum fields use ENUM.NETWORK syntax, and causality_actor_process versus action_process distinguish the chain originator from the resulting process.
- For endpoint management, know that isolation must be manually canceled, deleting an endpoint frees a license but leaves the agent installed, and blocking behavior differs between local analysis, WildFire, Restrictions, and Device Control.

---

Want the full breakdown? See the complete **[Palo Alto Networks Certified XDR Analyst (XDR-Analyst) study guide](https://certgrid.app/study-guide/palo-alto-networks-certified-xdr-analyst-xdr-analyst)** and **[free practice questions](https://certgrid.app/practice/palo-alto-networks-certified-xdr-analyst-xdr-analyst)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


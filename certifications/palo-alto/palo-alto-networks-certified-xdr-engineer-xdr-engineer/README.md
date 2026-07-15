# Palo Alto Networks Certified XDR Engineer (XDR-Engineer) - Study Cheatsheet

The Palo Alto Networks Certified XDR Engineer (XDR-Engineer) validates that you can deploy, configure, and operate Cortex XDR end to end. It targets security engineers and administrators who plan installations, roll out agents, onboard and parse logs, build detections, and troubleshoot the platform. The 90-minute exam covers planning and installation, agent configuration, ingestion and automation, detection engineering and reporting, and ongoing maintenance and troubleshooting.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Palo Alto Networks Certified XDR Engineer (XDR-Engineer) |
| Credential | Palo Alto Networks Certified XDR Engineer (XDR-Engineer) |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~90 minutes |
| Passing score | 700 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Planning and Installation | ~14% |
| 2 | Cortex XDR Agent Configuration | ~22% |
| 3 | Ingestion and Automation | ~22% |
| 4 | Detection and Reporting | ~22% |
| 5 | Maintenance and Troubleshooting | ~20% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Planning and Installation

- The Cortex XDR agent installs on Windows, macOS, and Linux endpoints; installing the Linux agent requires root or an account with equivalent elevated privileges.
- A fresh install package performs a complete initial installation and registration for endpoints that have no existing agent; it does not migrate alert history between tenants.
- A platform-specific installation package bundles the installer, proxy configuration, and policy assignment, so tying it to an endpoint group and policy ensures endpoints receive the correct policy automatically; proxy settings can be embedded at build time or applied later through policy.
- Broker VM applets extend collection: the Windows Event Collector pulls or receives Windows event logs (via WinRM or Windows Event Forwarding) from hosts without an agent, the Syslog Collector listens over TCP or UDP for forwarded logs, and the Local Agent Settings applet caches agent content locally to cut redundant internet traffic.
- VMware ESXi is a supported virtualization platform for hosting the Broker VM; setup follows deploy the appliance, configure the network, then register.
- A registration token is a tenant-specific credential used to link a Broker VM to the correct Cortex XDR tenant.

### Domain 2 - Cortex XDR Agent Configuration

- Exploit protection targets technique-based abuse of legitimate processes (memory corruption, code-reuse chains, heap tampering, kernel privilege escalation), while malware protection evaluates files, hashes, and behavior for a malicious verdict.
- Administrators extend exploit protection by adding an application's process to the profile's protected process list, applying the configured modules to custom or line-of-business software.
- A policy rule assigns a specific exploit protection profile to a defined endpoint group, allowing different enforcement levels across the environment; a built-in default policy guarantees every endpoint always has settings applied.
- Best practice is to pilot a new exploit protection profile in Report mode before enforcing it broadly in Block mode, scoping the pilot with a higher-ranked, narrowly scoped rule.
- Rule rank resolves conflicts: an endpoint group can be referenced by several rules, and a pilot rule ranked below the production rule never applies to overlapping endpoints.
- Dynamic groups auto-track a broad, changing population (for example all macOS endpoints via an OS filter), while static groups fit small, fixed, manually curated membership; a name pattern filter targets endpoints by hostname format.

### Domain 3 - Ingestion and Automation

- A Broker VM with the appropriate collection module gathers third-party logs and forwards them into Cortex XDR: the Syslog Collector receives forwarded server syslog, and the Windows Event Collector receives events via Windows Event Forwarding, both without an agent on the source.
- Each source format should be handled by its own collector instance configured for that specific format.
- Firewall (NGFW) logs reveal internal host-to-host traffic for lateral movement detection, so network activity for a host can be analyzed even without an agent installed on it.
- CloudTrail logs give visibility into AWS API calls and administrative activity, and Active Directory authentication logs enable identity analytics for detecting anomalous logon behavior.
- Creating an API key requires a name and an associated role; minimizing a key's permissions follows least privilege, for example scoping a reporting key to read-only so a leak cannot trigger isolation or config changes.
- Requests using an Advanced API key pass the numeric key identifier in the x-xdr-auth-id header alongside the Authorization header, and both values are required for verification.

### Domain 4 - Detection and Reporting

- BIOC rules match behavior on individual real-time events or causality chains, while correlation rules run scheduled XQL queries that can aggregate counts and join across multiple events and datasets over a time window.
- Correlating two distinct events, such as a file write followed by a registry change within a defined window, is a correlation rule use case that single-event BIOC logic cannot express.
- Custom BIOC rules are authored and maintained by the customer's detection engineers, whereas Analytics BIOC rules are written by Palo Alto Networks and delivered through content updates; both are rule-based and require no baseline.
- BIOC categories match by event type: a file rule matches path and extension, a process rule matches process name, command line, and parent process, and a registry rule matches activity like adding a value to an autorun key.
- A cryptographic file hash such as SHA256 is derived purely from file content, so it matches regardless of the file's name or location, unlike easily altered filename or path indicators.
- Indicator metadata aids triage: the class or category field labels the threat type, the source or vendor field records the indicator's origin, and expiration settings let stale indicators stop matching; teams add indicators in bulk via CSV upload or threat intel feed integration rather than one by one.

### Domain 5 - Maintenance and Troubleshooting

- Decommissioned endpoints left in the console keep consuming licensed endpoint capacity, so regular cleanup of stale records and uninstalling the agent are part of good license hygiene.
- In a proxy-restricted environment, the Broker VM's own proxy configuration must point at the proxy so it can reach the tenant, and even with correct firewall rules a broker that cannot resolve the tenant's FQDN through DNS will fail to connect.
- Significant clock drift on a Broker VM can break the TLS trust used to establish its secure tenant session, failing the connection even when the network path and firewall rules are fully correct.
- A connected agent stuck on old content points to a connectivity problem specifically with the content distribution servers, since basic check-in and content delivery can use different paths.
- Local content caching on the Broker VM and scheduled update windows both reduce redundant WAN traffic and avoid peak-hour contention at remote sites.
- Re-registering restores tenant identity and trust using the existing installation, which is faster and less disruptive than a full reinstall that replaces binaries and resets local configuration; end-of-life agent versions stop receiving new content updates over time.

## Study tips

- Master the difference between BIOC rules (single real-time events or causality chains) and correlation rules (scheduled XQL that aggregates and joins across datasets); this distinction is tested repeatedly.
- For any rollout question, reason through rule rank first: a lower-ranked rule never applies to endpoints already covered by a higher-ranked one, so pilots must be higher-ranked and narrowly scoped.
- When a scenario describes a broker or agent that cannot connect, walk the layered checklist in order: DNS resolution of the tenant FQDN, proxy configuration, firewall or outbound rules, and clock or NTP drift affecting TLS.
- Remember the least-scoped fix wins: prefer a narrow exception (specific hash) or scope exclusion over disabling a module or granting broad rights, and pilot in Report mode before Block.
- Know your data-source-to-detection mapping cold (firewall logs for lateral movement, AD auth logs for identity analytics, CloudTrail for AWS), because Analytics only works when its required sources are validated as flowing in.

---

Want the full breakdown? See the complete **[Palo Alto Networks Certified XDR Engineer (XDR-Engineer) study guide](https://certgrid.app/study-guide/palo-alto-networks-certified-xdr-engineer-xdr-engineer)** and **[free practice questions](https://certgrid.app/practice/palo-alto-networks-certified-xdr-engineer-xdr-engineer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


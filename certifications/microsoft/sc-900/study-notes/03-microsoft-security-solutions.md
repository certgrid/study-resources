# 03 - Describe the Capabilities of Microsoft Security Solutions

This domain is worth 35-40% of the exam, making it the heaviest domain. It covers core Azure infrastructure security services (DDoS Protection, Azure Firewall, WAF, virtual network segmentation, NSGs, Azure Bastion, Key Vault), security management with Microsoft Defender for Cloud, SIEM/SOAR with Microsoft Sentinel, and threat protection with Microsoft Defender XDR and its member services.

## Mental model

Three product layers answer three different questions:

1. Azure infrastructure services protect networks and secrets inside Azure.
2. Microsoft Defender for Cloud watches the security POSTURE of cloud workloads.
3. Microsoft Sentinel (SIEM/SOAR) and Microsoft Defender XDR detect and respond to ATTACKS.

| Scenario keyword                                    | Likely concept                              |
| --------------------------------------------------- | ------------------------------------------- |
| Absorb volumetric traffic floods                    | Azure DDoS Protection                       |
| Central network traffic filtering across VNets      | Azure Firewall                              |
| Protect web apps from SQL injection / XSS           | Web Application Firewall (WAF)              |
| Isolate workloads into subnets                      | Network segmentation with VNets             |
| Allow/deny rules on subnet or NIC                   | Network security group (NSG)                |
| RDP/SSH without public IP on the VM                 | Azure Bastion                               |
| Store keys, secrets, certificates                   | Azure Key Vault                             |
| Security posture and recommendations for cloud      | Microsoft Defender for Cloud (CSPM)         |
| Protect servers, databases, containers workloads    | Cloud workload protection (Defender plans)  |
| Collect and analyze logs from everywhere (SIEM)     | Microsoft Sentinel                          |
| Automate response with playbooks (SOAR)             | Microsoft Sentinel                          |
| Coordinated detection across email, endpoints, apps | Microsoft Defender XDR                      |
| Protect email and collaboration from phishing       | Microsoft Defender for Office 365           |
| Protect and investigate devices (EDR)               | Microsoft Defender for Endpoint             |
| Discover shadow IT, secure SaaS apps                | Microsoft Defender for Cloud Apps           |
| Detect attacks on on-premises Active Directory      | Microsoft Defender for Identity             |
| Find and prioritize device vulnerabilities          | Microsoft Defender Vulnerability Management |
| Research threat actors and indicators               | Microsoft Defender Threat Intelligence      |

## Core infrastructure security services in Azure

### Azure DDoS Protection

Distributed denial of service (DDoS) attacks flood a service with traffic to exhaust it. Azure DDoS Protection defends at the network edge.

| Tier                     | What you get                                                                     |
| ------------------------ | -------------------------------------------------------------------------------- |
| Infrastructure (default) | Basic always-on protection for the Azure platform itself, free                   |
| Network Protection       | Paid tier with tuning to your traffic, telemetry, alerts, rapid response support |

Attack types to recognize: volumetric (bandwidth floods), protocol (exploit layer 3/4 weaknesses), resource/application layer (target web apps).

### Azure Firewall

Azure Firewall is a managed, cloud-based network firewall service that protects Azure Virtual Network resources.

| Feature                    | Detail                                                                |
| -------------------------- | --------------------------------------------------------------------- |
| Fully stateful             | Tracks connections, not just individual packets                       |
| Built-in high availability | No extra load balancers needed                                        |
| Central rules              | Enforce application and network rules across subscriptions and VNets  |
| Threat intelligence        | Can alert on and deny traffic to/from known malicious IPs and domains |
| SNAT and DNAT              | Translates addresses for outbound and inbound traffic                 |

### Azure Web Application Firewall (WAF)

WAF protects web applications from common web exploits such as SQL injection and cross-site scripting (XSS). It deploys with services like Azure Application Gateway and Azure Front Door and applies rule sets centrally, so you do not patch each app for these attack classes individually.

Memory hook: Azure Firewall = network traffic in general. WAF = HTTP attacks against web apps specifically.

### Network segmentation with Azure virtual networks

An Azure virtual network (VNet) is your private network in Azure. Segmentation divides it into subnets so workloads are isolated and traffic between segments can be controlled.

Why segment:

- Contain a breach to one segment (supports Zero Trust "assume breach").
- Group resources with similar sensitivity and apply controls per segment.
- Reduce the attack surface between tiers (web, app, database).

### Network security groups (NSGs)

NSGs filter network traffic to and from Azure resources within a VNet.

| Aspect          | Detail                                                                                |
| --------------- | ------------------------------------------------------------------------------------- |
| Where applied   | Subnets and network interfaces                                                        |
| Rule properties | Name, priority (lower number wins), source/destination, port, protocol, allow or deny |
| Direction       | Separate inbound and outbound rules                                                   |
| Default rules   | Built-in rules that can be overridden by higher-priority custom rules (not deleted)   |

NSG vs Azure Firewall:

| Aspect       | NSG                                 | Azure Firewall                                   |
| ------------ | ----------------------------------- | ------------------------------------------------ |
| Scope        | Basic layer 3/4 filtering in a VNet | Full managed firewall across VNets/subscriptions |
| Intelligence | Simple allow/deny rules             | Threat intelligence, FQDN and application rules  |
| Typical use  | Micro-segmentation inside a VNet    | Centralized perimeter for hub-and-spoke networks |

### Azure Bastion

Azure Bastion provides secure RDP and SSH connectivity to virtual machines directly from the Azure portal over TLS, without exposing the VMs through public IP addresses on RDP/SSH ports.

Keywords: "no public IP on the VM," "no RDP/SSH ports open to the internet," "connect through the browser."

### Azure Key Vault

Azure Key Vault stores and controls access to secrets, encryption keys, and certificates.

| Object type  | Example                                         |
| ------------ | ----------------------------------------------- |
| Secrets      | Connection strings, API keys, passwords         |
| Keys         | Encryption keys used by apps and services       |
| Certificates | TLS/SSL certificate provisioning and management |

Key Vault also supports hardware security module (HSM) backed keys and helps remove secrets from application code (pairs naturally with managed identities).

## Security management: Microsoft Defender for Cloud

Microsoft Defender for Cloud is a cloud-native application protection platform (CNAPP) that measures and improves the security posture of resources in Azure, on-premises, and other clouds (AWS, GCP), and protects workloads against threats.

### Cloud Security Posture Management (CSPM)

| Element              | What it gives you                                               |
| -------------------- | --------------------------------------------------------------- |
| Secure score         | A percentage measuring your current security posture            |
| Recommendations      | Prioritized actions to harden resources                         |
| Foundational CSPM    | Free tier: secure score, basic recommendations                  |
| Defender CSPM (paid) | Advanced posture: attack path analysis, cloud security explorer |

### Security policies, standards, and recommendations

| Term              | Meaning                                                                                         |
| ----------------- | ----------------------------------------------------------------------------------------------- |
| Security standard | A set of requirements, e.g. Microsoft Cloud Security Benchmark (MCSB), applied to subscriptions |
| Security policy   | The implemented rule (built on Azure Policy) that checks a requirement                          |
| Recommendation    | The "fix this" guidance produced when resources fail a check                                    |

The Microsoft Cloud Security Benchmark is applied by default; regulatory standards (e.g. PCI DSS, ISO) can be added.

### Cloud workload protection (CWP)

Enhanced security comes from Defender plans that protect specific workload types with threat detection and alerts.

| Defender plan (examples) | Protects                                                      |
| ------------------------ | ------------------------------------------------------------- |
| Defender for Servers     | Windows and Linux machines (integrates Defender for Endpoint) |
| Defender for Storage     | Storage accounts (malware, unusual access)                    |
| Defender for Databases   | SQL and open-source databases                                 |
| Defender for Containers  | Kubernetes and container registries                           |
| Defender for App Service | Web apps running on App Service                               |
| Defender for Key Vault   | Unusual access attempts to vaults                             |

Memory hook: CSPM = "how healthy is my configuration?" CWP = "is something attacking this workload right now?"

## Microsoft Sentinel

Microsoft Sentinel is Microsoft's cloud-native SIEM and SOAR solution.

| Term | Full name                                        | Job                                                                     |
| ---- | ------------------------------------------------ | ----------------------------------------------------------------------- |
| SIEM | Security information and event management        | Collect logs and events across the estate, analyze, detect, investigate |
| SOAR | Security orchestration, automation, and response | Automate responses to alerts and incidents                              |

Sentinel end-to-end flow (collect, detect, investigate, respond):

| Capability  | How Sentinel delivers it                                                                                                   |
| ----------- | -------------------------------------------------------------------------------------------------------------------------- |
| Collect     | Data connectors ingest logs from Microsoft 365, Azure, AWS, third-party firewalls, and more into a Log Analytics workspace |
| Detect      | Built-in and custom analytics rules correlate events into alerts and incidents; user and entity behavior analytics (UEBA)  |
| Investigate | Incidents, investigation graph, hunting queries (KQL), workbooks for visualization                                         |
| Respond     | Automation rules and playbooks (built on Azure Logic Apps) for automated response                                          |

Cost note: Sentinel bills for data ingestion and retention in the workspace. This matters in labs and in "watch the cost" style wording.

Exam anchor: any question combining Microsoft AND third-party/multi-vendor log sources, or asking for SOAR playbooks, points to Microsoft Sentinel.

## Threat protection with Microsoft Defender XDR

Microsoft Defender XDR (extended detection and response) is a unified pre-breach and post-breach defense suite that coordinates detection, prevention, investigation, and response across endpoints, identities, email, and applications. Signals from the member services are correlated into single incidents, and automated self-healing can remediate affected assets.

### The Defender XDR services

| Service                                              | Protects                                | Recognize it by                                                                                       |
| ---------------------------------------------------- | --------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Microsoft Defender for Office 365                    | Email and collaboration tools           | Phishing, malicious links/attachments (Safe Links, Safe Attachments), attack simulation training      |
| Microsoft Defender for Endpoint                      | Devices (Windows, macOS, Linux, mobile) | EDR, attack surface reduction, automated investigation on endpoints                                   |
| Microsoft Defender for Cloud Apps                    | SaaS applications                       | Cloud access security broker (CASB), shadow IT discovery, app governance, session controls            |
| Microsoft Defender for Identity                      | On-premises Active Directory            | Sensors on domain controllers, detects identity attacks like pass-the-hash and lateral movement       |
| Microsoft Defender Vulnerability Management          | Device vulnerabilities                  | Continuous asset inventory, vulnerability assessment, risk-based prioritization, remediation tracking |
| Microsoft Defender Threat Intelligence (Defender TI) | Threat research                         | Threat actor profiles, indicators of compromise, infrastructure analysis for hunters and responders   |

### The Microsoft Defender portal

The Microsoft Defender portal (security.microsoft.com) is the single home for Defender XDR:

- Unified incidents and alerts queue across all Defender services
- Advanced hunting with KQL across email, endpoint, identity, and app data
- Threat analytics reports from Microsoft researchers
- Microsoft Secure Score for improving the security posture of the Microsoft 365 environment
- Exposure management and threat intelligence views
- Microsoft Sentinel can also be connected into the unified portal experience

Secure score disambiguation:

| Score                              | Lives in                   | Measures                          |
| ---------------------------------- | -------------------------- | --------------------------------- |
| Microsoft Secure Score             | Microsoft Defender portal  | Microsoft 365 environment posture |
| Secure score in Defender for Cloud | Defender for Cloud (Azure) | Azure/multicloud workload posture |

## Defender for Cloud vs Defender XDR vs Sentinel

The single most tested comparison in this domain:

| Product                      | Category           | Focus                                                                              |
| ---------------------------- | ------------------ | ---------------------------------------------------------------------------------- |
| Microsoft Defender for Cloud | CNAPP (CSPM + CWP) | Posture and workload protection for Azure/multicloud infrastructure                |
| Microsoft Defender XDR       | XDR                | Detect and respond to attacks across M365: email, endpoints, identities, SaaS apps |
| Microsoft Sentinel           | SIEM + SOAR        | Collect and correlate ALL logs (Microsoft + third party), hunt, automate response  |

They complement each other: Defender for Cloud and Defender XDR generate alerts; Sentinel can ingest those alerts alongside everything else.

## Common confusions

| Confusion                                                  | Correct idea                                                                 |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Azure Firewall vs NSG                                      | Managed central firewall with intelligence vs basic subnet/NIC traffic rules |
| Azure Firewall vs WAF                                      | General network traffic vs HTTP attacks on web apps (SQL injection, XSS)     |
| DDoS Protection vs Azure Firewall                          | Absorbing traffic floods vs filtering traffic by rules                       |
| Defender for Cloud vs Defender XDR                         | Cloud infrastructure posture/workloads vs M365 attack detection and response |
| Defender XDR vs Sentinel                                   | Microsoft-stack XDR vs SIEM/SOAR for all sources including third party       |
| Defender for Identity vs Entra ID Protection               | On-premises AD attack detection vs cloud sign-in/user risk detection         |
| Defender for Endpoint vs Defender Vulnerability Management | Detect/respond on devices vs find and prioritize weaknesses                  |
| Microsoft Secure Score vs Defender for Cloud secure score  | M365 posture vs Azure/multicloud posture                                     |
| Bastion vs VPN                                             | Portal-based RDP/SSH to VMs vs network-level connectivity                    |

## Exam traps

| Trap                                                     | Why people miss it                                                                                       |
| -------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| "Use Defender XDR to collect third-party firewall logs"  | Third-party/multi-vendor log collection is SIEM territory: Microsoft Sentinel.                           |
| "NSGs inspect application-layer web attacks"             | NSGs filter by IP/port/protocol; WAF handles SQL injection and XSS.                                      |
| "Defender for Cloud Apps protects Azure infrastructure"  | It is a CASB for SaaS applications; Defender for Cloud covers infrastructure.                            |
| "Defender for Identity watches Entra ID sign-ins"        | It monitors on-premises AD via domain controller sensors; Entra ID Protection covers cloud sign-in risk. |
| "Open RDP with a public IP but restrict by NSG"          | The Bastion answer wins: no public IP, no exposed RDP/SSH ports.                                         |
| "Key Vault encrypts your application data automatically" | Key Vault stores and controls keys/secrets/certificates; apps still use them.                            |
| "Sentinel playbooks are free"                            | Sentinel bills for ingestion; playbooks run on Logic Apps. Watch cost wording.                           |
| "SOAR means collecting logs"                             | Collection/analysis is SIEM; SOAR is orchestrated, automated response.                                   |

## Mini scenarios

| Scenario                                                                              | Best answer                                 |
| ------------------------------------------------------------------------------------- | ------------------------------------------- |
| A public website must stay online during a large-scale traffic flood attack.          | Azure DDoS Protection (Network Protection)  |
| Block SQL injection attempts against a customer-facing web app.                       | Web Application Firewall (WAF)              |
| Allow only port 443 inbound to a subnet of web servers.                               | Network security group (NSG)                |
| Admins need RDP to VMs that must not have public IP addresses.                        | Azure Bastion                               |
| An app needs its database connection string kept out of source code.                  | Azure Key Vault (with a managed identity)   |
| Measure and improve the security configuration of Azure and AWS resources.            | Microsoft Defender for Cloud (CSPM)         |
| Aggregate logs from Microsoft 365, Azure, and Palo Alto firewalls, then auto-respond. | Microsoft Sentinel (SIEM + SOAR)            |
| Detect a phishing campaign with malicious attachments sent to employees.              | Microsoft Defender for Office 365           |
| Investigate malware detected on corporate laptops and isolate a device.               | Microsoft Defender for Endpoint             |
| Discover which unsanctioned SaaS apps employees are using.                            | Microsoft Defender for Cloud Apps           |
| Detect pass-the-hash and lateral movement against on-premises domain controllers.     | Microsoft Defender for Identity             |
| Continuously find and prioritize CVEs across the device fleet.                        | Microsoft Defender Vulnerability Management |

## Check yourself

1. Which service protects web applications from SQL injection and cross-site scripting?
2. What is the difference between an NSG and Azure Firewall?
3. How does Azure Bastion improve VM administration security?
4. What three object types does Azure Key Vault manage?
5. What is the difference between CSPM and cloud workload protection in Defender for Cloud?
6. Define SIEM and SOAR, and name the Microsoft product that provides both.
7. Which Defender XDR service protects on-premises Active Directory, and which protects SaaS apps?
8. Where do you find Microsoft Secure Score, and what does it measure compared to the secure score in Defender for Cloud?

## Answer guide

1. Azure Web Application Firewall (WAF), deployed with Application Gateway or Front Door.
2. An NSG provides basic allow/deny filtering by IP, port, and protocol at subnet/NIC level; Azure Firewall is a managed, stateful, centralized firewall with threat intelligence and application-level rules across VNets.
3. It provides RDP/SSH through the Azure portal over TLS so VMs need no public IPs and no exposed RDP/SSH ports.
4. Secrets, keys, and certificates.
5. CSPM assesses and scores configuration posture and gives recommendations; cloud workload protection (Defender plans) provides threat detection and alerts for specific workloads like servers, storage, and databases.
6. SIEM collects and analyzes security data at scale for detection and investigation; SOAR automates and orchestrates response. Microsoft Sentinel delivers both.
7. Microsoft Defender for Identity protects on-premises AD; Microsoft Defender for Cloud Apps (a CASB) protects SaaS applications.
8. Microsoft Secure Score is in the Microsoft Defender portal and measures Microsoft 365 posture; the secure score in Microsoft Defender for Cloud measures Azure/multicloud workload posture.

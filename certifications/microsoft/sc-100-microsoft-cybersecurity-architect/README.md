# SC-100: Microsoft Cybersecurity Architect - Study Cheatsheet

Microsoft SC-100 (Cybersecurity Architect) validates your ability to design and continuously evolve an enterprise cybersecurity strategy across Zero Trust, governance/risk/compliance, security operations, identity, and protection of data, applications, endpoints, and infrastructure. It is aimed at experienced security architects who translate business and regulatory requirements into Microsoft security capabilities such as Entra, Defender XDR, Sentinel, Defender for Cloud, and Purview. Expect scenario-based questions that ask you to choose the best-fit architecture rather than to configure a single feature.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | SC-100 |
| Credential | SC-100: Microsoft Cybersecurity Architect |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Design solutions that align with security best practices and priorities | ~27% |
| 2 | Design security operations, identity, and compliance capabilities | ~27% |
| 3 | Design security solutions for infrastructure | ~27% |
| 4 | Design security solutions for applications and data | ~18% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Design solutions that align with security best practices and priorities

- Microsoft Zero Trust is built on three guiding principles: verify explicitly (authenticate and authorize on all available signals), use least privilege access (just-in-time and just-enough-access with risk-based adaptive policies), and assume breach (segment access, minimize blast radius, and verify end-to-end encryption).
- Zero Trust is organized into six technology pillars - Identity, Endpoints, Data, Applications, Infrastructure, and Network - coordinated by cross-cutting visibility, automation, and orchestration. Identity is treated as the primary control plane.
- Microsoft Entra Conditional Access is the Zero Trust policy decision and enforcement point that implements verify explicitly, evaluating signals such as sign-in and user risk, device compliance, location, and app to enforce MFA, block, or session controls per request.
- Continuous Access Evaluation (CAE) revokes or challenges active sessions in near real time when risk or policy changes, rather than waiting for token expiry.
- The Microsoft Cybersecurity Reference Architectures (MCRA) are diagram-based guidance showing how Microsoft security capabilities integrate with each other and third-party platforms to implement Zero Trust and modernize security operations.
- The Microsoft Cloud Security Benchmark (MCSB) provides prescriptive, prioritized control baselines for Azure and multicloud, mapped to frameworks like CIS and NIST, and is surfaced in Defender for Cloud as the default compliance and secure-score baseline.

### Domain 2 - Design security operations, identity, and compliance capabilities

- Onboarding Microsoft Sentinel into the unified Microsoft Defender portal gives analysts a single synchronized incident queue that correlates Sentinel analytics-rule alerts with Defender XDR alerts across endpoints, identities, email, SaaS apps, and servers.
- A single centralized Log Analytics workspace with Sentinel enabled is the recommended design when the goal is to correlate incidents and run cross-source analytics in one place, with the Azure Monitor Agent and data collection rules routing logs from any subscription or region.
- Multiple regional workspaces satisfy data residency and sovereignty requirements because Log Analytics data stays in its workspace region; cross-workspace KQL queries still let analysts correlate across them.
- Sentinel delivers SOAR through automation rules (which define when and how automated responses trigger) and playbooks (Azure Logic Apps workflows that perform enrichment and remediation such as disabling an account or isolating a device).
- Advanced hunting uses KQL against a shared schema spanning Defender XDR tables and Sentinel workspace tables; successful hunting queries can be promoted into custom detection rules.
- A hot interactive retention tier (commonly 90 days) supports fast investigation while a lower-cost archive/long-term retention tier with search jobs or data restore satisfies multi-year compliance mandates at far lower cost.

### Domain 3 - Design security solutions for infrastructure

- Azure Private Link projects a PaaS resource into a VNet as a private endpoint NIC with a private IP; linking the matching privatelink Private DNS zone makes the service FQDN resolve privately, and disabling public network access removes internet exposure with no connection-string changes.
- Disabling public network access on a resource blocks all public-endpoint access, including from within the VNet, so only private endpoints and explicitly allowed networks can reach it - enforcing least-privilege connectivity at the resource itself.
- Virtual WAN with a Secured Virtual Hub provides Microsoft-managed transitive routing plus integrated Azure Firewall (or partner NVA); routing intent policies automatically steer internet and private traffic through the hub firewall with minimal per-hub configuration.
- Azure Firewall Premium uniquely adds TLS inspection and an intrusion detection and prevention system (IDPS) on top of FQDN and threat-intelligence filtering; a default route (0.0.0.0/0) in each spoke pointing to the firewall forces all egress through inspection.
- NSGs still handle granular Layer 3/4 segmentation while Azure Firewall handles FQDN filtering, threat-intel filtering, and centralized logging, so both are typically deployed together in a defense-in-depth design.
- Application Security Groups (ASGs) let NSG rules reference logical tiers as sources and destinations, so newly scaled VMs inherit policy by joining the ASG; combining ASGs with explicit inter-tier allows and a default deny delivers maintainable east-west segmentation.

### Domain 4 - Design security solutions for applications and data

- GitHub Advanced Security is the native shift-left toolset for GitHub repos: Dependabot flags and blocks vulnerable dependencies, CodeQL performs static analysis (SAST), and secret scanning with push protection prevents hardcoded credentials from being pushed.
- Shift-left places checks progressively earlier in the lifecycle: IDE/pre-commit, PR-time SAST and software composition analysis (SCA), build-time image scanning, staging DAST, and runtime monitoring.
- Managed identities eliminate stored credentials: a system- or user-assigned identity gets an Entra token, RBAC grants data-plane access, and a contained database user mapped to the identity lets Azure SQL authenticate it via Entra without secrets.
- User-assigned managed identities have an independent lifecycle, so they can be pre-provisioned, shared, and are revocable without being orphaned when a single app is deleted.
- OIDC workload identity federation lets a GitHub Actions or workload present a short-lived token exchanged for an Azure token at runtime; scoping the federated credential subject to specific branches or environments removes long-lived secrets and constrains who can obtain tokens.
- Azure API Management is the API gateway that centralizes concerns: validate-jwt verifies Entra tokens at the gateway, rate-limit-by-key and quota policies throttle abuse, content/size validation guards payloads, and the backend topology is abstracted from callers.

## Study tips

- SC-100 questions are scenario-driven and ask for the best design, not just a working one - weigh requirements like least privilege, no stored secrets, data residency, and no public exposure, then pick the option that satisfies all of them.
- Anchor answers to the three Zero Trust principles (verify explicitly, least privilege, assume breach) and the six pillars; when in doubt, the option that verifies identity and device and segments to limit blast radius is usually correct.
- Know when to choose a single centralized Log Analytics/Sentinel workspace (correlation and unified analytics) versus multiple regional workspaces (data residency and sovereignty), since this is a recurring decision point.
- For infrastructure questions, distinguish the tools precisely: private endpoints plus disabling public access for resource isolation, Azure Firewall Premium for TLS inspection and IDPS, Front Door WAF for global Layer 7, and Bastion for portless admin access.
- For credentials and secrets, default to managed identities and OIDC workload identity federation over stored secrets, and to Key Vault with RBAC and private endpoints for anything that must be stored.

---

Want the full breakdown? See the complete **[SC-100 study guide](https://certgrid.app/study-guide/sc-100-microsoft-cybersecurity-architect)** and **[free practice questions](https://certgrid.app/practice/sc-100-microsoft-cybersecurity-architect)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


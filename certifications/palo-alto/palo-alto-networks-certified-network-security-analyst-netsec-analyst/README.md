# Palo Alto Networks Certified Network Security Analyst (NetSec-Analyst) - Study Cheatsheet

The Palo Alto Networks Certified Network Security Analyst (NetSec-Analyst) validates that firewall administrators and security analysts can run day-to-day operations on next-generation firewalls managed through Strata Cloud Manager (SCM). It covers building reusable objects, writing and evaluating Security and NAT policy, operating SCM (configuration scope, folders, deployment, dashboards, and Strata Logging Service), and troubleshooting traffic, policy, and management issues. The exam is 90 minutes with roughly 743 items in the bank and a passing score of 700.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Palo Alto Networks Certified Network Security Analyst (NetSec-Analyst) |
| Credential | Palo Alto Networks Certified Network Security Analyst (NetSec-Analyst) |
| Level | Intermediate |
| Practice mock length | ~75 questions |
| Duration | ~90 minutes |
| Passing score | 700 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Objects | ~30% |
| 2 | Policies | ~30% |
| 3 | Strata Cloud Manager Operations | ~26% |
| 4 | Troubleshooting | ~14% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Objects

- An address object can be defined as an IP netmask, a contiguous IP range, or a fully qualified domain name (FQDN); FQDN objects fit best when a hostname is stable but its backend IP addresses change.
- A service object bundles a protocol and port (for example TCP on a specific port) once so many rules can reference it; changing the object updates every rule that uses it.
- A snippet is a reusable configuration bundle (objects and other settings) that can be attached to multiple folders; an object inside it becomes available to every folder the snippet is assigned to without duplication.
- When a more specific folder defines an object with the same name as an inherited one, the more specific object takes precedence within that folder's branch.
- Static address groups support nesting, so a group can include other address groups as members; dynamic address groups use tags to determine membership.
- File Blocking rules are evaluated top-down and the first matching rule's action is used; the alert action lets a file transfer proceed while logging it for visibility and baselining.

### Domain 2 - Policies

- Security policy is evaluated top-down on a first-match basis, and by default a rule logs the session at session end once the connection closes or times out.
- Rule shadowing occurs when a broader rule higher in the list matches first, making a more specific rule below it unreachable; the fix is usually to reorder so specific rules sit above general ones.
- Rule evaluation order across scopes is: centrally managed pre-rules first, locally created rules next, then centrally managed post-rules last.
- Zone types differ: a universal rule also matches same-zone (intrazone) traffic between its listed zones, while an interzone rule matches only sessions crossing between two different zones.
- A NAT rule's Original Packet section matches the untranslated packet on source zone, destination zone, and destination interface, while the translated address is set in the Translated Packet section.
- Source NAT types include Dynamic IP and Port (DIPP) and Dynamic IP; DIPP rewrites source IP and port so many internal hosts share one external address (typical internet access).

### Domain 3 - Strata Cloud Manager Operations

- Strata Cloud Manager (SCM) centrally manages next-generation firewalls (hardware, VM-Series, and cloud) and Prisma Access from one place, while managed firewalls still enforce policy on their own data plane.
- A firewall is onboarded to SCM either through direct cloud onboarding or through an integrated Panorama deployment; Panorama can keep managing devices on-premises while connected to SCM for shared visibility.
- Folders provide the hierarchical structure that organizes and scopes configuration; a device must be associated with a folder before it can inherit that folder's configuration.
- Configuration inheritance flows downward from parent folders to children, and a device's effective configuration is built by inheriting through every ancestor, with more specific settings overriding more general ones.
- A snippet can be attached to multiple folders at once, and the order or priority in which snippets are attached to a folder determines how their contributed rules combine.
- Before a push, confirm the correct scope, review validation results, and account for concurrent administrator activity, since overlapping edits can conflict; the pending push summary shows exactly what will change.

### Domain 4 - Troubleshooting

- Security policy uses first-match, top-down evaluation, and the entire matched rule's configuration (including its security profiles) applies, so an early permissive rule with no threat profile leaves matching traffic uninspected.
- The Action and Rule fields are the first two traffic-log fields to check when identifying why a session was blocked, and 'reset-both' means the firewall reset the connection on both the client and server sides.
- The 'aged-out' session-end reason reflects an idle-timeout expiration, not an explicit policy denial, while 'not-applicable' means the session was denied before App-ID could evaluate the application.
- test security-policy-match and test nat-policy-match simulate policy outcomes for a hypothetical flow without sending real traffic.
- show session id reveals a session's ingress and egress zones and any NAT translation applied, show session all with filter criteria limits output to matching sessions, and show arp all confirms whether a next hop's Layer 2 (MAC) address resolved.
- A decrypted session can still fail despite an allow rule when the server certificate is expired (blocked by the decryption profile) or the negotiated cipher suite is unsupported, since decryption applies its own checks.

## Study tips

- When a question describes traffic being allowed but uninspected, look for a permissive first-match rule above the intended rule; remember the whole matched rule's profile set applies and evaluation then stops.
- For NAT questions, separate the two halves of a rule: match on the Original Packet (pre-translation zones and interface) and rewrite in the Translated Packet section; recall that Static NAT bi-directional is off by default.
- Memorize the SCM rule order pre-rules, local rules, post-rules, and that inheritance flows parent-to-child with the most specific setting winning, since scope questions hinge on both.
- Know your CLI: test security-policy-match and test nat-policy-match simulate flows, while show session id, show session all, and show arp all inspect live state.
- Map log symptoms to causes: local-only logs point to a missing Log Forwarding profile, empty widgets point to scope or time-range filters, and aged-out or not-applicable are session-end reasons, not denials.

---

Want the full breakdown? See the complete **[Palo Alto Networks Certified Network Security Analyst (NetSec-Analyst) study guide](https://certgrid.app/study-guide/palo-alto-networks-certified-network-security-analyst-netsec-analyst)** and **[free practice questions](https://certgrid.app/practice/palo-alto-networks-certified-network-security-analyst-netsec-analyst)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


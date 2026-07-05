# Citrix CCP-N: Certified Professional - Networking - Study Cheatsheet

Citrix CCP-N (Certified Professional - Networking) validates advanced configuration and troubleshooting of Citrix ADC (NetScaler), covering AAA/nFactor authentication, Web App Firewall, AppExpert (content switching, rewrite, responder), integrated caching and front-end optimization, Citrix ADM/AppFlow analytics, and GSLB. It targets network engineers and administrators who already hold CCA-N and design, deploy, and operate ADC in production. The 90-minute exam has roughly 800 items in the bank, with a passing score of 660 (scaled).

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Citrix CCP-N |
| Credential | Citrix CCP-N: Certified Professional - Networking |
| Level | Advanced |
| Practice mock length | ~64 questions |
| Duration | ~90 minutes |
| Passing score | 660 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Authentication, Authorization, and Auditing (AAA-TM / nFactor) | ~16% |
| 2 | Web App Firewall (WAF) | ~17% |
| 3 | Content Switching, Rewrite, and Responder (AppExpert) | ~17% |
| 4 | Citrix ADC Optimization | ~17% |
| 5 | Citrix ADM, AppFlow, and Analytics | ~17% |
| 6 | GSLB and Advanced Traffic Management | ~17% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Authentication, Authorization, and Auditing (AAA-TM / nFactor)

- AAA-TM requires two mandatory components: a dedicated authentication (AAA) virtual server that holds the authentication policies and login schema, and a traffic-management (LB or CS) vServer that has authentication enabled and references the AAA vServer by name with the -authnVsName parameter.
- An authentication profile lets an LB/CS vServer reference a non-addressable (no IP) authentication virtual server; the profile is bound to the traffic vServer and points to the AAA vServer.
- Form-based AAA-TM authentication redirects the unauthenticated client with an HTTP 302 to the AAA login page, while 401-based authentication returns an HTTP 401 challenge so the browser shows a native credential prompt.
- On successful login the ADC creates an AAA session, issues the NSC_AAAC session cookie to the client, and redirects the user back to the originally requested (landing/return) URL stored in the session.
- The NSC_AAAC cookie is scoped to a cookie domain; two applications served under FQDNs in different cookie domains do not share the cookie, so the user must re-authenticate for each.
- A single AAA virtual server can be shared by multiple LB vServers by setting the same -authnVsName on each; for SSO across them the AAA vServer must use a configuration that supports single sign-on.

### Domain 2 - Web App Firewall (WAF)

- A WAF profile takes effect only when it is referenced by a policy and that policy is bound to a bind point (an LB or CS virtual server, or the global/default bind point); an unbound policy inspects no traffic.
- The positive security model (whitelist) permits only requests conforming to explicitly defined allowed behavior and blocks everything else; it is implemented via Start URL, Field Formats, Form Field Consistency, Cookie Consistency, and similar checks.
- The negative security model (blacklist) allows all traffic by default and blocks only requests matching known-bad patterns from the signatures database (SQL injection, XSS, command injection, etc.).
- Positive-model protection is more configuration effort but gives tighter control; negative-model blocks only known-bad and lets unknown traffic pass - a profile with positive checks but no signatures has no negative-model protection.
- WAF policies bound at the same point are evaluated in ascending priority order, so the policy with the lower priority number (e.g., priority 90 before 200) is evaluated first.
- The Start URL check enforces an allow list of URLs where a session may begin; URL Closure extends it to permit any URL that appeared as a hyperlink in a previously served, allowed page.

### Domain 3 - Content Switching, Rewrite, and Responder (AppExpert)

- Advanced (default-syntax) content switching policies bound to a CS vServer are evaluated in ascending priority-number order, and the request is sent to the target of the first policy that evaluates TRUE - the lowest-numbered matching policy wins.
- A goto priority expression on a CS policy binding can alter evaluation flow, jumping forward to a specified priority or to END to stop further evaluation.
- Bind a default LB vServer to the CS vServer using the default (no-policy) target binding so requests matching no policy still reach a backend; without a default target and no matching policy the CS vServer has no reachable destination.
- HTTP.REQ.HOSTNAME.EQ("shop.example.com") matches the Host header with a case-insensitive exact match; content switching decisions operate on the inbound request, so expressions must use HTTP.REQ.
- To switch on the Host header of TLS traffic, the CS vServer must be type SSL with server certificates bound so the ADC can terminate SSL and read the encrypted header; an HTTP-type CS vServer cannot read it.
- Common request expressions: HTTP.REQ.URL.PATH.STARTSWITH("/api/v2") matches a path prefix; HTTP.REQ.URL.QUERY.VALUE("version").EQ("2") matches a query parameter value; HTTP.REQ.HEADER("User-Agent").CONTAINS("Mobile") matches a header substring.

### Domain 4 - Citrix ADC Optimization

- Integrated Caching is gated by the platform license: the Standard edition does not include it, so an Advanced (formerly Enterprise) or Premium (formerly Platinum) license is required to store or serve cached objects.
- A content group is configured as static or dynamic: static treats a URL as a single cached object, while dynamic stores multiple variants of the same URL differentiated by selectors (hit and invalidation selectors).
- A hit selector built on parameterized expressions (e.g., HTTP.REQ.URL.QUERY or HTTP.REQ.COOKIE.VALUE("sessionid")) lets the cache store and match a separate variant per user or per query value.
- The flashCache parameter set to YES collapses a thundering-herd of simultaneous misses for the same object into one origin fetch that many waiting clients share.
- relExpiry sets freshness relative to caching time (e.g., 43200 seconds = 12 hours for catalog images); absExpiry sets an absolute clock time (e.g., 02:00) at which the object expires.
- Each content group has a maxResSize parameter capping the largest response (in KB) it will store; responses larger than this limit are passed through uncached even if otherwise eligible.

### Domain 5 - Citrix ADM, AppFlow, and Analytics

- The Citrix ADM agent is a lightweight virtual appliance deployed in a remote datacenter or cloud to act as a proxy between the ADM server and managed ADC instances, establishing one secure outbound channel back to ADM.
- Each managed instance is associated with the agent that has network reachability to the instance's NSIP/management IP; that agent polls inventory and analytics and applies configuration jobs and StyleBook deployments.
- Instance discovery can be automatic by scanning a configured IP range and can integrate with public-cloud auto-scale group APIs so new ADC instances are added to inventory without manual steps.
- Configuration jobs push CLI commands to many instances at once and support variable substitution from a CSV file (e.g., a unique VIP per instance); jobs can be saved as reusable templates and scheduled.
- Job scheduling supports one-time future runs or recurring runs by frequency/day/time (e.g., weekly Sunday 02:00); the execution summary records per-instance success/failure and offers a retry on failed devices action.
- StyleBooks are declarative configuration templates; common building blocks are defined once and referenced by many StyleBooks for reusable, modular configuration, and a StyleBook configuration pack represents a deployed application instance.

### Domain 6 - GSLB and Advanced Traffic Management

- In GSLB the ADC acts as the authoritative DNS name server (ADNS) for the GSLB domain; when a client's local DNS resolver queries that domain, the ADC applies its GSLB method and returns an A or AAAA record for the chosen site.
- Sub-domain delegation needs an NS record in the parent zone delegating the GSLB sub-domain to the ADC plus an ADNS service on the ADC's SNIP listening on UDP/TCP port 53.
- Metric Exchange Protocol (MEP) is the proprietary protocol between GSLB sites that shares site/network metrics, remote GSLB service UP/DOWN state, and persistence information; it runs over TCP 3011 (or TCP 3009 when secured with SSL).
- A GSLB site is defined as LOCAL (the ADC being configured) or REMOTE (a partner datacenter), and includes the Site IP used for MEP communication.
- GSLB object hierarchy: GSLB services (representing the LB/CS vServers at each site) are bound to a GSLB virtual server, which is associated with the GSLB domain and applies the configured load-balancing method.
- Defining a GSLB service requires associating it with a previously created GSLB site (LOCAL or REMOTE) and specifying the IP address and port of the actual LB/CS vServer it represents.

## Study tips

- Memorize the AAA-TM wiring: a traffic vServer references the authentication vServer via -authnVsName (or an authentication profile for a non-addressable AAA vServer). Many questions hinge on whether a component is bound or merely created.
- For WAF questions, internalize positive vs negative model and the safe rollout order (Log + Learning, review, relax, then Block). Remember a policy must be bound to a bind point to inspect any traffic.
- Drill the advanced policy expression syntax (HTTP.REQ.HOSTNAME, URL.PATH.STARTSWITH, URL.QUERY.VALUE, HEADER, GET(n)) and the rule that the lowest-numbered matching policy wins on a CS vServer.
- Know the license editions that gate features (Integrated Caching and FEO need Advanced or Premium, not Standard) and the difference between static and dynamic content groups with selectors.
- For GSLB, lock in the port numbers (ADNS on 53, MEP on 3011/3010), the LOCAL vs REMOTE site model, and which proximity method maps to geo-IP (Static) versus RTT (Dynamic).

---

Want the full breakdown? See the complete **[Citrix CCP-N study guide](https://certgrid.app/study-guide/citrix-ccp-n-certified-professional-networking)** and **[free practice questions](https://certgrid.app/practice/citrix-ccp-n-certified-professional-networking)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


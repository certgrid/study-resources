# Citrix CCA-N: Certified Associate - Networking - Study Cheatsheet

The Citrix CCA-N (Certified Associate - Networking) validates your ability to deploy, configure, and manage Citrix ADC (NetScaler) for traffic management, load balancing, SSL offload, and secure remote access through Citrix Gateway. It targets network and systems administrators who handle day-to-day ADC operations, and the 90-minute exam draws from six domains with roughly equal weighting. Expect scenario questions on initial setup, virtual-server configuration, SSL termination, ICA-proxy gateways, and management-plane hardening.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Citrix CCA-N |
| Credential | Citrix CCA-N: Certified Associate - Networking |
| Level | Associate |
| Practice mock length | ~64 questions |
| Duration | ~90 minutes |
| Passing score | 610 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Citrix ADC Architecture and Fundamentals | ~17% |
| 2 | Citrix ADC Platform and Setup | ~17% |
| 3 | Load Balancing | ~17% |
| 4 | SSL/TLS Offload | ~17% |
| 5 | Citrix Gateway and Secure Access | ~17% |
| 6 | Citrix ADC Security and Management | ~17% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Citrix ADC Architecture and Fundamentals

- The nCore (multi-core) architecture runs the packet engine across multiple CPU cores in parallel, using a shared-memory model with distributed locking to coordinate cores and scale throughput.
- A load balancing virtual server is the logical entity that owns a VIP, receives client traffic, and distributes it across bound services or service groups.
- A service represents one back-end application instance (server IP/name + protocol + port) that is bound to a load balancing virtual server.
- The two primary benefits of load balancing on the ADC are improving availability across multiple back-end servers and offloading SSL/TLS decryption from those servers.
- Least Connection is the default load balancing method: each new request goes to the bound service currently handling the fewest active connections.
- GSLB (Global Server Load Balancing) distributes client traffic across servers in multiple geographic sites or data centers.

### Domain 2 - Citrix ADC Platform and Setup

- A factory-default ADC ships with NSIP 192.168.100.1 and mask 255.255.0.0; you connect a workstation on the 192.168.x.x network to reach the first-time setup utility.
- The NSIP is the single management IP used for GUI, SSH/CLI, SNMP, and HA communication; every ADC has exactly one NSIP and changing it requires a warm reboot to take full effect.
- Initial configuration captures the NSIP/mask/default gateway, a DNS name server, the host name, time zone, and license upload to establish basic reachability.
- Running 'save ns config' writes the running configuration to ns.conf so it persists across reboots; if config is lost after reboot, it was never saved.
- Configuring an NTP server keeps the clock synchronized, which is essential for accurate log timestamps, SSL certificate date-range validation, license enforcement, and HA consistency.
- Disabling HTTP management access while leaving HTTPS enabled forces all GUI administration over encrypted TLS, protecting admin credentials in transit (a standard hardening step).

### Domain 3 - Load Balancing

- A load balancing virtual server is defined by a virtual IP address (VIP), a protocol, and a listening port; the ADC owns the VIP and publishes it in DNS.
- A service group bundles many identical back-end servers (same protocol/settings) into one logical entity bound to the vserver as a unit, so 40 servers can be managed together.
- A monitor bound at the service group level is automatically inherited by every member, eliminating per-server monitor configuration; members can be added by IP or named server object.
- A load balancing virtual server is DOWN when no services or service groups are bound to it; it comes UP once at least one bound service is UP.
- When no method is configured, the ADC uses Least Connection by default; assign a higher weight to a more powerful server so it receives proportionally more traffic.
- When a single service group member fails, only that member is marked DOWN; the virtual server stays UP and simply avoids the failed member.

### Domain 4 - SSL/TLS Offload

- SSL offload terminates the client TLS session at the ADC and forwards decrypted traffic to back-end servers as plain HTTP, freeing servers from cryptographic work (often hardware-accelerated on MPX).
- Standard SSL offload uses an SSL-type load balancing virtual server bound to HTTP-type services; the encryption boundary exists only between client and ADC.
- SSL offload with end-to-end encryption uses an SSL vserver to terminate the client session and SSL-type back-end services so the ADC re-encrypts traffic to the servers.
- SSL pass-through forwards encrypted traffic untouched (no termination), whereas SSL offload terminates and decrypts the session on the ADC.
- An SSL virtual server requires a valid certificate-key pair to be bound; without one the vserver is marked DOWN even when all back-end services are UP.
- You import a certificate and its matching private key, then create a certificate-key pair object; that pair is the unit bound to an SSL vserver or service.

### Domain 5 - Citrix Gateway and Secure Access

- Basic mode (ICA proxy) is the lightweight Gateway mode that proxies HDX/ICA traffic between Workspace app clients and VDAs through StoreFront, without endpoint analysis or full VPN tunneling.
- A Citrix Gateway virtual server is SSL-based and needs a server certificate whose subject or SAN matches the external FQDN users type, or clients receive certificate errors.
- The Secure Ticket Authority (STA) issues the session ticket that authorizes the Gateway to proxy the HDX connection to the VDA; the STA list must match identically on the Gateway and the StoreFront Gateway object.
- The session profile (bound via a session policy) holds StoreFront integration settings: Web Interface Address, Single Sign-on Domain, Account Services Address, and ICA-proxy mode.
- Setting the Single Sign-on Domain (matching the users' AD domain) in the session profile enables SSO to StoreFront Receiver for Web.
- Multiple session policies/profiles let you apply different settings based on connection type, such as Workspace app versus a web browser.

### Domain 6 - Citrix ADC Security and Management

- Simple ACLs are stateless packet filters evaluated very early in the pipeline (matching source IP, protocol, destination port) and support a TTL after which they are automatically removed.
- Extended ACLs are stateless Layer 3/4 filters evaluated by priority; they are staged when created and only enforced after you run 'apply ns acls', which also flushes matching connections.
- Management-plane access is restricted by combining the Management Access (restrictAccess) setting with extended ACLs that permit the trusted subnet (e.g., 10.20.0.0/16) and deny all others to the NSIP.
- Rate limiting uses a limit identifier (threshold, interval, mode such as REQUEST_RATE) plus a stream selector keying on an attribute like CLIENT.IP.SRC or HTTP.REQ.URL, evaluated by a responder policy using SYS.CHECK_LIMIT.
- A stream selector defines the expressions that group and count traffic; keying on the request URL throttles only requests to that URL rather than all client traffic.
- Responder generates a reply or redirect directly from the appliance (e.g., respond-with a custom 429 when SYS.CHECK_LIMIT is exceeded), while Rewrite modifies the request or response in flight and forwards it.

## Study tips

- Memorize the factory defaults that show up repeatedly: NSIP 192.168.100.1 / 255.255.0.0, Least Connection as the default LB method, and that an SSL vserver without a bound cert-key pair is DOWN even when services are UP.
- Know the difference pairs cold: USNIP vs USIP, simple vs extended ACLs (TTL and auto-removal vs priority and 'apply ns acls'), SSL offload vs SSL pass-through vs end-to-end, and Responder (reply/redirect) vs Rewrite (modify in flight).
- For Gateway/ICA-proxy scenarios, trace the flow: certificate FQDN match, STA list identical on Gateway and StoreFront, session profile holding SSO domain and Web Interface Address, and the VDA hosting the actual HDX session.
- Remember the actions that need a follow-up step: changing the NSIP needs a warm reboot, 'save ns config' is required for persistence across reboots, extended ACLs need 'apply ns acls', and many features must be explicitly enabled before they work.
- When a question describes a symptom, reason about state: a DOWN vserver with no bound services, an incomplete cert chain from an unlinked intermediate CA, or an unreachable server because no SNIP exists in its subnet are recurring root causes.

---

Want the full breakdown? See the complete **[Citrix CCA-N study guide](https://certgrid.app/study-guide/citrix-cca-n-certified-associate-networking)** and **[free practice questions](https://certgrid.app/practice/citrix-cca-n-certified-associate-networking)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


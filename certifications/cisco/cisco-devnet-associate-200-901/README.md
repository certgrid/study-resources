# Cisco DevNet Associate (200-901) - Study Cheatsheet

The Cisco DevNet Associate (200-901) exam validates foundational software development and automation skills for Cisco platforms, covering APIs, Python, network automation, application deployment, and core networking. It is aimed at developers, network engineers, and DevOps staff beginning to build and automate against Cisco infrastructure. The 120-minute exam has roughly 90-110 questions, a passing score around 825/1000, and spans six weighted domains.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Cisco DevNet Associate (200-901) |
| Credential | Cisco DevNet Associate (200-901) |
| Level | Associate |
| Practice mock length | ~100 questions |
| Duration | ~120 minutes |
| Passing score | 825 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Software Development and Design | ~16% |
| 2 | Understanding and Using APIs | ~23% |
| 3 | Cisco Platforms and Development | ~16% |
| 4 | Application Deployment and Security | ~16% |
| 5 | Infrastructure and Automation | ~22% |
| 6 | Network Fundamentals | ~7% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Software Development and Design

- Git is a distributed version control system: every clone holds the full history, enabling offline commits, branching, and merging without a central server being reachable.
- The basic Git save flow is git add <file> to stage changes, then git commit -m "msg" to record them; git status and git diff inspect the working tree against the last commit.
- git checkout -b feature creates and switches to a new branch in one command; git merge (or git rebase) integrates one branch's changes into another.
- git checkout -- file.txt discards local uncommitted changes and restores the file from the last commit; git reset --soft HEAD~1 undoes the last commit but keeps its changes staged.
- JSON is the dominant lightweight, human-readable data-interchange format for REST payloads and config; YAML and XML are common alternatives.
- In Python, json.dumps(data) serializes a dict to a JSON string and json.loads(text) parses a JSON string back into a dict.

### Domain 2 - Understanding and Using APIs

- REST is an architectural style using stateless HTTP requests against resource URIs; GET reads a resource, POST creates, PUT fully replaces, PATCH partially updates, and DELETE removes.
- GET is safe and idempotent (no side effects); PUT and DELETE are idempotent; POST is neither safe nor idempotent.
- HTTP status classes: 2xx success (200 OK, 201 Created), 3xx redirection (304 Not Modified), 4xx client errors (400, 401, 404), 5xx server errors (500, 503).
- 401 Unauthorized means authentication is missing or failed and includes a WWW-Authenticate header; 403 Forbidden means the request was authenticated but not permitted.
- Common API auth schemes are API keys (a static token identifying the caller) and OAuth 2.0 bearer tokens (time-limited access tokens sent as Authorization: Bearer <token>).
- REST is client-initiated request/response; a webhook is server-initiated - the server pushes an HTTP callback to a registered URL when an event occurs, eliminating the need to poll.

### Domain 3 - Cisco Platforms and Development

- Cisco Catalyst Center (formerly DNA Center) exposes intent-based networking REST APIs for discovery, provisioning, path tracing, policy, and assurance; calls require an X-Auth-Token header and Content-Type: application/json.
- Catalyst Center auth tokens should be cached and reused until they expire, then refreshed, rather than generating a new token on every call.
- Cisco Meraki Dashboard API v1 base URL is https://api.meraki.com/api/v1 and uses the X-Cisco-Meraki-API-Key header for authentication.
- Cisco Webex APIs provide messaging, meetings, and calling integration; developers build bots, manage rooms and memberships, send adaptive cards, and subscribe to webhooks for real-time events.
- Cisco Secure Firewall Management Center (FMC) APIs automate access-control rules, NAT, and security policy; Cisco Umbrella and SecureX/XDR APIs cover DNS-layer security and threat orchestration.
- YANG (RFC 6020) is the data-modeling language that defines the structure of configuration and state data; it is consumed by both NETCONF and RESTCONF.

### Domain 4 - Application Deployment and Security

- Containers (Docker) package an app with its dependencies and runtime into one portable image, so the same artifact runs consistently across dev, test, and prod.
- A Dockerfile defines how an image is built; docker build -t myapp:1.0 . builds and tags an image from the current directory's Dockerfile.
- docker run -p 8080:80 web maps host port 8080 to container port 80; CMD ["python","app.py"] sets the default process a container runs at startup.
- Inspect running containers with docker logs <id> for stdout/stderr and docker exec -it <id> sh to open an interactive shell inside the container.
- Multi-stage builds with a minimal base image (such as alpine or distroless) most reduce final image size, and Docker layer/build-cache reuse skips rebuilding unchanged layers.
- Serverless / Function as a Service (AWS Lambda, Azure Functions, Google Cloud Functions) runs code on events and scales to zero when idle, minimizing cost for bursty workloads.

### Domain 5 - Infrastructure and Automation

- NETCONF over SSH (port 830) with YANG models provides transactional configuration (candidate datastore, commit, lock, rollback), making it suited to reliable programmatic network changes.
- RESTCONF gives a RESTful HTTP/JSON interface to the same YANG-modeled data using standard verbs, easier for developers already comfortable with REST.
- Ansible is agentless (no software on managed nodes), connects over SSH, and defines tasks in YAML playbooks; nothing needs to be installed on the network device.
- An Ansible play uses hosts: to target devices from an inventory; ansible-playbook -i hosts.ini site.yml runs a playbook against that inventory.
- cisco.ios.ios_config sends configuration to Cisco IOS/IOS XE devices; vendor collections like cisco.ios, cisco.nxos, and cisco.iosxr supply the platform modules.
- Ansible modules should be idempotent: re-running a playbook converges to the desired state and makes no change when the device already matches.

### Domain 6 - Network Fundamentals

- TCP is a connection-oriented, reliable Layer 4 protocol using a three-way handshake (SYN, SYN-ACK, ACK), sequence numbers, and acknowledgments for ordered, error-checked delivery.
- UDP is connectionless with only an 8-byte header and no retransmission or ordering, making it ideal for latency-sensitive, loss-tolerant traffic like real-time voice, video, and streaming.
- A switch operates at Layer 2, forwarding Ethernet frames by destination MAC using its CAM table; a router operates at Layer 3, forwarding packets by IP address between networks.
- The default gateway is the next-hop router a host uses to reach destinations outside its own subnet; without it, off-subnet traffic cannot be delivered.
- RFC 1918 private ranges are 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16; NAT translates these to public IPv4 to conserve address space and shield internal hosts.
- A /26 mask is 255.255.255.192, giving 64 addresses per subnet (62 usable); hosts .50 and .70 fall in different /26 subnets (0-63 vs 64-127) and require a router to communicate.

## Study tips

- Memorize HTTP methods and status codes cold (GET/POST/PUT/PATCH/DELETE; 200, 201, 400, 401, 403, 404, 429, 500) - they appear throughout the API and Cisco-platform domains.
- Be able to read and write basic Python with the requests library and json module, plus interpret short Ansible YAML playbooks and small Git command sequences; the exam shows real code and CLI snippets.
- Know which Cisco platform owns which task: Catalyst Center for campus intent-based networking, Meraki for cloud-managed, FMC/Umbrella/SecureX for security, Webex for collaboration, and ACI/APIC for data center.
- Distinguish NETCONF (SSH, port 830, XML, transactional datastores) from RESTCONF (HTTPS, REST verbs, JSON/XML) and remember both are driven by YANG models.
- Use the free Cisco DevNet Sandboxes and Learning Labs to make real API calls and run NETCONF/RESTCONF and Ansible - hands-on practice cements the concepts far better than reading alone.

---

Want the full breakdown? See the complete **[Cisco DevNet Associate (200-901) study guide](https://certgrid.app/study-guide/cisco-devnet-associate-200-901)** and **[free practice questions](https://certgrid.app/practice/cisco-devnet-associate-200-901)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


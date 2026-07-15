# HashiCorp Consul Associate (003) - Study Cheatsheet

The HashiCorp Consul Associate (003) exam validates that you can use Consul for service networking - service discovery, health checking, the key/value store, service mesh (Connect), and core security. It is a 60-minute, multiple-choice exam aimed at developers, operators, and architects who deploy and operate Consul in production and want to prove foundational competence.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | HashiCorp Consul Associate (003) |
| Credential | HashiCorp Consul Associate (003) |
| Level | Associate |
| Practice mock length | ~57 questions |
| Duration | ~60 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Consul Architecture | ~22% |
| 2 | Service Discovery | ~17% |
| 3 | Consul KV and Configuration | ~17% |
| 4 | Service Mesh and Security | ~24% |
| 5 | Security and Architecture | ~20% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Consul Architecture

- Consul is a single binary that runs as an agent in one of two modes: server (participates in Raft consensus and stores cluster state) or client (lightweight, registers local services, runs health checks, and forwards RPCs/queries to servers).
- Server quorum should be an odd number of voting servers - typically 3 (tolerates 1 failure) or 5 (tolerates 2 failures) - so Raft can elect a leader and commit writes without split-brain.
- Losing quorum (e.g. 2 of 3 servers down) means Consul cannot elect a leader or commit writes; reads of stale data may still work but no new writes are accepted.
- Raft uses a single leader; all writes go to the leader, are replicated to a majority quorum, and must be durably fsync'd to disk before being acknowledged - so disk I/O latency directly limits write throughput.
- Adding more voting servers increases write latency because every commit must be replicated to and acknowledged by a larger quorum.
- Consul uses the Serf gossip protocol for membership and failure detection: a LAN gossip pool within a datacenter and a WAN gossip pool between federated datacenters.

### Domain 2 - Service Discovery

- Services are registered with Consul via a service definition file (HCL/JSON in the agent config directory), the HTTP API (/v1/agent/service/register), or consul services register web.hcl.
- By default Consul's DNS interface listens on port 8600; query <service>.service.consul to get addresses of healthy instances and <service>.service.consul SRV for host+port.
- Only passing (healthy) instances are returned in discovery results by default; an instance that fails its health check is excluded until it passes again.
- Consul supports multiple check types: HTTP, TCP, gRPC, script, Docker, and TTL checks where the application must periodically report passing or be marked critical.
- deregister_critical_service_after automatically removes a service that has been in the critical state for a configured duration, cleaning up dead instances from the catalog.
- The HTTP health endpoint /v1/health/service/<name>?passing returns only healthy instances; without ?passing it returns all instances with their check status.

### Domain 3 - Consul KV and Configuration

- The Consul KV store holds dynamic configuration, feature flags, and coordination data, letting apps update behavior centrally without redeploying.
- Write a key with consul kv put app/maintenance true and read it with consul kv get app/maintenance; the API path is /v1/kv/<key>.
- consul kv get -recurse app/ returns all keys and values under a prefix in one call; consul kv delete -recurse app/ removes the whole subtree.
- Use a hierarchical key namespace (e.g. app/env/setting) so ACL tokens can be scoped to specific prefixes for least-privilege access.
- Check-And-Set (CAS) writes use the key's ModifyIndex: consul kv put -cas -modify-index=<n> key value succeeds only if the key has not changed, giving optimistic concurrency.
- Consul sessions plus KV CAS enable distributed locks and leader election (a session acquires a key, and the lock releases if the session or its TTL expires).

### Domain 4 - Service Mesh and Security

- Consul service mesh (Connect) provides automatic mutual TLS (mTLS) and service-to-service authorization without requiring changes to application code.
- Each service runs a sidecar proxy (Envoy is the supported proxy) that transparently establishes mTLS and enforces authorization, keeping the application unaware of mesh security.
- Intentions define which services are allowed (or denied) to communicate; create one with consul intention create web db to permit web to call db.
- Set a default-deny posture so services cannot talk to each other unless an intention explicitly allows it (zero-trust networking), independent of network topology.
- Connect issues a short-lived leaf (identity) certificate to each service from a CA; the built-in CA is the default, and Vault can be configured as the Connect CA provider for production.
- Longer leaf-certificate lifetimes are signed and rotated less frequently, reducing CA signing load and proxy churn (at the cost of slower credential rotation).

### Domain 5 - Security and Architecture

- Consul ACLs provide token-based access control over resources (services, KV, nodes, sessions); enable them with acl { enabled = true, default_policy = "deny" } for least privilege.
- With default_policy = deny, all access is denied unless a token grants it via attached policies (allowlist model); default_policy = allow is permissive and not recommended for production.
- The bootstrap (initial management) token is created once with consul acl bootstrap; it is a global management token with unrestricted privileges, so guard and rotate it carefully.
- An ACL token has a SecretID (the bearer credential sent in X-Consul-Token requests) and an AccessorID (a non-secret identifier used for logging, auditing, and token management).
- Create least-privilege tokens by attaching policies, e.g. consul acl token create -policy-name=web-read; assign separate agent, service, and session tokens scoped to what each needs.
- Auth methods (e.g. Kubernetes, JWT/OIDC) let workloads obtain dynamic, short-lived tokens automatically instead of hand-managing static tokens.

## Study tips

- Memorize the quorum/fault-tolerance table: 3 servers tolerate 1 failure, 5 tolerate 2; always use an odd number of voting servers and know that more servers means higher write latency.
- Be fluent in the core CLI verbs and their flags - consul kv get/put -recurse and -cas, consul services register/deregister, consul intention create, consul acl token create, consul snapshot save, and consul operator raft list-peers.
- Distinguish the three security layers and what each protects: gossip encryption (Serf membership traffic), TLS/mTLS (RPC control plane and service mesh data plane), and ACLs (authorization over resources).
- Know default behaviors and ports: DNS on 8600, only healthy instances returned by default, ACL default_policy deny vs allow, stale reads enabled for DNS, and blocking queries driven by X-Consul-Index.
- Read scenario questions carefully for the failure mode being described (lost quorum, critical health check, default-deny intention blocking traffic, expired session releasing a lock) and pick the answer that matches Consul's documented default.

---

Want the full breakdown? See the complete **[HashiCorp Consul Associate (003) study guide](https://certgrid.app/study-guide/hashicorp-consul-associate-003)** and **[free practice questions](https://certgrid.app/practice/hashicorp-consul-associate-003)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


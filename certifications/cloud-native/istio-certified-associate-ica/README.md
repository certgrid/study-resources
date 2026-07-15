# Istio Certified Associate (ICA) - Study Cheatsheet

The Istio Certified Associate (ICA) validates working knowledge of the Istio service mesh: its control-plane/data-plane architecture, traffic management, security (mTLS and authorization), and observability. It is a 90-minute, performance- and knowledge-based exam aimed at platform engineers, SREs, and developers who configure and operate Istio on Kubernetes. A scaled score of 750 is required to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Istio Certified Associate (ICA) |
| Credential | Istio Certified Associate (ICA) |
| Level | Associate |
| Practice mock length | ~60 questions |
| Duration | ~90 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Istio Architecture | ~27% |
| 2 | Traffic Management | ~28% |
| 3 | Security | ~23% |
| 4 | Observability | ~22% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Istio Architecture

- Istio splits into a data plane (Envoy proxies that intercept and move all workload traffic) and a control plane (istiod, which handles service discovery, configuration distribution, and certificate issuance).
- istiod is a single consolidated binary that merged the older Pilot, Citadel, and Galley components into one control-plane process.
- Envoy sidecars intercept pod traffic transparently using iptables rules set up by an init container (istio-init) or the Istio CNI plugin, requiring no application code changes.
- Sidecar injection is enabled by labeling a namespace with istio-injection=enabled (or with istio.io/rev=<revision> for revision-based installs); a mutating admission webhook then injects the proxy at pod creation.
- Existing pods do not get a sidecar retroactively. After labeling a namespace you must restart or redeploy the pods (e.g. kubectl rollout restart) so the webhook fires.
- istioctl kube-inject -f deploy.yaml | kubectl apply -f - performs manual injection without relying on the namespace label / webhook.

### Domain 2 - Traffic Management

- A VirtualService defines how requests are routed to a service (host matching, weighted splits, header/URI matches, retries, timeouts, fault injection, mirroring); a DestinationRule defines policies applied after routing (subsets, load balancing, connection pools, outlier detection, TLS).
- Subsets are declared in a DestinationRule under spec.subsets, each with a name and labels (e.g. version: v1); a VirtualService route then targets destination.host plus destination.subset.
- Weighted/canary routing is done with http.route[] entries each carrying a weight value (e.g. 90 to v1, 10 to v2); weights across a route must sum to 100.
- Header-based routing uses http.match[].headers (e.g. end-user.exact: tester). Match rules are evaluated top to bottom, so put specific matches (like the header route to v2) before the catch-all weighted default.
- Retries are configured with http.retries: { attempts, perTryTimeout, retryOn } (e.g. attempts: 3, perTryTimeout: 2s, retryOn: "5xx,connect-failure").
- Timeouts are set per-route with http.timeout; this is the overall request timeout, distinct from a retry's perTryTimeout.

### Domain 3 - Security

- Istio assigns each workload a SPIFFE identity derived from its Kubernetes service account, formatted as spiffe://<trust-domain>/ns/<namespace>/sa/<serviceaccount> (e.g. cluster.local/ns/foo/sa/bar).
- istiod issues short-lived X.509 certificates that the istio-agent in each pod automatically rotates, so there is no manual certificate management.
- Mutual TLS encrypts and mutually authenticates service-to-service traffic between sidecars; it is configured with a PeerAuthentication resource.
- PeerAuthentication mTLS modes: STRICT (only mTLS accepted), PERMISSIVE (accepts both plaintext and mTLS - the default, used during migration), and DISABLE.
- A mesh-wide STRICT policy is a PeerAuthentication in the root namespace (istio-system) with no selector and mtls.mode: STRICT; it can be overridden by namespace- or workload-scoped policies.
- During migration keep PERMISSIVE so non-injected/legacy clients keep working, then tighten to STRICT once every client is in the mesh; you can override specific legacy namespaces back to PERMISSIVE.

### Domain 4 - Observability

- Istio gives you the three observability signals out of the box without app instrumentation: metrics, distributed traces, and access logs, all emitted by the Envoy sidecars.
- Standard Istio request metrics (istio_requests_total, istio_request_duration_milliseconds, request size/response codes) are exposed by the proxies and scraped by Prometheus.
- The common observability add-on stack is Prometheus and Grafana for metrics, Jaeger or Zipkin for traces, and Kiali for the mesh topology graph.
- Kiali renders the service-graph topology with traffic health, request rates, and security (mTLS) status badges on each edge.
- Kiali derives its mTLS/security badges from Istio metrics in Prometheus (e.g. the connection_security_policy label); if those metrics or the Prometheus integration are missing, badges show as Unknown.
- Istio does NOT generate end-to-end traces by itself - applications must propagate the trace-context headers (B3 headers or W3C traceparent) from inbound to outbound requests, or traces break into disconnected single-hop spans.

## Study tips

- The exam is hands-on and command-heavy: practice istioctl (install, kube-inject, analyze, proxy-config, proxy-status, x describe) and kubectl until applying and debugging YAML is muscle memory under time pressure.
- Memorize which resource owns which job: VirtualService = routing/retries/timeouts/fault/mirror; DestinationRule = subsets/load-balancing/connection-pools/outlier-detection; Gateway = edge ports/TLS; ServiceEntry = external hosts.
- Know the security pairing cold: PeerAuthentication controls mTLS mode (STRICT/PERMISSIVE/DISABLE), RequestAuthentication validates JWTs, and AuthorizationPolicy enforces allow/deny on identities and request attributes.
- When a trace is broken or incomplete, suspect missing application-level propagation of B3/traceparent headers before blaming Istio config; sampling is head-based and propagated downstream.
- Use istioctl analyze to catch misconfigurations and istioctl proxy-status to spot proxies that are STALE/out of sync with istiod - these are fast wins for the troubleshooting questions.

---

Want the full breakdown? See the complete **[Istio Certified Associate (ICA) study guide](https://certgrid.app/study-guide/istio-certified-associate-ica)** and **[free practice questions](https://certgrid.app/practice/istio-certified-associate-ica)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


# KCNA: Kubernetes and Cloud Native Associate - Study Cheatsheet

The Kubernetes and Cloud Native Associate (KCNA) is an entry-level, multiple-choice exam from the CNCF that validates foundational knowledge of Kubernetes and the broader cloud native ecosystem. It covers core Kubernetes architecture, container orchestration, cloud native design principles, observability, and application delivery. It is aimed at engineers, students, and IT staff who are new to cloud native and want a credential before pursuing hands-on certifications like the CKA or CKAD.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | KCNA |
| Credential | KCNA: Kubernetes and Cloud Native Associate |
| Level | Associate |
| Practice mock length | ~60 questions |
| Duration | ~90 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Kubernetes Fundamentals | ~21% |
| 2 | Container Orchestration | ~20% |
| 3 | Cloud Native Architecture | ~22% |
| 4 | Cloud Native Observability | ~21% |
| 5 | Cloud Native Application Delivery | ~17% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Kubernetes Fundamentals

- A Pod is the smallest deployable unit in Kubernetes; Kubernetes manages Pods, not individual containers, and containers in a Pod share the same network namespace (IP) and can share storage volumes.
- etcd is a distributed, highly available key-value store that holds all cluster state - every Deployment, Service, ConfigMap, Secret, and other object is persisted there.
- The kube-apiserver is the front end of the control plane and the single entry point all users and components use to read and write cluster state.
- The kube-scheduler watches for newly created Pods with no assigned node and selects a node based on resource requests, taints/tolerations, affinity, and other constraints.
- The kube-controller-manager runs reconciliation control loops (e.g., the Deployment, ReplicaSet, and Node controllers) that drive actual state toward the declared desired state.
- The kubelet is the per-node agent that reads PodSpecs from the API server and ensures the described containers are running and healthy on that node.

### Domain 2 - Container Orchestration

- The Container Network Interface (CNI) is a CNCF spec defining a plugin interface for pod networking; the kubelet calls the CNI plugin to set up a Pod's network namespace and assign its IP.
- The Container Storage Interface (CSI) is a gRPC-based standard letting third-party storage vendors integrate with Kubernetes (dynamic provisioning, attach, mount, delete) without changing core code.
- A Service gives a stable network identity - a ClusterIP virtual IP and DNS name - and load-balances traffic across the Pods selected by its label selector (a plain key/value map under spec.selector).
- kube-proxy runs on each node, watches Service and EndpointSlice changes, and programs iptables or IPVS rules to forward Service traffic to backing Pods.
- Service types: ClusterIP (internal only, default), NodePort (exposes a port on every node), and LoadBalancer (provisions an external cloud load balancer); 'kubectl expose' creates a Service.
- An Ingress defines host/path-based HTTP/HTTPS routing into cluster Services but does nothing without a running ingress controller (e.g., NGINX) to fulfill its rules.

### Domain 3 - Cloud Native Architecture

- The CNCF (Cloud Native Computing Foundation) is a Linux Foundation project that hosts cloud native projects (Kubernetes, Prometheus, Envoy) and tracks them through Sandbox, Incubating, and Graduated maturity levels.
- The Open Container Initiative (OCI) standardizes the container image format and runtime behavior so images built by any tool (Docker, Podman, Buildah) run on any compliant runtime.
- A container image is an immutable, packaged artifact bundling an application with its dependencies; a container registry (e.g., Docker Hub, Harbor) stores and distributes those images.
- Cloud native principles include declarative APIs with desired-state reconciliation and immutable infrastructure (replace components rather than modifying them in place).
- The HorizontalPodAutoscaler (HPA) adjusts a workload's replica count based on observed metrics such as CPU utilization, memory, or custom metrics, against a configured target.
- The Cluster Autoscaler adds nodes when Pods cannot be scheduled due to insufficient capacity and removes underutilized nodes, scaling the cluster size to match demand.

### Domain 4 - Cloud Native Observability

- The three pillars of observability are logs (discrete timestamped events), metrics (numeric time series like request rate and latency), and traces (the path of a request across services).
- Prometheus is the CNCF de facto standard for metrics; it uses a pull model, scraping the /metrics HTTP endpoint of each target and storing time-series data queried with PromQL.
- A Prometheus time series is uniquely identified by its metric name together with its set of key/value labels; its local storage is not designed for long-term, highly available retention without remote write.
- OpenTelemetry (OTel) is a vendor-neutral CNCF project (merging OpenCensus and OpenTracing) providing APIs, SDKs, and a collector to generate and export traces, metrics, and logs to backends like Jaeger or Prometheus.
- Jaeger is a distributed tracing backend used to visualize how a request flows across services; tracing relies on context propagation between services.
- A liveness probe detects an unrecoverable state (e.g., deadlock); on failure the kubelet kills and restarts the container per the Pod's restartPolicy.

### Domain 5 - Cloud Native Application Delivery

- Helm is the Kubernetes package manager; a chart bundles templated manifests with metadata and a default values file, and charts are versioned, installable, upgradable, and rollback-able.
- Helm commands: 'helm install <name> ./chart' to install, 'helm upgrade --install <name> ./chart' to install-or-upgrade idempotently, and 'helm rollback <name> <revision>' to revert a release.
- Kustomize is a template-free customization tool (built into kubectl) that uses a kustomization.yaml to layer overlays and strategic-merge/JSON patches over base manifests per environment.
- GitOps treats Git as the single source of truth for desired state, and a reconciling agent continuously syncs the live cluster to match the repo, providing audit trails and pull-request-based changes.
- Argo CD and Flux are the leading CNCF GitOps continuous-delivery tools; if someone changes the cluster manually, the agent reverts it back to the state declared in Git.
- RollingUpdate is the default Deployment strategy: it incrementally replaces old Pods with new ones, gated by maxSurge (extra Pods allowed) and maxUnavailable (Pods that can be down) for little or no downtime.

## Study tips

- KCNA is multiple choice with no hands-on tasks, but you should still recognize what common kubectl, helm, and probe configurations do - study commands and their effects, not just definitions.
- Memorize the control-plane components (kube-apiserver, etcd, kube-scheduler, kube-controller-manager) versus node components (kubelet, kube-proxy, container runtime) and exactly what each one does.
- Know the CNCF project landscape and what each tool is for: Prometheus (metrics), Jaeger/OpenTelemetry (tracing), Argo CD/Flux (GitOps), Helm (packaging), Envoy/Istio/Linkerd (service mesh), KEDA/Knative (event-driven/serverless).
- Be precise about the three health probes: liveness restarts a container, readiness removes it from Service endpoints without restarting, and startup gates the other two during slow boots.
- Watch for cloud native principles wording - declarative desired-state reconciliation, immutable infrastructure, and standard interfaces (CRI, CNI, CSI, OCI) are recurring exam themes.

---

Want the full breakdown? See the complete **[KCNA study guide](https://certgrid.app/study-guide/kcna-kubernetes-and-cloud-native-associate)** and **[free practice questions](https://certgrid.app/practice/kcna-kubernetes-and-cloud-native-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


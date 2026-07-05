# CKS: Certified Kubernetes Security Specialist - Study Cheatsheet

The Certified Kubernetes Security Specialist (CKS) is a hands-on, performance-based exam that validates your ability to secure container-based applications and Kubernetes platforms across build, deployment, and runtime. It assumes you already hold a valid CKA and is aimed at platform engineers, SREs, and security practitioners who harden clusters, lock down workloads, secure the supply chain, and monitor for threats. You get 120 minutes to solve live tasks on real clusters and must score at least 67%.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CKS |
| Credential | CKS: Certified Kubernetes Security Specialist |
| Level | Intermediate |
| Practice mock length | ~16 questions |
| Duration | ~120 minutes |
| Passing score | 670 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Cluster Setup | ~14% |
| 2 | Cluster Hardening | ~17% |
| 3 | System Hardening | ~16% |
| 4 | Minimize Microservice Vulnerabilities | ~20% |
| 5 | Supply Chain Security | ~15% |
| 6 | Monitoring, Logging and Runtime Security | ~18% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Cluster Setup

- kube-bench checks a cluster against the CIS Kubernetes Benchmark; run 'kube-bench run --targets master' on a control-plane node and '--targets node' on workers to scope the checks.
- An empty podSelector ({}) selects all pods in a namespace; a policy with policyTypes:[Ingress] and no ingress rules denies all inbound, and one with policyTypes:[Egress] and no egress rules denies all outbound, forming a default-deny baseline.
- NetworkPolicies are only enforced if the CNI supports them (Calico, Cilium, Weave); plain flannel ignores them, so applying a policy with an unsupported CNI silently allows all traffic.
- To block pod access to the cloud metadata endpoint, write an egress policy whose allowed destinations exclude 169.254.169.254/32, e.g. ipBlock cidr 0.0.0.0/0 with except [169.254.169.254/32].
- On kubeadm clusters the kube-apiserver runs as a static pod in /etc/kubernetes/manifests/; editing that manifest makes the kubelet automatically recreate the pod, so no restart command is needed.
- Encryption at rest is configured by an EncryptionConfiguration manifest (providers like aescbc, secretbox, or kms) referenced via --encryption-provider-config; after enabling it you must re-write existing Secrets (kubectl get secrets -A -o json | kubectl replace -f -) to encrypt them.

### Domain 2 - Cluster Hardening

- Set automountServiceAccountToken:false on a pod or ServiceAccount when the workload does not call the API, removing the token at /var/run/secrets/kubernetes.io/serviceaccount and shrinking attack surface.
- Patch the default SA to stop mounting tokens with: kubectl patch serviceaccount default -p '{"automountServiceAccountToken":false}'.
- Use Roles (namespace-scoped) not ClusterRoles for least privilege: 'kubectl create role pod-reader --verb=get,list --resource=pods -n web' then 'kubectl create rolebinding ... --role=pod-reader --user=dev -n web'.
- Test effective permissions with 'kubectl auth can-i', impersonating with --as; a ServiceAccount is referenced as system:serviceaccount:<namespace>:<name>, and 'kubectl auth can-i --list --as=...' enumerates everything a subject can do.
- RBAC enforces privilege-escalation prevention: you can only create or update a role with permissions you already hold, unless you have the special 'escalate' verb; binding a role you don't hold requires the 'bind' verb, so granting 'bind' on a powerful role enables escalation.
- The system:masters group and binding the cluster-admin ClusterRole to broad subjects grants full cluster control; remove such bindings and grant scoped least-privilege roles instead.

### Domain 3 - System Hardening

- In Kubernetes 1.30+, AppArmor is set via securityContext.appArmorProfile with type:Localhost and localhostProfile:<name> for a node-loaded profile; the older container.apparmor.security.beta.kubernetes.io annotation is deprecated.
- Set seccompProfile.type:RuntimeDefault to apply the container runtime's built-in syscall filter; type:Localhost with localhostProfile points to a custom profile, and type:Unconfined disables filtering.
- Custom localhost seccomp profiles live under the kubelet seccomp root (default /var/lib/kubelet/seccomp), so a file at /var/lib/kubelet/seccomp/profiles/myprofile.json is referenced as localhostProfile:profiles/myprofile.json.
- A seccomp profile uses defaultAction:SCMP_ACT_ERRNO to deny by default, then an allowlist of syscalls with action SCMP_ACT_ALLOW; this is the default-deny pattern the exam expects.
- Use a RuntimeClass with handler:runsc and set spec.runtimeClassName on a pod to run it under gVisor (sandboxed runtime) for stronger isolation of untrusted or multi-tenant workloads.
- Drop all Linux capabilities and add back only what is required, e.g. capabilities:{drop:[ALL], add:[NET_BIND_SERVICE]}; NET_BIND_SERVICE is the single cap needed to bind ports below 1024.

### Domain 4 - Minimize Microservice Vulnerabilities

- Enforce the restricted Pod Security Standard on a namespace with the label: kubectl label ns prod pod-security.kubernetes.io/enforce=restricted; the modes are enforce, audit, and warn.
- Pod Security Admission is configured purely by namespace labels of the form pod-security.kubernetes.io/<mode>=<level> where level is privileged, baseline, or restricted; baseline disallows hostPath and privileged, restricted additionally requires runAsNonRoot and a non-Unconfined seccomp profile.
- Prefer mounting secrets as files over environment variables, because env vars can leak via child processes, crash dumps, and 'kubectl describe', whereas file mounts can be permissioned and are less exposed.
- Mount Secret volumes readOnly:true with a restrictive defaultMode such as 0400, and enable encryption at rest so the secret is protected in etcd and on disk.
- Use a service mesh (Istio, Linkerd) with sidecar proxies to enforce mTLS between pods without changing application code; in Istio a PeerAuthentication with mtls.mode:STRICT in the namespace requires mutual TLS.
- OPA Gatekeeper uses a two-object pattern: a ConstraintTemplate defines the Rego policy and generates a CRD, and a Constraint instance scopes and enforces it against matching resources.

### Domain 5 - Supply Chain Security

- Scan a container image and fail CI on findings with: trivy image --severity HIGH,CRITICAL --exit-code 1 myreg/app:1.0; trivy fs --severity HIGH,CRITICAL . scans a filesystem or source tree.
- Pin images by immutable digest (myreg/app@sha256:<digest>) so a repointed tag cannot silently swap in malicious content; combine with minimal/distroless or scratch base images and multi-stage builds.
- Restrict pods to approved registries with an admission policy (OPA Gatekeeper, Kyverno, or the built-in ImagePolicyWebhook) that rejects image references not starting with the allowed registry prefix, e.g. requiring registry.internal/ and denying docker.io/*.
- The built-in ImagePolicyWebhook admission plugin is configured via --admission-control-config-file and calls an external service to allow or deny images at admission time.
- cosign signs images for provenance: 'cosign sign --key cosign.key myreg/app@sha256:<digest>' to sign and 'cosign verify --key cosign.pub' to verify; enforce verification at admission with a Kyverno verifyImages rule or the sigstore policy-controller.
- Keyless signing uses 'cosign sign' with an OIDC identity backed by Fulcio (short-lived certs) and Rekor (transparency log), avoiding long-lived signing keys.

### Domain 6 - Monitoring, Logging and Runtime Security

- Audit logging requires both a policy and a backend: set --audit-policy-file=/etc/kubernetes/audit/policy.yaml and --audit-log-path=/var/log/kubernetes/audit.log on the apiserver static pod; without the policy file no events are recorded.
- Kubernetes audit levels are None, Metadata, Request, and RequestResponse; RequestResponse is the most verbose, capturing event metadata plus the full request and response bodies.
- Audit Policy rules are evaluated top-down and the first matching rule wins, so put a specific rule (e.g. level:RequestResponse for resources:secrets) before any catch-all Metadata rule.
- Scope an audit rule to Secrets in one namespace with resources:[{group:'', resources:['secrets']}] and namespaces:['prod'] to capture caller, verb, and timestamp for those access events.
- Set omitStages:['RequestReceived'] at the top of the Policy to skip the noisy initial stage and only log events at later stages.
- Control audit log rotation and retention with --audit-log-maxage (days to keep), --audit-log-maxbackup (number of files), and --audit-log-maxsize (MB per file).

## Study tips

- Set up a kubectl alias and context-switching habit early; the exam spans multiple clusters and you must run 'kubectl config use-context <name>' before each task or you will edit the wrong cluster.
- Bookmark the allowed docs (kubernetes.io, Falco, Trivy, gVisor, Kyverno, AppArmor) and practice navigating them fast; you cannot memorize every YAML field but you can find it quickly.
- On kubeadm clusters, edit static pod manifests in /etc/kubernetes/manifests/ and wait for the kubelet to recreate the apiserver pod; verify with 'kubectl get pod -n kube-system' or 'crictl ps' instead of trying to restart it manually.
- Always read the task's target namespace and cluster carefully, and after applying NetworkPolicies remember to allow DNS egress on port 53 or you will break the workload you were asked to secure.
- Manage your 120 minutes by weight: flag and skip a stubborn task, finish the higher-count domains (Cluster Hardening, Microservice Vulnerabilities, System Hardening) first, and return to skipped items at the end.

---

Want the full breakdown? See the complete **[CKS study guide](https://certgrid.app/study-guide/cks-certified-kubernetes-security-specialist)** and **[free practice questions](https://certgrid.app/practice/cks-certified-kubernetes-security-specialist)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


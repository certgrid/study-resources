# KCSA: Kubernetes and Cloud Native Security Associate - Study Cheatsheet

The Kubernetes and Cloud Native Security Associate (KCSA) is a 90-minute, multiple-choice exam validating foundational knowledge of securing Kubernetes clusters and cloud native workloads. It covers the 4Cs model, control-plane component hardening, security fundamentals (RBAC, Secrets, NetworkPolicies, Pod Security), threat modeling, platform security tooling, and compliance frameworks. It is aimed at developers, platform engineers, and security practitioners who are new to cloud native security and want to demonstrate baseline competence.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | KCSA |
| Credential | KCSA: Kubernetes and Cloud Native Security Associate |
| Level | Associate |
| Practice mock length | ~60 questions |
| Duration | ~90 minutes |
| Passing score | 750 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Overview of Cloud Native Security | ~11% |
| 2 | Kubernetes Cluster Component Security | ~22% |
| 3 | Kubernetes Security Fundamentals | ~25% |
| 4 | Kubernetes Threat Model | ~16% |
| 5 | Platform Security | ~19% |
| 6 | Compliance and Security Frameworks | ~8% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Overview of Cloud Native Security

- The 4Cs of Cloud Native Security are Cloud, Cluster, Container, and Code - layered outermost to innermost, where each layer secures the layer inside it.
- Cloud is the outermost layer; if the cloud account or IAM is compromised, all inner layers (Cluster, Container, Code) inherit the exposure.
- A strong Cloud layer cannot compensate for weak Cluster, Container, or Code layers - every layer must be secured independently.
- Defense in depth means applying multiple independent layers of security so a single control failure or bypass does not lead to full compromise.
- Shift-left security moves checks earlier in the lifecycle (code review, build, CI) so vulnerabilities and misconfigurations are caught before reaching production, when remediation is cheap.
- Shift-left CI practices include SAST scanning, dependency/SCA checking, IaC scanning, and container image scanning during pull requests.

### Domain 2 - Kubernetes Cluster Component Security

- The kube-apiserver and etcd are the two highest-priority control-plane components to secure, because compromising either yields broad control over the entire cluster.
- etcd is the sole persistent store for all cluster state including Secrets; its compromise (or a stolen backup) exposes the whole cluster.
- By default Secrets are stored in etcd base64-encoded, not encrypted; enable encryption at rest via the kube-apiserver --encryption-provider-config flag (AES-CBC, AES-GCM, or a KMS provider).
- etcd should be reachable only by the API server, secured with mutual TLS (--client-cert-auth=true, --trusted-ca-file, --cert-file, --key-file), with no direct workload access.
- The kube-apiserver is the central policy enforcement point: every request passes through authentication, then authorization (RBAC), then admission control.
- Set --anonymous-auth=false so unauthenticated requests are rejected rather than mapped to the system:anonymous identity.

### Domain 3 - Kubernetes Security Fundamentals

- RBAC is the primary authorization mechanism; follow least privilege by granting only the verbs (get, list, create, delete) on only the resources a subject genuinely needs.
- Test effective permissions with kubectl auth can-i, e.g. kubectl auth can-i --list --as=system:serviceaccount:web:app-sa or kubectl auth can-i create deployments --as=dev@corp -n web.
- Bind a ClusterRole to a ServiceAccount in a namespace with a RoleBinding, e.g. kubectl create rolebinding deployer-view --clusterrole=view --serviceaccount=ci:deployer -n ci.
- The Pod Security Standards define exactly three levels: privileged (no restrictions), baseline (blocks known escalation vectors like hostNetwork, hostPID, privileged), and restricted (strongest, enforces non-root and dropped capabilities).
- Enforce a Pod Security Standard per namespace with a label, e.g. kubectl label ns payments pod-security.kubernetes.io/enforce=restricted.
- A default-deny NetworkPolicy uses an empty podSelector {} with a policyType but no rules: spec: { podSelector: {}, policyTypes: [Ingress] } drops all ingress until a more specific policy allows it.

### Domain 4 - Kubernetes Threat Model

- STRIDE is a threat-modeling methodology categorizing threats as Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, and Elevation of Privilege.
- Repudiation threats involve destroying or polluting logs to undermine the ability to attribute actions; tamper-resistant audit logs counter this.
- A supply-chain attack targets how software is built and delivered - pulling a tampered image (embedded malware, backdoored dependencies, known CVEs) introduces attacker code directly into running workloads.
- Two of the most common Kubernetes attack vectors are supply-chain compromise via malicious images and exposed, unauthenticated management interfaces (dashboard or API endpoint).
- privileged: true drops nearly all capability restrictions and grants host-level access, making container escape and node compromise trivial.
- Mounting the container runtime socket (/run/containerd/containerd.sock or /var/run/docker.sock) into a pod lets it create arbitrary privileged containers - a direct escape-to-node path.

### Domain 5 - Platform Security

- Linux namespaces (pid, net, mnt, ipc, uts, user) isolate each container's view of processes, network, filesystem, and IPC; cgroups enforce CPU, memory, and I/O limits.
- Seccomp uses a BPF filter to restrict which system calls a container's processes may make, limiting what an attacker can do even after compromising the application.
- The restricted Pod Security Standard requires a seccomp profile of RuntimeDefault or Localhost; Unconfined is disallowed and admission rejects such pods.
- Apply a custom seccomp profile with seccompProfile: { type: Localhost, localhostProfile: profiles/audit.json }; RuntimeDefault is the recommended preventive baseline.
- Image scanning tools (Trivy, Grype, Snyk) compare image-layer packages against CVE databases (NVD, OSV, vendor advisories); scan at build time, push time, and continuously in the registry.
- Fail a CI build on serious findings, e.g. trivy image --severity HIGH,CRITICAL --exit-code 1 myrepo/app:1.0.

### Domain 6 - Compliance and Security Frameworks

- The CIS Kubernetes Benchmark is a community-consensus set of prescriptive, testable hardening recommendations covering API server flags, etcd, kubelet, RBAC, network policies, and pod security.
- kube-bench is an open-source Aqua Security tool that automates CIS Kubernetes Benchmark checks and produces a pass/fail report with remediation guidance.
- Run kube-bench as a scheduled cluster Job and in CI/CD, exporting results to a centralized dashboard for trend tracking; deploy it with kubectl apply -f the project's job.yaml.
- On managed clusters (EKS, GKE, AKS), control-plane checks may not apply because the provider hides those components; focus on node/worker and policy checks you actually control.
- Compliance frameworks like PCI DSS (cardholder data), HIPAA (health data), and SOC 2 (service orgs) mandate specific controls and require auditable evidence they operate effectively.
- API server audit logging records the authenticated principal, verb, resource, namespace, source IP, timestamp, and outcome, providing a non-repudiation trail for accountability and investigations.

## Study tips

- Memorize the 4Cs in order (Cloud, Cluster, Container, Code) and remember each layer secures the one inside it - many questions hinge on placing a control at the correct layer.
- Know the three Pod Security Standards levels (privileged, baseline, restricted) and exactly what restricted enforces: non-root, drop ALL capabilities, no privilege escalation, and a RuntimeDefault/Localhost seccomp profile.
- Be able to read kube-apiserver and kubelet flags at a glance: --anonymous-auth=false, --authorization-mode=Webhook, --encryption-provider-config, --audit-policy-file, and NodeRestriction.
- Recognize the classic escape vectors (privileged: true, runtime socket mount, hostPath, hostNetwork reaching metadata service) and the STRIDE category each threat maps to.
- Distinguish tools by purpose: kube-bench (CIS benchmark), Trivy/Grype (image scanning + SBOM), Cosign (signature verification at admission), Falco (runtime detection), Kyverno/Gatekeeper (policy-as-code).

---

Want the full breakdown? See the complete **[KCSA study guide](https://certgrid.app/study-guide/kcsa-kubernetes-and-cloud-native-security-associate)** and **[free practice questions](https://certgrid.app/practice/kcsa-kubernetes-and-cloud-native-security-associate)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


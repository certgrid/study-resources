# CKAD: Certified Kubernetes Application Developer - Study Cheatsheet

The Certified Kubernetes Application Developer (CKAD) exam validates your ability to design, build, configure, expose, deploy, observe, and maintain cloud-native applications on Kubernetes. It is a 2-hour, hands-on, performance-based test taken in a live cluster from the command line, aimed at developers and engineers who package and run applications on Kubernetes rather than administer the cluster itself. You need 66% to pass, and speed with kubectl plus comfort editing YAML are essential.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CKAD |
| Credential | CKAD: Certified Kubernetes Application Developer |
| Level | Intermediate |
| Practice mock length | ~19 questions |
| Duration | ~120 minutes |
| Passing score | 660 out of 1000 |
| Notes reviewed | 2026-07-12 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Application Design and Build | ~21% |
| 2 | Application Deployment | ~21% |
| 3 | Application Observability and Maintenance | ~16% |
| 4 | Application Environment, Configuration and Security | ~26% |
| 5 | Services and Networking | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Application Design and Build

- A Job uses spec.completions to set how many successful pod completions are required and spec.parallelism to cap how many pods run concurrently; completions: 5 with parallelism: 2 runs until 5 succeed while never exceeding 2 at once.
- spec.completionMode: Indexed (paired with completions) gives each pod a unique completion index via the JOB_COMPLETION_INDEX env var, useful for partitioning work; the default is NonIndexed.
- A CronJob's --schedule uses the standard 5-field cron syntax (minute hour day-of-month month day-of-week); '*/5 * * * *' means every 5 minutes.
- spec.concurrencyPolicy on a CronJob controls overlap: Allow (default) permits concurrent runs, Forbid skips a new run if the prior Job is still active, and Replace cancels the running Job and starts a new one.
- spec.startingDeadlineSeconds on a CronJob limits how late a missed scheduled run may still start; if the controller cannot start within that window the run is skipped and counted as missed.
- Init containers run sequentially to completion before any app container starts, making them the right place to gate startup on an external dependency (e.g. a loop running 'until nslookup db; do sleep 2; done').

### Domain 2 - Application Deployment

- kubectl rollout undo deployment/web with no --to-revision reverts to the immediately previous revision; add --to-revision=N to roll back to a specific historical revision.
- In a RollingUpdate, maxUnavailable caps how many pods may be down and maxSurge caps how many extra pods may be created; with 10 replicas, maxUnavailable: 2 keeps at least 8 available and maxSurge: 2 allows at most 12 total during the update.
- strategy.type: Recreate terminates all existing pods before creating any new ones, causing downtime; RollingUpdate (the default) replaces pods gradually with no downtime.
- kubectl set image deployment/web app=myreg/app:v2 updates a named container's image in place and triggers a new rollout and revision.
- kubectl rollout status deployment/web watches and blocks until the rollout completes or fails, returning non-zero on failure, making it ideal for scripting and diagnosis.
- A rollout is marked failed after spec.progressDeadlineSeconds (default 600s) of no progress, surfacing condition Progressing=False with reason ProgressDeadlineExceeded.

### Domain 3 - Application Observability and Maintenance

- A startupProbe protects slow-starting containers: while it runs, the kubelet disables the liveness and readiness probes, so set periodSeconds x failureThreshold to cover the expected warm-up (e.g. ~45s) before liveness can kill the container.
- A livenessProbe restarts the container on failure; a readinessProbe only removes the pod from Service endpoints on failure without restarting it; a startupProbe gates the other two during startup.
- Probe handlers come in three forms: httpGet (path/port), exec (command, success on exit 0, e.g. cat /tmp/healthy), and tcpSocket (connection succeeds, e.g. port 5432).
- failureThreshold (consecutive failures before acting) and periodSeconds (interval between checks) together set how long a probe tolerates failure before restarting or de-registering the pod.
- kubectl logs <pod> --previous (or -p) retrieves logs from the previously terminated container instance, which is essential for diagnosing CrashLoopBackOff.
- kubectl logs web -c app -f streams a specific container's logs in a multi-container pod; -c is required when the pod has more than one container and no default-container annotation; --since=5m and --timestamps narrow and label output.

### Domain 4 - Application Environment, Configuration and Security

- envFrom with configMapRef (or secretRef) imports every key in the source as environment variables; valueFrom.configMapKeyRef (or secretKeyRef) with name and key selects a single entry, and an explicit env value overrides envFrom for the same key.
- kubectl create secret generic db --from-literal=password=s3cr3t creates a Secret; in a manifest, data values must be base64-encoded while stringData accepts plain text that the API server encodes for you.
- kubectl create configmap appcfg --from-file=app.conf builds a ConfigMap from a file; setting immutable: true on a ConfigMap or Secret blocks updates and improves performance but requires recreation to change.
- A configMap volume with an items list projects only the selected keys to chosen relative paths; use volumeMount.subPath (e.g. subPath: nginx.conf with mountPath: /etc/nginx/nginx.conf) to mount a single file without hiding the rest of the directory.
- A projected volume can combine configMap, secret, and downwardAPI sources under one mount; the Downward API via valueFrom.fieldRef also exposes pod metadata (name, namespace, labels, IP) as environment variables.
- securityContext.runAsUser: 1000 forces a non-root UID and allowPrivilegeEscalation: false blocks gaining extra privileges; with runAsNonRoot: true the kubelet refuses to start a container whose image would run as root, erroring 'container has runAsNonRoot and image will run as root'.

### Domain 5 - Services and Networking

- kubectl expose deployment web --port=80 --target-port=8080 creates a Service where --port is the ClusterIP listening port and --target-port is the pod port traffic is forwarded to; type defaults to ClusterIP.
- Service types: ClusterIP (internal virtual IP, default), NodePort (a port in 30000-32767 on every node, reachable at http://<node-IP>:<nodePort>), LoadBalancer (provisions an external LB), and ExternalName (a CNAME alias to spec.externalName like db.corp.local with no proxying).
- CoreDNS gives every Service the FQDN <service>.<namespace>.svc.<cluster-domain>; a Service 'db' in namespace 'data' resolves to db.data.svc.cluster.local, with 'svc' always following the namespace.
- A headless Service (clusterIP: None) creates a DNS A record per ready pod instead of one virtual IP; used as a StatefulSet's serviceName it yields stable names like <pod>.<service>.<namespace>.svc.cluster.local.
- A Service with no selector plus a manually created Endpoints/EndpointSlice object lets you route to fixed external IPs and ports; a Service whose selector does not match any Ready pod labels has empty endpoints and refuses connections.
- When a Service exposes multiple ports, each entry in spec.ports must have a unique name; targetPort can reference a named container port (e.g. targetPort: http) instead of a number.

## Study tips

- Set up your shell first: alias k=kubectl, export do='--dry-run=client -o yaml', and learn export now='--force --grace-period=0' so you can scaffold manifests fast and delete pods instantly.
- Generate YAML imperatively instead of writing from scratch: 'k run', 'k create', and 'k expose' with $do produce a skeleton you edit, which is far faster than memorizing full manifests.
- Always confirm and switch context with 'kubectl config use-context' and use the right namespace (-n) for every task; many questions live in non-default namespaces and points are lost for acting in the wrong one.
- Use 'kubectl explain <resource>.<field> --recursive' to recall exact field paths and spelling during the exam since you cannot rely on memory under time pressure, and bookmark the official kubernetes.io docs allowed in the browser.
- Budget your time: skip and flag hard questions, do high-weight Configuration and Security and Networking items confidently, and verify each answer with 'kubectl get', 'describe', and 'logs' before moving on.

---

Want the full breakdown? See the complete **[CKAD study guide](https://certgrid.app/study-guide/ckad-certified-kubernetes-application-developer)** and **[free practice questions](https://certgrid.app/practice/ckad-certified-kubernetes-application-developer)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


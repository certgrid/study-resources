# CKA: Certified Kubernetes Administrator - Study Cheatsheet

The Certified Kubernetes Administrator (CKA) is a hands-on, performance-based exam from the Cloud Native Computing Foundation that validates your ability to install, configure, and operate production Kubernetes clusters. You solve real tasks in live clusters from a terminal within 120 minutes, so command fluency and kubectl speed matter as much as conceptual knowledge. It is aimed at administrators, DevOps and platform engineers, and SREs who manage Kubernetes day to day.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | CKA |
| Credential | CKA: Certified Kubernetes Administrator |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 660 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Cluster Architecture Installation and Configuration | ~22% |
| 2 | Workloads and Scheduling | ~21% |
| 3 | Services and Networking | ~19% |
| 4 | Storage | ~19% |
| 5 | Troubleshooting | ~20% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Cluster Architecture Installation and Configuration

- The control plane consists of kube-apiserver (the REST front end and single source of truth), kube-scheduler (assigns Pods to nodes), kube-controller-manager (runs built-in controller loops), and etcd (the backing store); cloud-controller-manager is optional for cloud integrations.
- etcd is the sole backing store for all cluster state; back it up with 'etcdctl snapshot save <path>' and restore with 'etcdctl snapshot restore', supplying --cacert, --cert, and --key plus ETCDCTL_API=3 when TLS is enabled.
- kubeadm init bootstraps a control plane: it generates PKI certs and kubeconfigs, writes static Pod manifests to /etc/kubernetes/manifests/, sets up RBAC, and deploys the kube-proxy and CoreDNS add-ons.
- After kubeadm init, copy /etc/kubernetes/admin.conf to $HOME/.kube/config and run 'chown $(id -u):$(id -g) $HOME/.kube/config' so a non-root user can run kubectl.
- kubeadm runs etcd and the control plane components as static Pods; the kubelet watches /etc/kubernetes/manifests/ and manages them directly without the API server, so editing a manifest there restarts that component.
- Worker nodes join with 'kubeadm join' using a bootstrap token plus the CA cert hash (--discovery-token-ca-cert-hash sha256:...); regenerate an expired token with 'kubeadm token create --print-join-command'.

### Domain 2 - Workloads and Scheduling

- A Deployment manages a ReplicaSet and Pod template for stateless workloads; create one imperatively with 'kubectl create deployment web-app --image=nginx:1.25 --replicas=3'.
- Deployment strategies are RollingUpdate (default, controlled by maxSurge and maxUnavailable) and Recreate (terminates all old Pods before creating new ones); update an image with 'kubectl set image deployment/frontend nginx=nginx:1.25'.
- 'kubectl rollout undo deployment/<name>' rolls back to the previous revision; view history with 'kubectl rollout history' and roll back to a specific one with --to-revision.
- resources.requests sets the guaranteed minimum CPU and memory the scheduler uses for placement; resources.limits caps usage; a Pod with all containers having equal requests and limits is QoS class Guaranteed.
- Probe types are livenessProbe (restarts a stuck container), readinessProbe (removes a Pod from Service endpoints when failing), and startupProbe (protects slow-starting containers from premature liveness restarts).
- Taints (kubectl taint) repel Pods from nodes; effects are NoSchedule (block new Pods), PreferNoSchedule (soft), and NoExecute (block new and evict existing Pods lacking a matching toleration, honoring optional tolerationSeconds).

### Domain 3 - Services and Networking

- Service types are ClusterIP (default, internal-only virtual IP), NodePort (static port 30000-32767 on every node, built on a ClusterIP), LoadBalancer (provisions an external cloud LB on top of NodePort), and ExternalName (CNAME alias).
- A NodePort forwards traffic from <NodeIP>:<port> to backend Pods regardless of which node runs them; create a ClusterIP imperatively with 'kubectl create service clusterip my-svc --tcp=80:8080' (port 80, targetPort 8080).
- CoreDNS (the default DNS since Kubernetes 1.13, configured by the 'coredns' ConfigMap in kube-system) resolves Services as <service>.<namespace>.svc.cluster.local; same-namespace Pods can use just the service name.
- A headless Service sets spec.clusterIP: None; DNS then returns the individual Pod IPs instead of a single virtual IP, which is how StatefulSets get stable per-Pod DNS records.
- kube-proxy runs on every node and programs the network rules (iptables or IPVS mode) that forward Service virtual-IP traffic to healthy backend Pods.
- An Ingress defines HTTP/HTTPS host- and path-based routing and TLS termination but does nothing on its own; you must deploy an Ingress controller (NGINX, Traefik, HAProxy) because Kubernetes ships none by default.

### Domain 4 - Storage

- A PersistentVolume (PV) is a cluster-scoped piece of storage; a PersistentVolumeClaim (PVC) is a namespace-scoped request that binds to a matching PV by size, access mode, and storageClassName.
- Access modes are ReadWriteOnce (RWO, read-write by one node), ReadOnlyMany (ROX, read-only by many nodes), ReadWriteMany (RWX, read-write by many nodes), and ReadWriteOncePod (RWOP, exactly one Pod).
- Reclaim policies are Retain (keep the PV and data; it goes Released and needs manual cleanup before reuse) and Delete (remove the PV and underlying storage when the PVC is deleted); Recycle is deprecated.
- A StorageClass defines dynamic provisioning: it names a provisioner (a CSI driver or cloud plugin), parameters such as disk type, a reclaimPolicy, and a volumeBindingMode; mark one default with the storageclass.kubernetes.io/is-default-class annotation.
- A PVC referencing a storageClassName that has no provisioner and no matching pre-created PV stays Pending indefinitely until the StorageClass is added or an admin creates a satisfying PV.
- volumeBindingMode: WaitForFirstConsumer delays PV provisioning and binding until a Pod that uses the PVC is scheduled, so the volume is created in the right zone or node.

### Domain 5 - Troubleshooting

- CrashLoopBackOff means a container repeatedly starts then exits, and the kubelet applies an exponential back-off (capped at five minutes) before each restart; inspect with 'kubectl logs <pod> --previous' to see the crashed container's output.
- ImagePullBackOff and ErrImagePull mean the kubelet could not pull the image, so the container never started; causes include a wrong image name or tag, a missing or incorrect imagePullSecret for a private registry, or registry network problems.
- A Pod stuck Pending usually means the scheduler found no node that fits its resource requests, or a taint blocks it, or an unbound PVC is referenced; run 'kubectl describe pod <name>' and read the Events section.
- The scheduler fits Pods using requests (not limits); if a Pod's CPU or memory request exceeds the allocatable capacity of every node, it stays Pending until capacity frees up or the request is lowered.
- Use 'kubectl logs <pod> -c <container>' to read a specific container's stdout/stderr in a multi-container Pod; add --previous for a crashed instance and -f to follow.
- 'kubectl exec -it <pod> -- /bin/sh' opens an interactive shell in a running container for live debugging; for distroless containers use 'kubectl debug' with an ephemeral container instead.

## Study tips

- The exam is hands-on in live clusters, not multiple choice; practice solving tasks end to end in a real terminal and budget your 120 minutes across roughly 15-20 tasks, skipping high-effort low-weight ones first.
- Set up speed aliases and context immediately: 'alias k=kubectl', enable kubectl autocompletion, and always run 'kubectl config use-context <ctx>' at the start of each task since each question may target a different cluster.
- Lean on imperative commands and 'kubectl create ... --dry-run=client -o yaml > file.yaml' to scaffold manifests fast, then edit; memorize 'kubectl explain <resource>.<field>' to recall spec structure without leaving the terminal.
- The official Kubernetes documentation (kubernetes.io/docs) is allowed during the exam in one extra browser tab; practice navigating it quickly and bookmark nothing you cannot find by search, since only the permitted domains are open.
- Always verify your work after each task with get, describe, and logs, and confirm Pods reach Running/Ready; a task that looks done but leaves a Pod Pending or a Service with no endpoints earns no points.

---

Want the full breakdown? See the complete **[CKA study guide](https://certgrid.app/study-guide/cka-certified-kubernetes-administrator)** and **[free practice questions](https://certgrid.app/practice/cka-certified-kubernetes-administrator)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


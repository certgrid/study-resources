# RETIRED - Docker Certified Associate (DCA) - Study Cheatsheet

The Docker Certified Associate (DCA) validates real-world expertise operating Docker in production, spanning Swarm orchestration, image creation and registry management, engine installation and configuration, container networking, security hardening, and persistent storage. It is aimed at engineers, SREs, and DevOps practitioners with roughly 6-12 months of hands-on Docker experience. The 90-minute exam has multiple-choice and multiple-select questions, with a passing score around 65%.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | RETIRED - Docker Certified Associate (DCA) |
| Credential | RETIRED - Docker Certified Associate (DCA) |
| Level | Associate |
| Practice mock length | ~55 questions |
| Duration | ~90 minutes |
| Passing score | 650 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Orchestration | ~21% |
| 2 | Image Creation, Management, and Registry | ~21% |
| 3 | Installation and Configuration | ~16% |
| 4 | Networking | ~16% |
| 5 | Security | ~13% |
| 6 | Storage and Volumes | ~12% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Orchestration

- docker swarm init configures the current node as the first manager, generates the Raft cluster, and prints both manager and worker join tokens; retrieve them later with docker swarm join-token worker or docker swarm join-token manager.
- Swarm uses the Raft consensus protocol, requiring a quorum of (N/2)+1 managers; a 5-manager cluster tolerates loss of 2, a 3-manager cluster tolerates loss of 1. Always run an odd number of managers (3 or 5) and spread them across availability zones.
- In a network partition, only the side holding a quorum majority can commit writes (scheduling, scaling); the minority partition becomes read-only until quorum is restored.
- docker stack deploy -c docker-compose.yml mystack deploys a multi-service stack from a Compose file, applying deploy-key settings such as replicas, placement, and update_config.
- docker service scale web=5 and docker service update --replicas 5 web both set a replicated service to 5 tasks; replicated mode runs a fixed count, while global mode runs exactly one task on every matching node (ideal for monitoring/logging agents).
- When a node goes down, its tasks are rescheduled onto other available nodes and no new tasks are assigned to the failed node; Swarm reconciles desired vs actual state continuously.

### Domain 2 - Image Creation, Management, and Registry

- Multi-stage builds use multiple FROM statements; each FROM starts a fresh filesystem, and COPY --from=<stage> pulls only needed artifacts into the runtime stage, shrinking final image size by leaving build tooling behind.
- Only instructions that change the filesystem create layers: RUN, COPY, and ADD produce layers; ENV, LABEL, EXPOSE, CMD, ENTRYPOINT, and WORKDIR add metadata without a new filesystem layer.
- ENTRYPOINT in exec form (JSON array) defines the fixed executable and cannot be overridden by docker run arguments; CMD supplies default arguments that ARE overridable, and when both exist CMD values are appended as arguments to ENTRYPOINT.
- Exec form (CMD ["nginx", "-g"]) runs the binary directly as PID 1; shell form (CMD nginx -g) wraps it in /bin/sh -c, which can swallow signals and break graceful shutdown.
- COPY only moves local build-context files; ADD additionally fetches remote URLs and auto-extracts local tar archives. Best practice is to prefer COPY unless you specifically need ADD's extraction.
- Order Dockerfile instructions for cache efficiency: copy the dependency manifest (package.json, requirements.txt, go.mod) and install dependencies BEFORE copying the rest of the source so code changes do not bust the dependency layer.

### Domain 3 - Installation and Configuration

- The Docker daemon is configured via /etc/docker/daemon.json; common keys include storage-driver, data-root, dns, hosts, and log-driver. The daemon must be restarted (sudo systemctl restart docker) for changes to take effect.
- overlay2 is the recommended and default storage driver on modern kernels; others include devicemapper, btrfs, and zfs. After an engine upgrade, keep daemon.json pinned to the same storage driver used before to avoid losing existing images and containers.
- Set the default storage location with the data-root option (for example {"data-root": "/data/docker"}); the legacy graph key is deprecated. Isolating /var/lib/docker on its own partition/disk is a best practice.
- Configure persistent container DNS by setting the dns key in /etc/docker/daemon.json (for example {"dns": ["8.8.8.8"]}).
- Bind the daemon API to a TCP socket via the hosts key (for example {"hosts": ["unix:///var/run/docker.sock", "tcp://0.0.0.0:2376"]}); port 2376 is the conventional TLS-secured port. Note hosts in daemon.json can conflict with systemd's -H flag.
- Secure remote daemon access with TLS using three files: the CA certificate (ca.pem), server certificate (server-cert.pem), and server key (server-key.pem), with matching client certs.

### Domain 4 - Networking

- The built-in network drivers are bridge (default for standalone containers), host, none, overlay (multi-host Swarm), and macvlan; ipvlan is also available.
- User-defined bridge networks provide automatic DNS resolution of containers by name via Docker's embedded DNS at 127.0.0.11; the default bridge (docker0) does NOT, requiring legacy --link instead.
- docker network create mynet defaults to the bridge driver on the local host; add --driver overlay for Swarm-wide networks.
- Publish ports with -p <host-port>:<container-port>; -p 8080:80 forwards host port 8080 to container port 80 via iptables NAT, host port always listed first.
- The host network driver (--network host) removes network isolation: the container shares the host's network namespace, IP, and ports, binding directly to host ports with no NAT.
- The none driver disables all networking, leaving only a loopback interface, useful for fully isolated batch jobs.

### Domain 5 - Security

- Docker Content Trust (DCT) uses The Update Framework (TUF) and Notary to sign image tags at push and verify signatures on pull; enable it by exporting DOCKER_CONTENT_TRUST=1 to enforce signature checks on pull, push, run, and build FROM.
- Swarm secrets are created with docker secret create my_secret ./secret.txt, stored encrypted in the Raft log, delivered to authorized tasks over mutual TLS, and mounted on tmpfs as files under /run/secrets/<name> inside the container (never written to worker disk).
- The --privileged flag grants nearly all Linux capabilities, mounts the host /dev tree, and disables seccomp/AppArmor, effectively breaking container isolation; avoid it in production.
- Drop and add capabilities precisely: docker run --cap-drop ALL --cap-add NET_BIND_SERVICE myapp follows least privilege; NET_BIND_SERVICE lets a non-root process bind ports below 1024.
- --security-opt no-new-privileges sets the no_new_privs kernel bit, preventing the process from gaining new privileges via setuid binaries or file capabilities.
- Docker applies a default seccomp profile that blocks roughly 44 dangerous syscalls, plus mandatory access control via AppArmor (Ubuntu/Debian) or SELinux (RHEL/CentOS).

### Domain 6 - Storage and Volumes

- Docker supports exactly three mount types: volume (Docker-managed under /var/lib/docker/volumes/), bind (any existing host path), and tmpfs (host RAM only).
- Volumes are created and managed by the Docker daemon and survive container removal; bind mounts reference an arbitrary host path that Docker does not manage or clean up.
- Create a named volume with docker volume create myvolume and attach with -v myvolume:/app/data so data persists independently of the container lifecycle.
- Bind-mount a single file or directory for live development or config injection, for example -v /host/path/config.yml:/etc/app/config.yml; append :ro to make any bind or volume mount read-only.
- The modern --mount flag uses explicit key=value pairs (type=volume,source=myvol,target=/data) and is preferred over -v for clarity and better error reporting; type can be volume, bind, or tmpfs.
- tmpfs mounts live entirely in host memory, are never written to disk or the container's writable layer, and disappear when the container stops, making them ideal for sensitive or ephemeral data; cap them with a size limit.

## Study tips

- Memorize quorum math: for N managers, quorum is (N/2)+1, so a 3-manager cluster tolerates 1 failure and a 5-manager cluster tolerates 2. Many orchestration questions hinge on this and on running an odd number of managers across AZs.
- Know the exact flag syntax: -p host:container for ports, -v name:/path versus -v /host:/path for volumes vs bind mounts, and --cap-drop ALL --cap-add <CAP>. The exam tests precise CLI strings, not concepts alone.
- Be able to distinguish near-identical options on multiple-select questions (e.g., COPY vs ADD, replicated vs global services, default bridge vs user-defined bridge DNS). Read every option; several questions have more than one correct answer.
- Drill the daemon.json keys (storage-driver, data-root, dns, hosts, log-driver) and where systemd-specific config lives (drop-in files under /etc/systemd/system/docker.service.d/), since installation/config questions cite exact file paths.
- Manage your 90 minutes across roughly 55 questions: flag long multi-select scenario items, answer the quick command-recall questions first, and leave nothing blank since there is no penalty for guessing.

---

Want the full breakdown? See the complete **[RETIRED - Docker Certified Associate (DCA) study guide](https://certgrid.app/study-guide/retired-docker-certified-associate-dca)** and **[free practice questions](https://certgrid.app/practice/retired-docker-certified-associate-dca)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


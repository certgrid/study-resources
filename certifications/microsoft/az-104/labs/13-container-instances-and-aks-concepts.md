# Lab 13 - Azure Container Instances and AKS Concepts

Containers on AZ-104 mean ACI, Container Apps, and ACR, with AKS as recognition-level context. This lab runs a public image on ACI, reviews ACR, and maps the concepts you need to tell the services apart.

## Time Needed

25-30 minutes.

## What You Will Learn

- How to run a container in ACI with CPU/memory sizing
- What a container group is
- What Azure Container Registry stores and its SKUs
- Where Container Apps and AKS fit (concept level)

## AZ-104 Concepts Covered

| Concept          | Where you see it in the lab           |
| ---------------- | ------------------------------------- |
| ACI              | You deploy a public image             |
| Sizing           | You set CPU cores and memory          |
| Restart policy   | You choose Always/OnFailure/Never     |
| Container groups | You read the group view               |
| ACR              | You review the create screen and SKUs |
| ACA vs AKS       | You compare capabilities in a table   |

## Cost Warning

Small but real: ACI bills PER SECOND while the container runs (a 1 vCPU / 1 GB instance costs a few cents per hour). Delete the container instance at the end of THIS lab. The ACR review step creates nothing.

## Steps

### 1. Deploy a container instance

1. Search **Container instances > Create**.
2. Resource group `rg-az104-labs`, name `aci-lab`, your region.
3. Image source: **Other registry**, image:

```text
mcr.microsoft.com/azuredocs/aci-helloworld:latest
```

4. Size: note the defaults (1 vCPU, 1.5 GiB) and that you can change CPU/memory here: this IS the "manage sizing" exam bullet.
5. Networking: Public with a DNS name label like `aci-lab-<unique>`; port 80.
6. Advanced: look at **Restart policy** options (Always / OnFailure / Never). Keep Always for a web app; OnFailure/Never suit batch jobs.
7. Create, then browse to `http://aci-lab-<unique>.<region>.azurecontainer.io`: the hello-world page loads. Seconds from create to running: that speed is ACI's selling point.

### 2. Read the container group

1. On `aci-lab`, open **Containers**: one container in a container GROUP. Groups can hold multiple containers sharing host, network, and volumes (like a pod); multi-container groups are YAML/template deployments only.
2. Check **Logs** and **Connect** tabs: basic troubleshooting surface.

### 3. CLI recognition

```bash
az container show --name aci-lab --resource-group rg-az104-labs --output table
az container logs --name aci-lab --resource-group rg-az104-labs
```

Creation shape to recognize: `az container create --image ... --cpu 1 --memory 1.5 --restart-policy OnFailure` (PowerShell: `New-AzContainerGroup`).

### 4. Review Azure Container Registry

1. Search **Container registries > Create**; fill nothing in permanently, just read:
   - Name rules (5-50 alphanumeric, becomes `<name>.azurecr.io`)
   - SKUs: Basic / Standard / Premium: Premium adds geo-replication and private link.
2. Cancel. Recognition commands: `az acr create`, `az acr build`, `docker push <registry>.azurecr.io/img:tag`.

### 5. Map the container services

| Need                                                | Service                  |
| --------------------------------------------------- | ------------------------ |
| One container, fast, per-second billing             | Container Instances      |
| Microservices, HTTP scale, scale to zero, revisions | Container Apps           |
| Full Kubernetes API, node pools, cluster control    | Azure Kubernetes Service |
| Store private images for all of the above           | Azure Container Registry |

AKS recognition points (that is all AZ-104 needs): control plane is free/managed, you pay for nodes (VMs), containers scale via pods, and images typically come from ACR.

## Clean Up

Delete the container instance NOW; it bills every second it runs:

```bash
az container delete --name aci-lab --resource-group rg-az104-labs --yes
```

## Success Criteria

You are done when you can explain:

- Why ACI is the answer for quick, isolated container work
- What a container group shares between containers
- Which service scales to zero (Container Apps, not ACI)
- The three ACR SKUs and what Premium adds
- Which restart policy suits a batch job

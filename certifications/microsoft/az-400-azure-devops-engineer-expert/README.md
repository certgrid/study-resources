# AZ-400: Azure DevOps Engineer Expert - Study Cheatsheet

AZ-400: Azure DevOps Engineer Expert validates your ability to combine people, processes, and technologies to deliver products and services continuously across version control, work tracking, infrastructure as code, build, release, security, and monitoring. It is aimed at DevOps professionals who already hold the AZ-104 (Azure Administrator) or AZ-204 (Azure Developer) associate certification and who design and implement DevOps practices primarily with Azure DevOps and GitHub. The 120-minute exam carries roughly 40-60 questions, and you need a scaled score of 700 to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | AZ-400 |
| Credential | AZ-400: Azure DevOps Engineer Expert |
| Level | Advanced |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-24 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Configure Processes and Communications | ~19% |
| 2 | Design and Implement Source Control | ~21% |
| 3 | Design and Implement Build and Release Pipelines | ~22% |
| 4 | Develop a Security and Compliance Plan | ~20% |
| 5 | Implement an Instrumentation Strategy | ~18% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Configure Processes and Communications

- Built-in process templates (Agile, Scrum, CMMI, Basic) cannot be edited directly; to customize work item types or states you must create an inherited process from the desired base, modify it, and switch projects to use the inherited process.
- Branch policies can require linked work items on pull requests, which blocks PR completion until at least one work item is associated, enforcing end-to-end traceability from requirement to code.
- Use the PR completion option (or a transition rule) to automatically move linked work items to Resolved/Closed when the PR merges, reducing manual board upkeep.
- The Predecessor/Successor link type models sequential dependencies (one item must finish before another starts) and is the correct choice for tracking cross-team blocking dependencies; visualize these on Delivery Plans.
- Delivery Plans is a built-in feature that overlays multiple teams' backlogs and iterations on a single timeline, giving leadership a consolidated cross-team view without leaving the project.
- Area paths separate work ownership across teams within one project, while iteration paths define sprints; a single project with multiple teams each owning an area path is the recommended scaling pattern over many small projects.

### Domain 2 - Design and Implement Source Control

- Trunk-based development uses short-lived feature branches (typically 1-3 days) merged frequently into main, minimizing merge conflicts and best supporting continuous deployment at scale.
- GitHub Flow branches features directly off main and merges back via PR, suiting continuous delivery; Gitflow (main, develop, feature, release, hotfix) suits scheduled releases with parallel maintenance.
- For a hotfix in Gitflow, branch from main, apply the fix, then merge back into both main and develop so the fix is not lost in the next release.
- Rebase and fast-forward is the merge strategy that produces a strictly linear history with no merge commits; squash merge collapses a branch into a single commit on the target.
- To permanently purge a large or sensitive file from history you must rewrite history with git filter-repo (recommended) or BFG Repo Cleaner; a normal delete leaves the blob in every prior packfile.
- Git LFS requires a client-side tool installed locally; without it a clone fetches only LFS pointer files (metadata), not the actual binary content.

### Domain 3 - Design and Implement Build and Release Pipelines

- In YAML triggers, the correct keyword is paths with include/exclude lists (for example src/api/*); it is not files, and include selects the directories that activate CI.
- The variables section can mix entry types only when written as a YAML sequence: a '- group: name' entry imports a variable group and a '- name:/value:' entry defines an inline variable.
- Manual approval before production is implemented with environment approvals and checks on an Azure DevOps environment targeted by the deployment job, not with a task inside the job.
- Deployment strategies in deployment jobs include runOnce, rolling (with maxParallel, e.g. 25% to update 25% of targets at a time), and canary; canary shifts traffic incrementally while monitoring.
- Cache@2 is the built-in caching task; for NuGet, key it on the hash of packages.lock.json and point path at the packages folder so the cache is reused only when dependencies are unchanged.
- Publish and consume build outputs across stages with PublishPipelineArtifact@1 and DownloadPipelineArtifact@2, or the YAML shortcut keywords 'publish' and 'download'.

### Domain 4 - Develop a Security and Compliance Plan

- Access Key Vault secrets without hardcoding credentials by using the AzureKeyVault task (or a variable group linked to Key Vault) over an ARM service connection authenticated by a managed identity or service principal.
- Variable groups linked to Azure Key Vault retrieve secret values at runtime; the values are never stored in the pipeline definition and are automatically masked in logs.
- Prefer workload identity federation over long-lived client secrets for ARM service connections, eliminating secret rotation and the risk of leaked credentials.
- Apply least privilege to service connections: scope the service principal's role (for example Contributor) to a single resource group, not the whole subscription.
- Restrict a service connection to authorized pipelines via pipeline permissions so other pipelines cannot use it to reach protected resources.
- GitHub Advanced Security for Azure DevOps provides secret scanning (leaked credentials), dependency scanning (vulnerable open-source packages), and CodeQL code scanning, all integrated into the DevOps experience.

### Domain 5 - Implement an Instrumentation Strategy

- Azure Application Insights is the APM service for distributed tracing across microservices, using correlation IDs and the W3C Trace Context standard to follow a request end to end.
- Use the Application Insights SDK methods TrackMetric() for custom numeric business metrics and TrackEvent() for custom events such as feature usage.
- Auto-instrumentation enables Application Insights monitoring without code changes for supported platforms (for example App Service, Functions), while custom telemetry captures app-specific signals.
- Availability tests (URL ping tests and multi-step web tests) provide synthetic monitoring from multiple global locations to validate uptime and responsiveness.
- Azure Monitor supports metric alerts (static or dynamic thresholds on a metric, for example average server response time > 2s over a 5-minute window) and log alerts (KQL queries against logs).
- Action groups define notification and automation channels including email, SMS, voice, push, webhooks, Azure Functions, Logic Apps, and ITSM connectors, and are reused across multiple alert rules.

## Study tips

- Expect heavy emphasis on Azure DevOps services (Boards, Repos, Pipelines, Artifacts) plus GitHub equivalents; when a question gives requirements like 'minimal effort', 'least privilege', or 'no hardcoded credentials', let those constraints eliminate distractors.
- Know the YAML pipeline schema cold: triggers and path filters, stages/jobs/steps, deployment jobs and strategies (runOnce, rolling, canary), environments with approvals and checks, variable groups vs inline variables, and templates with extends/resources:repositories.
- Distinguish branch policies (require reviewers, build validation, linked work items, comment resolution, merge strategy) from branch security/permissions (block force push); a few questions hinge on this exact split.
- For security questions, default to managed identity or workload identity federation over secrets, scope service connections to the smallest resource and authorized pipelines, and place SAST/SCA in build and DAST against a deployed environment.
- Practice with multi-answer 'select all that apply' and YAML/code drag-and-drop style items, and budget time for one or two case studies; read every requirement before choosing, because partial solutions are common wrong answers.

---

Want the full breakdown? See the complete **[AZ-400 study guide](https://certgrid.app/study-guide/az-400-azure-devops-engineer-expert)** and **[free practice questions](https://certgrid.app/practice/az-400-azure-devops-engineer-expert)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


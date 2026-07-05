# HashiCorp Terraform Associate (004) - Study Cheatsheet

The HashiCorp Terraform Associate (004) exam validates that you understand Infrastructure as Code concepts and can use Terraform's core workflow to provision, manage, and version cloud-agnostic infrastructure. It targets cloud engineers, DevOps practitioners, and developers with hands-on Terraform experience who can write HCL, manage state, consume modules, and use HCP Terraform. The exam is 57-60 multiple-choice questions in 60 minutes, with a scaled passing score around 700.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | HashiCorp Terraform Associate (004) |
| Credential | HashiCorp Terraform Associate (004) |
| Level | Associate |
| Practice mock length | ~57 questions |
| Duration | ~60 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Infrastructure as Code Concepts | ~11% |
| 2 | Purpose of Terraform | ~11% |
| 3 | Terraform Basics | ~11% |
| 4 | Terraform CLI Operations | ~11% |
| 5 | Terraform Modules | ~11% |
| 6 | Core Terraform Workflow | ~11% |
| 7 | State Management | ~11% |
| 8 | HCL Configuration | ~11% |
| 9 | HCP Terraform and Cloud | ~11% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Understand infrastructure as code (IaC) concepts

- Infrastructure as Code means defining infrastructure in machine-readable configuration files (Terraform's .tf files written in HCL) instead of provisioning resources by hand through a console or imperative scripts.
- Because .tf files are plain text, they can be committed to version control such as Git, giving every change an author, timestamp, and commit message, plus peer review through pull requests before apply.
- A 'snowflake server' is a host that drifted into a unique, hard-to-reproduce state through accumulated manual changes; IaC eliminates snowflakes by rebuilding from a single source of truth.
- Terraform is declarative: you describe the desired end state and Terraform computes the create, update, and destroy operations needed to reach it, rather than you writing step-by-step commands.
- The Terraform configuration itself acts as living documentation - reading the code tells you exactly what infrastructure should exist, and it cannot silently drift from reality because it is what Terraform applies.
- Using one parameterized configuration for dev, staging, and production yields consistent environments that differ only by variable values, reducing 'works in staging but not production' problems.

### Domain 2 - Understand the purpose of Terraform (vs other IaC)

- Terraform is cloud-agnostic: a single configuration and workflow can provision AWS, Azure, Google Cloud, and many other platforms, unlike AWS CloudFormation which targets AWS only.
- Terraform uses a plugin-based provider architecture; Terraform Core is decoupled from any platform and relies on interchangeable provider plugins to make API calls.
- A provider translates Terraform resource definitions (HCL) into the API calls of a specific platform such as AWS, Azure, Kubernetes, or a SaaS service.
- Providers are downloaded from the Terraform Registry (registry.terraform.io) during terraform init; HashiCorp and the community publish thousands of providers there.
- You can declare multiple providers in one configuration (for example azurerm and aws) and Terraform manages resources for each in a single plan/apply lifecycle.
- Terraform builds one dependency graph spanning all providers, so it can wire an output from one provider into a resource of another (for example a cloud VPC ID feeding a monitoring config) within a single run.

### Domain 3 - Understand Terraform basics

- terraform init initializes a working directory: it downloads provider plugins declared in required_providers, installs modules, and configures the backend.
- A fully qualified provider source address is HOSTNAME/NAMESPACE/TYPE; for AWS it is registry.terraform.io/hashicorp/aws, and an omitted hostname defaults to registry.terraform.io.
- The required_providers block must be nested inside the top-level terraform block and maps each local provider name to its source and version constraint.
- A provider block (separate from required_providers) configures how an installed provider behaves, such as region or credentials; required_providers declares which providers and versions are needed.
- The .terraform.lock.hcl dependency lock file records the exact provider versions and cryptographic checksums selected during init, ensuring reproducible installs across machines.
- Pin or constrain provider versions to prevent an unexpected major upgrade from introducing breaking changes; commit the lock file so the whole team uses identical versions.

### Domain 4 - Use Terraform outside the core workflow

- The classic terraform import command takes two positional arguments in order: ADDRESS then ID, for example terraform import aws_instance.web i-0abc123.
- Classic CLI import requires that a matching resource block already exist in your configuration; importing into a non-existent address produces an error.
- Config-driven import (Terraform 1.5+) uses an import block with two arguments: to (the resource address, unquoted) and id (the provider-specific string identifier).
- An import block is part of your .tf files, so it is committed to version control and the import is previewed during terraform plan before being applied.
- terraform plan -generate-config-out=generated.tf generates HCL for imported resources into a new file; the target file must not already exist.
- Import only brings the real object into state - it does not write your configuration. If your resource block differs from actual attributes, the next plan proposes changes to reconcile them.

### Domain 5 - Interact with Terraform modules

- Every module block must include the source argument, which tells Terraform where to find the module's .tf files; without it terraform init errors.
- A module is simply a directory containing one or more .tf configuration files; the root module is your working directory and it can call child modules.
- Local path sources begin with ./ or ../ and are resolved relative to the calling module's directory, for example source = "./modules/network".
- Public Terraform Registry module addresses follow NAMESPACE/NAME/PROVIDER, for example terraform-aws-modules/vpc/aws.
- The version argument is honored only for modules from a registry (public or private/HCP); for Git, HTTP, and other generic sources it is ignored - pin those with a ref in the URL.
- Git sources can pin a revision with a ref query parameter, for example source = "git::https://github.com/org/repo.git?ref=v2.0.0".

### Domain 6 - Use the core Terraform workflow

- The core individual workflow is three ordered stages: Write (author HCL), Plan (preview changes), Apply (provision real infrastructure).
- terraform plan creates an execution plan showing proposed create/update/destroy actions without making any changes; it first refreshes in-memory state against real resources to detect drift.
- Plan symbols: + means create, - means destroy, ~ means update in place, and -/+ means destroy and then recreate (replacement).
- A -/+ replacement destroys the existing object and creates a new one because a changed attribute forces replacement; a ~ in-place update keeps the same object and provider-assigned ID.
- terraform apply without a saved plan generates its own plan, displays the changes, then pauses and requires you to type the literal word "yes"; any other input cancels with no changes made.
- Save a reviewed plan with terraform plan -out=tfplan, then terraform apply tfplan executes exactly those actions with no re-prompt, guaranteeing the applied changes match the reviewed plan.

### Domain 7 - Implement and maintain state

- With no backend declared, Terraform uses the local backend and writes state to terraform.tfstate in the current working directory.
- The backend is configured with a backend block nested inside the top-level terraform block; only one backend block is allowed per configuration.
- Any change to the backend configuration requires re-running terraform init, which detects the change and offers to migrate existing state to the new location.
- Remote backends (s3, azurerm, gcs, HCP Terraform) store a single shared source-of-truth state so the whole team reads and writes the same state.
- State locking prevents two engineers from running apply simultaneously and corrupting state; most remote backends provide locking automatically.
- Without remote state and locking you risk concurrent applies, merge conflicts, and exposed secrets, since state can contain sensitive values in plain text.

### Domain 8 - Read, generate, and modify configuration

- Variable value precedence from lowest to highest: environment variables (TF_VAR_name), then terraform.tfvars, then *.auto.tfvars (alphabetical), then -var and -var-file flags on the command line, which win over everything.
- Among auto-loaded files, *.auto.tfvars files are processed after terraform.tfvars, so a value in an .auto.tfvars file overrides the same key in terraform.tfvars.
- A variable with a default uses that default when no value is supplied; a variable with no default and no supplied value is required and prompts interactively in a terminal (or errors in non-interactive runs).
- Set values via -var="key=value" or -var-file=staging.tfvars on the CLI, via terraform.tfvars/*.auto.tfvars files, or via the TF_VAR_<name> environment variable.
- Variable type constraints include primitives (string, number, bool) and complex types such as list(...), map(...), set(...), and object({ name = string, count = number }).
- Terraform performs automatic type conversion where possible, for example converting the string "8080" to the number 8080; if conversion is impossible it errors during validation.

### Domain 9 - Understand HCP Terraform capabilities

- Connect a working directory to HCP Terraform with a cloud block nested inside the terraform block, specifying the organization and a workspaces selector (name or tags).
- In the CLI-driven workflow with the cloud block, the default execution mode is remote: terraform apply uploads the configuration and runs plan/apply on HCP Terraform's managed infrastructure while streaming output to your terminal.
- Local execution mode runs plan and apply on your own machine but still stores state in HCP Terraform.
- The VCS-driven workflow connects a workspace to a Git repository (GitHub, GitLab, Bitbucket) via webhooks, so pushes/merges to the tracked branch and PRs targeting it automatically queue runs.
- A VCS-connected workspace treats the repository as the source of truth and rejects CLI-uploaded configuration for apply runs.
- The default run flow is plan, then a Needs Confirmation pause requiring a user with apply permission to click Confirm & Apply, then apply.

## Study tips

- Memorize the exact plan action symbols (+, -, ~, -/+) and which CLI flags change behavior (-out, -target, -refresh-only, -auto-approve), since many questions hinge on precise command and symbol meaning.
- Know variable precedence cold - environment variables lose to terraform.tfvars, which loses to *.auto.tfvars, which loses to -var/-var-file flags - because it is a frequent tricky question.
- Distinguish required_providers (declares which providers/versions) from the provider block (configures behavior), and remember the source address format HOSTNAME/NAMESPACE/TYPE.
- Be clear on what terraform init does and when it must be re-run: changing providers, modules, or the backend all require another init.
- Read every option fully on import, state, and HCP workflow questions; the difference between classic CLI import (resource block must pre-exist) and config-driven import blocks (1.5+, generate-config-out) is a common trap.

---

Want the full breakdown? See the complete **[HashiCorp Terraform Associate (004) study guide](https://certgrid.app/study-guide/hashicorp-terraform-associate-004)** and **[free practice questions](https://certgrid.app/practice/hashicorp-terraform-associate-004)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


# GitHub Actions - Study Cheatsheet

The GitHub Actions certification validates your ability to build and manage CI/CD automation using GitHub Actions, covering workflow syntax and events, jobs/steps/runners, secrets and security, and reuse/optimization patterns. It is aimed at developers, DevOps engineers, and platform engineers who author and maintain GitHub-native automation. The exam is 832-question-pool based with a passing score of 700 and a 120-minute duration.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | GitHub Actions |
| Credential | GitHub Actions |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Workflows and Events | ~27% |
| 2 | Jobs, Steps, and Runners | ~28% |
| 3 | Secrets and Security | ~23% |
| 4 | Reuse and Optimization | ~22% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Workflows and Events

- Workflows are defined in YAML files placed in the .github/workflows/ directory at the root of the repository; each file is one workflow.
- The top-level on: key declares triggers; common ones are push, pull_request, schedule (cron), and workflow_dispatch (manual). It accepts a single event, an array, or a map with filters.
- branches / branches-ignore filter which branches trigger push and pull_request; paths / paths-ignore filter by changed files (e.g. paths-ignore: ['**.md'] skips docs-only changes).
- branches and branches-ignore cannot be used together in the same event; likewise paths and paths-ignore are mutually exclusive.
- workflow_dispatch can define inputs (with required, type: string/boolean/choice/number, and default) that are entered when the workflow is manually run and read via inputs.<name> or github.event.inputs.<name>.
- schedule uses POSIX cron syntax in UTC (e.g. '0 2 * * *'); the shortest interval allowed is every 5 minutes, and scheduled runs can be delayed during high load.

### Domain 2 - Jobs, Steps, and Runners

- A job is a set of steps that runs on a single runner; by default all jobs in a workflow run in parallel unless ordered with needs.
- needs: [jobA] makes a job wait for the listed job(s) to finish successfully before it starts, creating a dependency graph.
- runs-on specifies the runner: GitHub-hosted labels like ubuntu-latest, windows-latest, macos-latest, or self-hosted labels for custom hardware.
- Self-hosted runners are used for specific hardware, on-prem network access, custom software, or compliance needs; you manage and secure them yourself.
- Steps either run a shell command (run:) or invoke a reusable action (uses:); the with: keyword passes inputs to an action.
- A matrix strategy (strategy.matrix) runs a job across combinations such as OS and language versions in parallel; fail-fast: false lets all combinations finish instead of cancelling siblings on first failure.

### Domain 3 - Secrets and Security

- An action is a packaged, reusable unit of automation referenced in a step via uses: (e.g. actions/checkout@v4); actions/checkout clones the repo into the runner workspace.
- Custom actions come in three flavors: JavaScript (runs via Node.js on the runner), Docker container (packages code plus its environment), and composite (bundles multiple steps/commands into one action).
- Pin third-party actions to a full-length commit SHA rather than a mutable tag; a SHA is immutable so the exact reviewed code runs even if the v4 tag is later moved by a maintainer or attacker.
- Store credentials as encrypted secrets and reference them as ${{ secrets.NAME }}; set one via the CLI with gh secret set API_KEY --body "value".
- The permissions: key sets GITHUB_TOKEN scopes at the workflow or job level; apply least privilege, e.g. permissions: { contents: read, packages: write }.
- Set permissions: { id-token: write } to allow the workflow to request an OIDC token for cloud authentication.

### Domain 4 - Reuse and Optimization

- GITHUB_TOKEN is an automatically provided, repo-scoped token created per run; its permissions are configurable and it expires when the job finishes.
- Reusable workflows (on: workflow_call) eliminate copy-pasted YAML by centralizing common pipelines; callers pass inputs and secrets and consume the workflow's outputs.
- actions/upload-artifact and actions/download-artifact move files between jobs and runs; set a short retention-days and upload only what is needed to control storage cost.
- actions/cache supports restore-keys as fallback prefixes so a partial hit from a similar older key still saves download time when the exact key misses.
- Caches are evicted least-recently-used once a repository exceeds the 10 GB total cache limit; caches are also scoped by branch with main-branch caches readable by other branches.
- GitHub-hosted minutes are billed by rounded-up wall-clock minutes per job at a per-minute rate; Windows runners cost 2x and macOS runners cost 10x the Linux rate.

## Study tips

- Memorize the canonical YAML keys and where they live: on:, jobs:, runs-on:, steps:, uses:/run:, with:, needs:, permissions:, concurrency:, strategy.matrix - many questions test exact placement.
- Know the difference between $GITHUB_OUTPUT (step outputs read via steps.<id>.outputs) and $GITHUB_ENV (env vars for later steps), and how job outputs flow through needs.<id>.outputs.
- Security questions hinge on least-privilege permissions:, SHA-pinning actions, OIDC vs long-lived keys, and the danger of pull_request_target with untrusted fork code - read those scenarios carefully.
- For cost questions, remember minutes round UP per job, Windows is 2x and macOS is 10x Linux, the cache limit is 10 GB with LRU eviction, and self-hosted runners are not billed minutes.
- When a question lists multiple plausible answers, pick the one matching GitHub's documented best practice (path filters, caching keyed on lockfiles, fail-fast: false for full results, concurrency with cancel-in-progress).

---

Want the full breakdown? See the complete **[GitHub Actions study guide](https://certgrid.app/study-guide/github-actions)** and **[free practice questions](https://certgrid.app/practice/github-actions)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


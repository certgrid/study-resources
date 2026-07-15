# GitHub Foundations - Study Cheatsheet

GitHub Foundations validates entry-level knowledge of the GitHub platform: Git fundamentals, repositories, collaboration through issues and pull requests, GitHub Actions basics, and the wider GitHub ecosystem including security and account management. It is designed for developers, project managers, students, and anyone new to GitHub who wants to demonstrate baseline proficiency. The exam has roughly 75 questions, a 90-minute time limit, and is scored on a 100-1000 scale with 700 to pass.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | GitHub Foundations |
| Credential | GitHub Foundations |
| Level | Intermediate |
| Practice mock length | ~60 questions |
| Duration | ~90 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Introduction to GitHub | ~21% |
| 2 | Working with Repositories | ~24% |
| 3 | Collaboration Features | ~23% |
| 4 | Modern Development | ~31% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Introduction to GitHub

- Git is a distributed version control system (DVCS): every clone is a full copy of the repository including its entire commit history, so work can continue offline.
- A commit is an immutable snapshot of staged changes, identified by a unique 40-character SHA-1 hash, and carries an author, committer, message, and timestamp.
- A repository is the version-controlled container for a project's files, complete change history, branches, issues, pull requests, and settings.
- Common Git workflow commands: git add stages changes, git commit records staged changes locally, git push uploads local commits to a remote, git clone copies a remote repo (with history) locally.
- git fetch downloads remote changes without merging them; git pull does a fetch AND merge into your current branch (pull = fetch + merge).
- Branches create independent, parallel lines of development; create and switch with git switch -c <branch> (or the older git checkout -b <branch>).

### Domain 2 - Working with Repositories

- A pull request proposes changes from a source branch into a target branch (often main) and provides a place for discussion, review, and automated checks before merging.
- Issues track tasks, bugs, feature requests, and discussions; they can be assigned, labeled, grouped into milestones, and linked to pull requests.
- A fork is a personal copy of someone else's repository where you make changes independently and propose them back to the upstream via a pull request.
- A merge conflict occurs when different branches change the same lines and Git cannot auto-merge; it must be resolved manually before the merge completes.
- The main (default) branch is the primary, usually stable line of a project's code; branch protection rules can guard it.
- Branch protection rules can require pull request reviews, require status checks (CI) to pass, and prevent direct pushes before changes reach a protected branch.

### Domain 3 - Collaboration Features

- GitHub Actions is a CI/CD and automation platform that runs workflows in response to repository events such as push and pull_request, on a schedule, or via manual dispatch.
- Actions (the reusable units inside workflows) come in three types: JavaScript actions, Docker container actions, and composite actions; the Marketplace offers thousands of prebuilt ones.
- A README on the repository's main page documents the project's purpose, setup, and usage; it is the first thing visitors see.
- GitHub Pages hosts static websites directly from a repository (for example from the main branch, a /docs folder, or a gh-pages branch).
- GitHub Codespaces provides cloud-hosted development environments accessible in the browser or VS Code, with the repository pre-cloned and tooling preconfigured.
- GitHub Packages hosts and shares packages (npm, Maven, NuGet, RubyGems, Docker, etc.) alongside source code with the same permissions model.

### Domain 4 - Modern Development

- GitHub Actions secrets are encrypted at rest, decrypted only in runner memory during execution, automatically masked from logs, and referenced as secrets.NAME; they can be set at repo, environment, or organization level.
- GitHub Advanced Security features include code scanning (SAST, often via CodeQL), secret scanning, and dependency review to find vulnerabilities before merge.
- Apply least privilege when granting access: give collaborators only the role they need (read, triage, write, maintain, or admin).
- Workflows are defined as YAML files in the .github/workflows/ directory; each specifies triggers (on), jobs, and steps.
- The GITHUB_TOKEN is an automatically created, short-lived token whose scope can be narrowed with the permissions key in a workflow for least-privilege automation.
- Environment protection rules can require manual approval or wait timers before a job deploys to a sensitive environment such as production.

## Study tips

- Know the precise difference between similar Git commands: fetch vs pull (pull adds the merge), merge vs rebase, and clone vs fork vs star; these distinctions are frequently tested.
- Memorize where configuration files live: workflows in .github/workflows/, plus CODEOWNERS, issue/PR templates, and dependabot.yml in the .github directory.
- Match the GitHub feature to the scenario: Pages for static sites, Codespaces for cloud dev environments, Packages for artifacts, Actions for automation, Projects/Milestones for planning.
- Watch for cost and billing questions: included free minutes, the spending limit in billing settings, monthly billing cycle, self-hosted runner trade-offs, and free runners for public repos.
- Read scenario questions carefully and pick the least-privilege, most-secure option (encrypted secrets, scoped GITHUB_TOKEN, branch protection with required reviews and status checks).

---

Want the full breakdown? See the complete **[GitHub Foundations study guide](https://certgrid.app/study-guide/github-foundations)** and **[free practice questions](https://certgrid.app/practice/github-foundations)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


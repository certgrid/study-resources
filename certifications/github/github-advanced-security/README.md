# GitHub Advanced Security - Study Cheatsheet

GitHub Advanced Security (GH-500) validates that you can secure code across the software supply chain using GHAS features: secret scanning, dependency management with Dependabot, code scanning with CodeQL, and security administration across GitHub Enterprise Cloud and Server. It is aimed at security engineers, DevOps practitioners, and administrators responsible for rolling out and operating GHAS. The exam covers feature functionality and availability, alert triage and remediation, custom CodeQL queries, and enterprise licensing and configuration.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | GitHub Advanced Security |
| Credential | GitHub Advanced Security |
| Level | Intermediate |
| Practice mock length | ~75 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | GHAS Security Features and Functionality | ~10% |
| 2 | Secret Scanning | ~15% |
| 3 | Dependency Management | ~15% |
| 4 | Code Scanning | ~15% |
| 5 | Code Scanning with CodeQL | ~10% |
| 6 | GHAS Best Practices and Corrective Measures | ~14% |
| 7 | GHAS Administration in GitHub Enterprise | ~21% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - GHAS Security Features and Functionality

- GitHub recognizes a SECURITY policy file automatically only when it lives in the repository root, a docs folder, or a .github folder, and links it from the Security tab.
- By default only repository administrators and security managers can view secret scanning alerts; broader visibility must be granted deliberately to other users or teams.
- The security manager role grants read access across all of an organization's repositories plus write access to security alerts, without full owner-level administrative control.
- Dependabot alerts are a free core feature that works on private repositories without any GHAS license, unlike secret scanning and its push protection.
- Secret scanning push protection blocks a push containing a recognized secret pattern before it enters repository history, and an authorized user can request a bypass with a stated reason.
- Custom secret scanning patterns let an organization define its own detection rule, usually a regular expression, for token formats not covered by GitHub's built-in patterns.

### Domain 2 - Secret Scanning

- The secret scanning alert list can be filtered by secret type, validity status, and alert state (open or closed).
- Validity checks classify supported secrets as active, inactive, or unknown based on the partner provider's response to GitHub's query.
- Secret scanning covers GitHub Discussions posts and comments, issues, pull requests, and wikis, not just source code.
- Push protection must be opted into per custom pattern; when a push is blocked, an authorized user can bypass it with a permitted reason if the organization allows it.
- A secret buried in an earlier commit must be removed from that specific commit, typically via interactive rebase, since amending only the tip leaves it in history.
- Repository-level custom patterns are capped at a fixed maximum, and reaching that limit prevents adding another pattern at that level.

### Domain 3 - Dependency Management

- Direct dependencies are explicitly declared in a manifest, while transitive dependencies are pulled in indirectly and are revealed through a lockfile's resolved tree.
- NuGet projects need a packages.lock.json file for the dependency graph to show transitive packages, and Python projects need a lockfile like Pipfile.lock or poetry.lock beyond requirements.txt.
- In dependabot.yml, the allow key restricts Dependabot to only the listed dependencies, while setting open-pull-requests-limit to 0 for an ecosystem stops all new version-update PRs without deleting the entry.
- The groups key bundles matching version updates (such as devDependencies) into a single combined pull request, and the plural directories key matches multiple paths or globs in one entry.
- Security update pull requests require the dependency graph, Dependabot alerts, and Dependabot security updates to all be enabled together.
- Dependency review runs as a pull request check that flags vulnerable dependencies introduced by that change; fail-on-severity sets the threshold and allow-ghsas excludes specific advisory IDs.

### Domain 4 - Code Scanning

- Default setup enables CodeQL with minimal configuration, while advanced setup uses a workflow file and suits custom build handling or combining CodeQL with an external SARIF-producing tool.
- A CodeQL workflow separates configuration of languages and queries in an init step from the scan performed in a later analyze step.
- build-mode is set per language: none for interpreted languages, and autobuild or manual for compiled languages such as C#, C++, or Java that require an actual build.
- In the queries field, prefixing a suite name with a plus sign adds it to the default suite instead of replacing it, and a relative path can point to a local directory of custom .ql files.
- The packs field references published, versioned CodeQL query packs by scope, name, and version.
- paths-ignore exclusions are applied on top of paths inclusions, so an ignored subdirectory stays excluded even if it falls under an included path.

### Domain 5 - Code Scanning with CodeQL

- Rendering a full source-to-sink flow path in the results UI requires the path-problem query kind, which is built on path-flow classes; the plain problem kind surfaces a single location only.
- A source is where tainted data enters, a sink is where it causes harm if it arrives unsanitized, and a barrier marks a point where tainted data should no longer be considered to flow.
- A Configuration class exposing isSource and isSink predicates is the standard pattern for expressing global data flow or taint tracking.
- codeql database analyze accepts sarif-latest, which code scanning uploads accept, while CSV output suits internal reporting but is not accepted for upload.
- The @id metadata is the stable machine identifier code scanning uses to recognize the same query's alerts across scans, and @name supplies the human-readable alert title.
- Compiled languages like Java, C++, and Go rely on tracing an actual build for extraction, so a CodeQL database only captures code compiled during that traced build.

### Domain 6 - GHAS Best Practices and Corrective Measures

- GitHub Actions has no built-in on trigger for code scanning, secret scanning, or Dependabot alert events, so reacting to them requires an external receiver that forwards the webhook and calls the repository dispatch API.
- Every webhook configuration page keeps a Recent Deliveries log showing each attempt, its response status, and a redeliver option to replay events missed during a receiver outage.
- An organization-level security configuration that applies secure defaults ensures every new repository inherits protection automatically without manual per-repository setup.
- A ruleset that requires the code scanning results status check to pass can target many repositories at once, enforcing a consistent merge gate without per-repository branch protection.
- Real confirmation that a fix worked comes from a fresh scan no longer reporting the finding and the specific alert transitioning to closed, not from a merged status alone.
- A reopened alert with a new data flow path deserves fresh review because the code that produced the earlier dismissal has since changed.

### Domain 7 - GHAS Administration in GitHub Enterprise

- The security-events write permission is what authorizes a workflow token to upload SARIF analysis results into code scanning.
- GitHub Connect must first be enabled at the enterprise level, after which individual features such as advisory database sync and Actions sync are turned on separately.
- Dependabot alerts rely on the synced advisory database, so on a GHES instance without that Connect feature the instance will not know about recently disclosed vulnerabilities.
- An air-gapped GHES instance that blocks outbound internet access loses GitHub Connect, so administrators must manually download and upload the CodeQL Action and CLI bundle and advisory data on a recurring basis.
- GHAS billing counts active committers, defined by qualifying pushes within a rolling 90-day window, so removing a departed engineer's access does not immediately clear their committer count.
- An external collaborator who pushes to a GHAS-enabled repository is counted as an active committer just like an organization member.

## Study tips

- Memorize what each GHAS feature requires: Dependabot alerts are free, but secret scanning, push protection, and CodeQL code scanning need a GHAS license on private repositories.
- Know the exact dependabot.yml keys and their effects (allow, ignore, groups, directories, open-pull-requests-limit, schedule) since the exam tests configuration outcomes directly.
- For CodeQL questions, keep build-mode straight: none for interpreted languages, autobuild or manual for compiled ones, and remember path-problem is required for source-to-sink flow paths.
- When a question asks how to confirm a fix, choose the answer involving a fresh scan and the alert transitioning to closed, not a merge or a manual dismissal.
- Watch for the 90-day active-committer billing window and the fact that automatic enablement settings are never retroactive to existing repositories.

---

Want the full breakdown? See the complete **[GitHub Advanced Security study guide](https://certgrid.app/study-guide/github-advanced-security)** and **[free practice questions](https://certgrid.app/practice/github-advanced-security)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


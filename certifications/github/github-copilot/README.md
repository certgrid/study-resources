# GitHub Copilot - Study Cheatsheet

The GitHub Copilot certification (GH-300) validates that you can use GitHub Copilot effectively and responsibly across the software development lifecycle. It targets developers, team leads, and technical decision makers who work with Copilot in the IDE, Chat, CLI, and agent workflows. The exam covers responsible AI use, Copilot plans and features, data flow and architecture, prompt engineering, real-world productivity use cases, and privacy and content-exclusion configuration.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | GitHub Copilot |
| Credential | GitHub Copilot |
| Level | Intermediate |
| Practice mock length | ~75 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Using GitHub Copilot Responsibly | ~17% |
| 2 | GitHub Copilot Features | ~28% |
| 3 | Copilot Data and Architecture | ~13% |
| 4 | Prompt Engineering and Context Crafting | ~13% |
| 5 | Developer Productivity with Copilot | ~14% |
| 6 | Privacy, Content Exclusions, and Safeguards | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Using GitHub Copilot Responsibly

- Accountability for merged code stays with the human developer and reviewers, not with Copilot; accepting and committing a suggestion makes you the owner of that code.
- Copilot suggestions are statistically plausible completions, not verified-correct implementations, so you must read and reason about every suggestion before accepting it, especially edge cases like unusual date formats or locales.
- Copilot can hallucinate plausible-but-fake APIs, method names, or CLI flags (for example a git flag that follows the naming style but was never implemented) because it predicts likely tokens rather than consulting real documentation.
- Training-data staleness means Copilot may keep suggesting deprecated libraries (such as Microsoft's ADAL after the recommended migration to MSAL) if its data predates the shift.
- Never place live credentials, hardcoded API keys, passwords, or real customer personal data in source or prompts; replace secrets with an environment variable or secret-manager reference.
- A code-referencing / public-code match should trigger review of the actual license terms and a decision to rewrite or add attribution before shipping.

### Domain 2 - GitHub Copilot Features

- Copilot plans progress from Copilot Free (single model, verified students get Copilot Pro free) to Pro, Pro+ (a considerably larger premium-request allowance), Business, and Enterprise.
- Each Copilot Business seat includes the same base premium-request allowance as an individual Pro subscription; organization owners assign seats and can delegate seat management, but developers cannot self-assign a seat.
- The coding agent works autonomously by creating its own branch and opening the pull request itself as part of its workflow.
- Copilot code review lets developers request automated reviews that appear alongside human comments, and organizations can scope the policy broadly or narrowly.
- The standalone Copilot CLI runs independently of any editor and works over a plain SSH session, whereas the IDE's integrated terminal panel is an editor feature; the terminal chat participant answers using recent terminal commands and output.
- Official Copilot Chat surfaces include the IDE, github.com, the GitHub mobile app, and Windows Terminal, and each surface is governed by its own distinct organization policy toggle.

### Domain 3 - Copilot Data and Architecture

- Every request passes through GitHub's Copilot proxy even when a different underlying model handles generation, keeping the architecture consistent across model choices.
- The proxy layer screens prompts for toxic or offensive content before inference, so problematic input is caught early rather than after generation.
- The suggestion lifecycle runs prompt building, inference, then post-processing (including public-code matching and deduplication), then ranking by a quality/confidence score, with the top-ranked candidate shown as inline ghost text.
- Copilot generates suggestions from learned patterns and does not compile or execute code to verify correctness, so a suggestion can look reasonable yet fail to build or run.
- The context window is measured in tokens (sub-word units), and cost and resource use scale with token count, so unusual identifiers and dense minified code consume more tokens per character.
- When a prompt exceeds the token limit, Copilot truncates lower-priority context (distant lines, less-relevant tabs) while preserving the code closest to the cursor; it does not reject the request outright.

### Domain 4 - Prompt Engineering and Context Crafting

- The three core components of a well-formed prompt are context (relevant background), intent (the desired outcome), and specificity (concrete inputs, constraints, or examples); omitting any one tends to yield vague responses.
- Zero-shot gives no example, one-shot provides exactly one worked example before asking Copilot to continue, and few-shot supplies several examples to pin down the pattern.
- Prompt files let a team save and reuse a well-crafted, on-demand prompt across members, while custom instructions apply ambient guidance to all interactions; a good prompt file specifies output format and expected inputs.
- Reference the exact file with a chat file reference (for example #file) to bring its real content into context instead of relying on the model guessing.
- Close unrelated files and keep relevant ones open, and add relevant imports and type hints, to reduce noise and prime Copilot toward the intended library and data shapes.
- Avoid contradictory instructions, such as requiring an unchanged signature while also adding new required parameters; decide which constraint actually applies and state it clearly before re-prompting.

### Domain 5 - Developer Productivity with Copilot

- Copilot Chat can propose plausible reasons a query is slow (a missing index, an unneeded join), but these are hypotheses from the query structure that you must confirm against the real schema and execution plan.
- Generate test fixtures by describing the schema's field names and types and asking for fabricated values, which produces structurally accurate data without pulling real production data into a committed file.
- Copilot can translate code between languages by mapping source logic to idiomatic target constructs (for example TypeScript interfaces from Python type hints), but subtle behavioral differences still require human review.
- Refactors that change a contract must ripple to callers: switching from thrown exceptions to a result object, splitting a class, or extracting DB calls into a repository all change the public surface, and repository extraction can silently alter transaction and connection scoping.
- High line coverage does not equal branch coverage, because a conditional line can be marked covered by hitting only one branch; genuine edge cases (empty carts, negative totals, invalid quantities) must be exercised explicitly.
- For test generation, name the desired framework or keep an existing test file open to steer Copilot toward the right conventions (for example JUnit 5), and verify a cache test actually exercises eviction, not just get and set.

### Domain 6 - Privacy, Content Exclusions, and Safeguards

- Content exclusion is a path-based, admin-managed control: a repository-root pattern of "/**" excludes every file, and completions appear in a file based solely on whether that file's own path matches a rule.
- Exclusion works only by file path, so an unexcluded file (for example pricing-notes.md) can still surface the same concepts, because rules have no awareness of files that describe the same idea in other words.
- Repository-level exclusion is a flat list of path patterns configured in that repository's Settings under Copilot, while organization-level configuration pairs each repository name with its own paths.
- Content-exclusion changes can take up to about 30 minutes to propagate, and reloading or restarting the editor forces Copilot to reconnect and fetch the current rules.
- The Copilot status icon or menu in the editor reflects whether the currently open file is excluded.
- GitHub's IP indemnification is available only to Business and Enterprise customers, is scoped to claims involving Copilot-suggested code, and requires the public-code matching filter to stay enabled; disabling that filter removes the indemnification basis.

## Study tips

- Copilot is a probabilistic assistant, not an oracle: on nearly every question, the safest answer preserves human review, verification, and accountability rather than blind trust in the output.
- Learn the plan matrix cold (Free, Pro, Pro+, Business, Enterprise) plus who owns seat assignment, which capabilities are policy-gated per surface, and that Business/Enterprise exclude data from training by default.
- Memorize the suggestion lifecycle order (prompt build, proxy screening, inference, post-processing/public-code match, ranking, display) and that everything flows through the Copilot proxy regardless of model.
- Distinguish similar-sounding controls: content exclusion (admin, path-based, shared) vs the personal per-language toggle, prompt files (reusable task) vs custom instructions (ambient guidance), and public-code filter Blocked vs Allow-with-referencing.
- For IP indemnification and privacy questions, remember the qualifying condition: Business/Enterprise only, and only while the public-code matching filter stays enabled.

---

Want the full breakdown? See the complete **[GitHub Copilot study guide](https://certgrid.app/study-guide/github-copilot)** and **[free practice questions](https://certgrid.app/practice/github-copilot)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


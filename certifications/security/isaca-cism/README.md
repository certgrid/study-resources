# ISACA CISM - Study Cheatsheet

The ISACA Certified Information Security Manager (CISM) exam validates the ability to govern, design, and manage an enterprise information security program rather than to perform hands-on technical tasks. It targets experienced security managers, aspiring CISOs, IT consultants, and risk and compliance professionals who align security with business strategy. The 4-hour exam has 150 multiple-choice questions scored on a 200-800 scale (700 to pass) across four domains: Governance, Risk Management, Program, and Incident Management.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | ISACA CISM |
| Credential | ISACA CISM |
| Level | Intermediate |
| Practice mock length | ~100 questions |
| Duration | ~240 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-06-23 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Information Security Governance | ~24% |
| 2 | Information Security Risk Management | ~20% |
| 3 | Information Security Program | ~30% |
| 4 | Incident Management | ~25% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Information Security Governance

- Information security governance is a subset of enterprise (corporate) governance; its primary goal is to align the security strategy with business objectives, not to operate as a standalone technical function.
- The single most important success factor for a security program is visible, committed senior management and board support - it provides the authority, funding, and 'tone at the top' that makes security culture enforceable.
- The document hierarchy is strict: policies state high-level management intent (the 'what/why'), standards define mandatory measurable requirements (specific algorithms, configurations), procedures give step-by-step instructions (the 'how'), and guidelines are recommended but optional.
- Senior management and the board are accountable for information security risk and must formally approve risk appetite; the information security manager drives and implements the strategy but does not own the residual-risk acceptance decision.
- A RACI matrix assigns exactly one Accountable party per task or decision, plus Responsible (do the work), Consulted (provide input), and Informed (kept updated) roles to remove ambiguity.
- The data/information owner (a business role) classifies data, defines who may access it, and approves access; the custodian (often IT) implements and maintains the controls the owner specifies.

### Domain 2 - Information Security Risk Management

- Risk is a function of likelihood and impact (Risk = Likelihood x Impact), expressing the probability that a threat exploits a vulnerability and the resulting harm.
- There are exactly four risk treatment options: avoid (stop the activity), mitigate (reduce likelihood/impact with controls), transfer (shift financial impact via insurance or contract), and accept (formally acknowledge residual risk within appetite).
- Risk appetite is the aggregate amount and type of risk leadership is willing to accept in pursuit of objectives; risk tolerance is the acceptable variation around a specific risk. Appetite is set by senior management/the board.
- Residual risk is what remains after controls are applied; risk acceptance is appropriate only when residual risk is within appetite and treatment cost outweighs benefit, with formal sign-off from an authorized risk owner.
- Quantitative analysis uses monetary values: SLE = Asset Value x Exposure Factor, ALE = SLE x ARO; the justification for a control is comparing the reduction in ALE to the annualized cost of the control.
- Qualitative analysis ranks risks by relative severity (high/medium/low or scored likelihood x impact matrices) and is faster and cheaper but more subjective than quantitative methods.

### Domain 3 - Information Security Program

- Security awareness training targets the human factor (phishing, social engineering, password misuse) - the goal is to change user behavior to reduce human-related risk, measured by metrics such as declining phishing click rates.
- Program value to leadership is demonstrated with KPIs tied to business outcomes: fewer/less-severe incidents, faster MTTD/MTTR, critical vulnerabilities remediated within SLA, and improving compliance posture - not raw activity counts.
- Controls are classified by type - preventive (MFA, access controls, hardening, input validation), detective (IDS, log monitoring, audits), and corrective (backups, patching, incident response) - and a defense-in-depth program layers all three.
- Aligning the program to a recognized framework (ISO/IEC 27001, NIST CSF, CIS Controls, COBIT) ensures comprehensive coverage, provides a common language with auditors, and avoids overlooked threat categories.
- ISO/IEC 27001 certifies an Information Security Management System (ISMS); its Statement of Applicability (SoA) documents which Annex A controls apply and why others are excluded.
- Third-party/vendor risk is managed contractually: define required controls, breach-notification obligations, and right-to-audit clauses, and review independent assurance reports (SOC 2 Type II, ISO 27001) for ongoing assurance.

### Domain 4 - Incident Management

- The NIST SP 800-61 incident response lifecycle that CISM follows has four phases: Preparation; Detection and Analysis; Containment, Eradication, and Recovery; and Post-Incident Activity (lessons learned).
- Preparation - building the plan, tools, roles, communication trees, and training before an incident - is the phase that most reduces response time and improvisation under pressure.
- When an incident is confirmed, the immediate priority is containment to limit the spread and damage; eradication (removing the threat and its root cause) and recovery follow after containment.
- Key incident metrics are MTTD (Mean Time to Detect - incident start to identification) and MTTR (Mean Time to Respond/Recover - detection through return to normal); a downward MTTR trend signals improving maturity.
- Legal and regulatory breach-notification deadlines are strict and drive escalation - e.g., GDPR requires notifying the supervisory authority within 72 hours of becoming aware of a personal-data breach.
- Evidence handling requires chain of custody and forensic imaging: capture a bit-for-bit image (e.g., with dd) and compute a hash (e.g., SHA-256) to prove integrity; preserve volatile data first (order of volatility).

## Study tips

- Always answer as a security MANAGER, not a technician: choose the governance, risk, or business-aligned option over the hands-on technical fix. When in doubt, the answer that involves senior management, business alignment, or risk appetite is usually correct.
- Identify the FIRST/BEST/MOST/PRIMARY step. CISM questions hinge on these qualifiers - many options are valid actions, but only one is the best first step (often risk assessment, asset identification, or obtaining management support).
- Map every scenario back to business value and risk. The justification for any control, spend, or decision is reducing business risk to within the organization's risk appetite - never security for its own sake.
- Know the standard sequences cold: the four risk responses, the NIST incident lifecycle phases, and the policy-standard-procedure hierarchy. Questions test whether you order or classify them correctly.
- Pace yourself: 150 questions in 240 minutes is about 90 seconds each. Flag and skip lengthy scenario questions, answer the quick wins first, and return to the hard ones - there is no penalty for guessing.

---

Want the full breakdown? See the complete **[ISACA CISM study guide](https://certgrid.app/study-guide/isaca-cism)** and **[free practice questions](https://certgrid.app/practice/isaca-cism)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


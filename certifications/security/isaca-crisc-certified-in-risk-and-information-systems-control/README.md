# ISACA CRISC (Certified in Risk and Information Systems Control) - Study Cheatsheet

ISACA's CRISC (Certified in Risk and Information Systems Control) validates the ability to identify, assess, respond to, and monitor enterprise IT risk and to design and maintain information systems controls. It is aimed at risk practitioners, control professionals, and IT/business managers who own or oversee risk. The exam is scenario-heavy and spans four domains: Governance, IT Risk Assessment, Risk Response and Reporting, and Information Technology and Security.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | ISACA CRISC (Certified in Risk and Information Systems Control) |
| Credential | ISACA CRISC (Certified in Risk and Information Systems Control) |
| Level | Intermediate |
| Practice mock length | ~75 questions |
| Duration | ~240 minutes |
| Passing score | 563 out of 1000 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Governance | ~26% |
| 2 | IT Risk Assessment | ~22% |
| 3 | Risk Response and Reporting | ~32% |
| 4 | Information Technology and Security | ~20% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Governance

- Accountability for outsourced functions stays with the organization; a third party takes on contractual responsibilities but cannot relieve the enterprise of accountability to its stakeholders and regulators.
- The board sets and formally approves the overall risk appetite (reflecting its ultimate accountability), and senior management translates that appetite into measurable risk tolerance ranges for specific objectives and processes.
- In the three lines model, external audit is NOT a line; the three internal lines are operational management, oversight/risk functions, and internal audit, while external audit provides independent assurance from outside.
- The risk owner is accountable for ensuring a specific risk is managed to an acceptable level and for its treatment; the control owner is accountable only for a specific control, so the two roles often rest with different people.
- Persistent resourcing shortfalls should be escalated to leadership with a documented business case, not resolved by quietly reducing risk-work scope or quality.
- Document hierarchy: a policy states intent, a standard specifies mandatory measurable requirements that operationalize the policy, and procedures give step-by-step instructions approved at the department or process-manager level.

### Domain 2 - IT Risk Assessment

- A well-formed IT risk scenario specifies the actor (threat source), the threat type/event, the affected asset, and the timing/duration, giving enough detail to assess likelihood and impact.
- Recovery Time Objective (RTO) is the target duration to restore a process after disruption; Recovery Point Objective (RPO) is tolerable data loss/currency, and Maximum Tolerable Downtime (MTD) is the outer limit RTO must stay within.
- Consolidating multiple critical applications or business units onto a single cloud region, vendor, or key person creates concentration risk, where one failure causes a correlated enterprise-wide impact.
- Current (residual) risk reflects exposure that exists right now under the controls actually operating; a well-designed control that has never been executed fails on operating effectiveness, not design.
- Vulnerability scans give broad technical inventory, architecture reviews reveal design weaknesses, and penetration tests confirm which vulnerabilities are realistically exploitable - together forming a rounded technical picture.
- Risk velocity (how quickly a scenario could hit the organization) is a valid factor for ranking scenarios that have similar likelihood and impact.

### Domain 3 - Risk Response and Reporting

- The four risk response options are mitigate (treat), transfer/share, avoid, and accept; when a control's cost far exceeds the risk reduction, a cheaper alternative or accepting the residual risk is more defensible.
- Control types by function: preventive (stops an event, e.g. pre-hire screening), detective (identifies an event, e.g. a SOC), deterrent (discourages an actor, e.g. warning signage), and corrective; physical controls include fencing, guard patrols, and biometric readers.
- A compensating control is justified only when the primary control is technically infeasible on constrained systems or its cost is clearly disproportionate to the risk reduction achieved.
- A key risk indicator must be measurable - expressible in consistent quantifiable terms that allow comparison across periods - and monitored more frequently than the longer-term strategic risk appetite.
- Continuous control monitoring uses automated testing to provide ongoing assurance about control effectiveness between periodic audit cycles.
- Predefined, objective escalation thresholds (a defined loss amount, control-failure severity, or risk-rating change) remove ambiguity about when an event must be escalated outside the normal cycle.

### Domain 4 - Information Technology and Security

- Contractual data portability and defined exit-assistance provisions directly reduce cloud vendor lock-in by giving a practical path to migrate away from a provider.
- Incident management restores service during an outage, while problem management investigates root cause and drives permanent fixes to prevent recurrence.
- Data should be classified at the point of creation so downstream access, storage, and transmission controls match its true sensitivity from the start.
- Least privilege grants only the access a role requires; a broad department template over-provisions entitlements, which differs from segregation-of-duties concerns over conflicting tasks.
- Shared generic or fixed factory administrator credentials prevent actions from being traced to an individual and let anyone who knows them access every device, undermining accountability at scale.
- Because public cloud infrastructure is multi-tenant, a failure of the logical controls that separate tenants could expose or affect another customer's workload.

## Study tips

- CRISC answers are almost always about accountability and appetite: when a question asks 'who is responsible' or 'what should you do first,' favor the risk owner, senior management, or the board over a technician or a documentation task.
- Distinguish the paired terms the exam loves to test: risk owner vs control owner, appetite vs tolerance, RTO vs RPO vs MTD, incident vs problem management, and inherent vs residual (current) risk.
- When two answers both look correct, pick the one that addresses the root cause or provides decision-useful information to management, not the one that merely restores service or reports a symptom.
- For control questions, first classify by function (preventive, detective, deterrent, corrective) and by type (physical, technical, administrative) before choosing - the wording usually maps cleanly to one category.
- Read every scenario as a business-risk decision, not a purely technical one: the best answer aligns the response with risk appetite, cost-benefit, and stakeholder accountability.

---

Want the full breakdown? See the complete **[ISACA CRISC (Certified in Risk and Information Systems Control) study guide](https://certgrid.app/study-guide/isaca-crisc-certified-in-risk-and-information-systems-control)** and **[free practice questions](https://certgrid.app/practice/isaca-crisc-certified-in-risk-and-information-systems-control)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


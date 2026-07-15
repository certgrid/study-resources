# Red Hat Certified Ansible (EX294-style) - Study Cheatsheet

The Red Hat Certified Ansible exam (EX294-style) validates your ability to automate Linux system administration at scale using Ansible: writing playbooks and roles, managing inventories, templating configuration with Jinja2, handling variables and secrets, and ensuring tasks run idempotently. It is a hands-on, performance-based exam aimed at sysadmins, DevOps engineers, and automation practitioners who manage fleets of systems. Expect to build and run real playbooks against managed nodes rather than answer purely theoretical questions.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | Red Hat Certified Ansible (EX294-style) |
| Credential | Red Hat Certified Ansible (EX294-style) |
| Level | Intermediate |
| Practice mock length | ~50 questions |
| Duration | ~120 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-11 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Ansible Fundamentals | ~19% |
| 2 | Inventory | ~20% |
| 3 | Playbooks and Tasks | ~26% |
| 4 | Variables and Templates | ~20% |
| 5 | Roles and Reuse | ~15% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Ansible Fundamentals

- Ansible is agentless: it manages nodes over SSH (Linux) or WinRM (Windows) with no persistent agent installed on the targets, only Python on the managed node for most modules.
- Idempotency means re-running the same playbook converges to the desired state and reports 'ok' (no changes) when the system is already correct, instead of repeating changes.
- Check mode (ansible-playbook site.yml --check or -C) performs a dry run that reports what would change without actually modifying any host.
- Ad-hoc commands run a single module against hosts without a playbook: ansible <pattern> -m <module> -a '<args>', e.g. ansible all -m ping or ansible all -m ansible.builtin.setup.
- ansible-playbook site.yml runs a full playbook; --syntax-check parses YAML and play structure without connecting; --list-hosts shows which hosts a play would target.
- The forks setting (ansible.cfg [defaults] forks=, or -f on the CLI, default 5) controls how many hosts Ansible configures in parallel.

### Domain 2 - Inventory

- Inventory defines the managed hosts and groups Ansible operates on, plus optional host and group variables, in INI or YAML format.
- Static inventory lists hosts explicitly; dynamic inventory uses plugins (e.g. amazon.aws.aws_ec2, azure_rm) to auto-discover hosts from a cloud or CMDB so the inventory stays accurate as instances change.
- Per-host connection variables are set inline, e.g. web1 ansible_host=10.0.0.5 ansible_port=2222 ansible_user=deploy.
- Groups let you target logically related hosts; a group is declared with [webservers] in INI, and hosts can belong to multiple groups.
- Special built-in groups: 'all' matches every host and 'ungrouped' matches hosts not in any user-defined group.
- Group variables live in group_vars/<group>.yml and host variables in host_vars/<host>.yml, kept alongside the inventory or playbook.

### Domain 3 - Playbooks and Tasks

- A play maps a group of hosts (hosts:) to an ordered set of tasks and roles; a playbook is one or more plays in a YAML list.
- A task invokes a single module (e.g. ansible.builtin.dnf, copy, service) with arguments to perform one idempotent action.
- Handlers are special tasks listed under handlers: that run only when triggered by notify, and only once, at the end of the play (or earlier with meta: flush_handlers).
- Conditionals use when: with a Jinja2 expression (no surrounding {{ }} needed), e.g. when: ansible_os_family == 'RedHat'.
- Loops use loop: (preferred) or the older with_items:; loop_control with label and index_var customizes loop output and indexing.
- Error handling: ignore_errors: true continues past failures, and block/rescue/always provides try-catch-finally semantics around grouped tasks.

### Domain 4 - Variables and Templates

- The ansible.builtin.template module renders a Jinja2 .j2 template using variables and facts to a file on the managed host, with mode/owner/group control.
- Facts are system data gathered by the setup module (OS, IP, memory, etc.); reference them like ansible_facts['os_family'] or ansible_os_family.
- Disable fact gathering with gather_facts: false when not needed, and limit collection with gather_subset (e.g. gather_subset: min or '!all') to speed runs.
- Fact caching (jsonfile or redis cache plugin with a timeout) persists facts between runs so they are not re-gathered every execution.
- Variable precedence (low to high, abbreviated): role defaults < inventory/group_vars < host_vars < play vars < set_fact/registered < extra-vars (-e); -e always wins.
- Put easily overridable tunables in a role's defaults/main.yml (lowest precedence) and internal constants in vars/main.yml (higher precedence).

### Domain 5 - Roles and Reuse

- A role is a reusable, structured bundle of tasks, handlers, variables, templates, and files for one unit of functionality, following a fixed directory layout.
- Standard role layout: tasks/, handlers/, templates/, files/, vars/, defaults/, meta/, and library/, each with a main.yml entry point where applicable.
- defaults/main.yml holds the lowest-precedence default variables meant to be easily overridden; vars/main.yml holds higher-precedence values not meant for casual override.
- Apply roles via the roles: keyword (runs before the play's tasks:), or with import_role / include_role inside tasks.
- import_role is static (parsed at parse time, so its tags and handlers are known up front) while include_role is dynamic (evaluated at runtime, supporting loops and when: on the include itself).
- pre_tasks run before roles, then roles run, then tasks:, then post_tasks; handlers notified anywhere run at the end of the play unless flushed early.

## Study tips

- This is a hands-on exam: practice writing and running real playbooks against managed nodes, not just memorizing facts. Always re-run your playbook to confirm it is idempotent (second run reports zero changes).
- Lean on ansible-doc <module> during practice to recall exact module parameters and examples; knowing how to find syntax fast beats memorizing every option.
- Validate before you commit: use --syntax-check to catch YAML errors and --check (dry run) to preview changes, and watch indentation carefully since YAML is whitespace-sensitive.
- Use fully qualified collection names (e.g. ansible.builtin.copy) to avoid ambiguity, and confirm required collections are installed with ansible-galaxy collection list.
- Master variable precedence and Vault: know that -e extra-vars wins over everything, put overridable values in defaults/, and be ready to create and decrypt vaulted files with the correct vault password.

---

Want the full breakdown? See the complete **[Red Hat Certified Ansible (EX294-style) study guide](https://certgrid.app/study-guide/red-hat-certified-ansible-ex294-style)** and **[free practice questions](https://certgrid.app/practice/red-hat-certified-ansible-ex294-style)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_


# Module 01: Enterprise System & User Environment Setup

## Objective
Design and configure a production-ready Linux environment with 16 employee accounts across 5 departments, implementing role-based access control (RBAC), strict directory permissions, password security policies, and automated user auditing.

---

## User & Group Architecture

Total 16 users created across 5 functional departments:

* **Infrastructure Group (`infra`):** `itadmin01`, `itadmin02`
* **Development Department (`devdept`):** `dev01`, `dev02`, `dev03`, `dev04` | Lead: `devlead`
* **QA Department (`qadept`):** `qa01`, `qa02`, `qa03` | Lead: `qalead`
* **HR Department (`hrdept`):** `hr01`, `hr02` | Manager: `hrmanager`
* **Finance Department (`findept`):** `fin01`, `fin02` | Lead: `financelead`

---

## Directory Hierarchy & Permissions

Base directory path: `/company`

* **`/company/development`**
  * Permissions: `2770` (`root:devdept`)
  * Features: **SGID enabled** for automatic group ownership inheritance on new files. ACL applied for `financelead` user read-only access (`r-x`).
* **`/company/qa`**
  * Permissions: `0770` (`root:qadept`)
  * Features: Restricted to QA team. ACL applied for `devlead` user access (`rwx`).
* **`/company/hr`**
  * Permissions: `0770` (`root:hrdept`)
  * Features: Restricted strictly to HR team.
* **`/company/finance`**
  * Permissions: `0770` (`root:findept`)
  * Features: Restricted to Finance team. ACL applied for `hrmanager` user access (`rwx`).
* **`/company/shared`**
  * Permissions: `1777` (`root:infra`)
  * Features: **Sticky Bit enabled**. Open collaboration directory where users can create files, but only file owners or root can delete them.
* **`/company/backups`**
  * Permissions: `0700` (`root:infra`)
  * Features: Highly restricted backup storage accessible strictly by Root and Infrastructure Team (`infra`).

---

## Security & Administrative Policies

* **Sudo Administrative Privileges:**
  * `%infra` group has full sudo privileges (`ALL=(ALL:ALL) ALL`).
  * Regular department users have zero sudo capabilities.
* **PAM & Password Aging Policies:**
  * Min length 12 characters, complexity enforced via `pam_pwquality`.
  * Password history set to 5 via `pam_pwhistory` (prevents reuse).
  * Max password age set to 45 days (`chage -M 45`), Min age set to 5 days (`chage -m 5`), Warning before expiry set to 7 days (`chage -W 7`).
* **User Lifecycle & Audit:**
  * Immediate offboarding procedure for resigned users (locking account and changing shell to `/usr/sbin/nologin`).
  * Cron job scheduled on 1st of every month running `/usr/local/bin/company_user_audit.sh` to generate the `company_user_audit.txt` report.

---

## Key Linux Concepts Applied

* User & Group Management & Lifecycle
* Standard POSIX Permissions & Access Control Lists (ACLs)
* Special Permissions (SGID, Sticky Bit)
* Sudo RBAC Configuration (`/etc/sudoers.d/`)
* PAM Modules & Password Aging (`chage`)
* Cron Automation & Audit Reporting

---

## Outcome
Successfully deployed and verified an enterprise-grade Linux user and directory access management setup meeting all operational, access control, and security specifications.

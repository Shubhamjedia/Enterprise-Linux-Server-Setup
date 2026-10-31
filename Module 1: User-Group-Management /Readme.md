

# Enterprise Linux RBAC & User Management Setup

A production-grade Linux infrastructure setup managing 16 user accounts across 5 departments with strict Role-Based Access Control (RBAC), ACLs, custom security policies, and automated auditing.

---

## ⚡ Overview & Features

* **16 Users Across 5 Groups:** Infrastructure (`infra`), Development (`devdept`), QA (`qadept`), HR (`hrdept`), and Finance (`findept`).
* **Granular Directory Security:** Custom POSIX permissions, **SGID** (group inheritance), **Sticky Bit** (safe shared storage), and extended **ACLs** for cross-department lead access.
* **Privilege Isolation:** Full `sudo` access restricted to `%infra`; regular users have zero elevated privileges.
* **PAM & Hardened Passwords:** 12+ character complexity, 5-password history retention, and forced 45-day password rotation (`chage`).
* **Automated Auditing:** Scheduled monthly Cron job executing `/usr/local/bin/company_user_audit.sh`.

---

## 📂 Directory Access Map

| Directory | Permissions | Ownership | Special Access & Features |
| :--- | :--- | :--- | :--- |
| `/company/development` | `2770` | `root:devdept` | **SGID** enabled \| ACL: `financelead` (r-x) |
| `/company/qa` | `0770` | `root:qadept` | Restricted \| ACL: `devlead` (rwx) |
| `/company/hr` | `0770` | `root:hrdept` | HR Team strictly |
| `/company/finance` | `0770` | `root:findept` | Restricted \| ACL: `hrmanager` (rwx) |
| `/company/shared` | `1777` | `root:infra` | **Sticky Bit** (Global access, safe deletion) |
| `/company/backups` | `0700` | `root:infra` | Infra & Root access only |

---

## 🛠️ Concepts & Tools Applied
* **Access Control:** POSIX Permissions, `setfacl` / `getfacl`, SGID, Sticky Bit
* **Identity & Security:** PAM (`pam_pwquality`, `pam_pwhistory`), `chage`, `/etc/sudoers.d/`
* **Automation:** Cron, Bash Scripting, User Offboarding (`/usr/sbin/nologin`)

---

## Outcome
Successfully deployed and verified an enterprise-grade Linux user and directory access management setup meeting all operational, access control, and security specifications.

# Module 3 : Requirements & Execution Proofs

Is document mein Module 04 ki har requirement aur uske specific execution proof (screenshot) ka direct mapping hai.

---

### Requirement 1: Complete Project Data Transfer
* **Requirement:** Securely transfer the complete Development project data (`/project/company/developer`) from `server1` to `server 2` and verify that all files copied successfully.
* **Execution Proof:**



---

### Requirement 2: HR Confidential Data Transfer Access Control
* **Requirement:** Restrict HR report transfers so that only `itadmin1` and `itadmin2` can send files to `server 2`, blocking regular department users.
* **Execution Proof:**



---

### Requirement 3: Finance Backup with Permission & Ownership Preservation
* **Requirement:** Create a backup of the Finance department directory on `server 2` while preserving all original Linux permissions, timestamps, and file ownership.
* **Execution Proof:**



---

### Requirement 4: Incremental Synchronization for Updated Files
* **Requirement:** Synchronize only modified files in the Development folder to `server 2` using `rsync` without re-copying unchanged files.
* **Execution Proof:**



---

### Requirement 5: Backup Verification
* **Requirement:** Inspect and verify total transferred files, file size, ownership, permissions, and transfer status on `server 2`.
* **Execution Proof:**



---

### Requirement 6: File Transfer Audit Report
* **Requirement:** Generate the daily transfer report at `/project/company/file_transfer_report.txt` containing Source Server (`server1`), Destination Server (`server 2`), Department, Transfer Method, Transferred Files, Status, and Timestamp.
* **Execution Proof:**



---

### Requirement 7: SSH Key Authentication Enforcement
* **Requirement:** Configure SSH key-based authentication (`ssh-keygen` & `ssh-copy-id`) for `itadmin1` and `itadmin2` to perform SCP, SFTP, and Rsync transfers from `server1` to `server 2` without password prompts.
* **Execution Proof:**

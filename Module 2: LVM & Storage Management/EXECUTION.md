# Module 2: Requirements & Execution Proofs

### Requirement 1: Storage Disk Initialization
* **Requirement:** Initialize the new 5 GB storage disk as a Physical Volume (PV) to add it to the company's storage setup.
* **Execution Proof:**
<img width="1699" height="545" alt="partation" src="https://github.com/user-attachments/assets/759ae37b-c7c9-4fff-845e-47aec548f5a5" />
<img width="1735" height="626" alt="pv create" src="https://github.com/user-attachments/assets/b827c460-641b-4c16-a312-dde413113bb8" />




---

### Requirement 2: Centralized Storage Pool Creation
* **Requirement:** Create a centralized Volume Group named `company_vg` with 5 GB storage capacity that can be expanded in the future.
* **Execution Proof:**
 <img width="1734" height="522" alt="vg creation" src="https://github.com/user-attachments/assets/da8992a9-6d42-43c0-b9b3-59d8e87e3c41" />




---

### Requirement 3: Dedicated Logical Volume Allocation
* **Requirement:** Create separate Logical Volumes (LVs) for each department with the required storage:
  * Development: 1.5 GB (`developer`)
  * QA: 1.0 GB (`QA`)
  * HR: 500 MB (`HR`)
  * Finance: 500 MB (`finance`)
  * Backup: 1.0 GB (`backup`)
* **Execution Proof:**
  <img width="1733" height="596" alt="extenction" src="https://github.com/user-attachments/assets/6b89079f-f861-4b46-ade0-d12dad39af4c" />
  <img width="1720" height="707" alt="lvm listing" src="https://github.com/user-attachments/assets/585ab4ab-1a24-4b3f-b9a5-9faa55c406f8" />




---

### Requirement 4: Persistent File System Mounting
* **Requirement:** Format all logical volumes and add them to `/etc/fstab` so they mount automatically whenever the system restarts.
* **Execution Proof:**
  <img width="1710" height="657" alt="fstab" src="https://github.com/user-attachments/assets/457ead8f-0d0d-440e-a825-bc1873a6d446" />
  <img width="1705" height="606" alt="mount point listing" src="https://github.com/user-attachments/assets/bc185da7-8f9f-4843-9cb3-18acd2613a13" />




---

### Requirement 5: Online Storage Expansion (Development)
* **Requirement:** Increase the Development storage (`developer`) from 1.5 GB to 2.0 GB (+500 MB) live without losing any data or unmounting.
* **Execution Proof:**



---

### Requirement 6: Controlled Storage Reduction (Backup)
* **Requirement:** Safely reduce the Backup storage (`backup`) from 1.0 GB to 500 MB without losing any files or data.
* **Execution Proof:**
 
<img width="1732" height="297" alt="umount" src="https://github.com/user-attachments/assets/c8ea84a6-792a-47e8-93fb-627ec94533f1" />
<img width="1701" height="475" alt="lv reduce" src="https://github.com/user-attachments/assets/95038dd0-b97f-4e0b-8984-bcef165ec1c1" />




---

### Requirement 7: Live Storage Infrastructure Scaling
* **Requirement:** Add a new 1 GB disk to extend `company_vg` without stopping any running services or affecting existing data.
* **Execution Proof:**



---

### Requirement 8: Pre-Upgrade Point-in-Time Snapshot
* **Requirement:** Create an LVM snapshot for the Development volume before a major software upgrade so it can be restored if the upgrade fails.
* **Execution Proof:**

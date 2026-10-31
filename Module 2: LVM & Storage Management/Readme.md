# Enterprise Storage Management & LVM Architecture

A high-availability enterprise storage subsystem built using Logical Volume Management (LVM), featuring dynamic volume scaling, persistent mounts, and point-in-time disaster recovery snapshots.

---

## ⚡ Overview & Features

* **Centralized Storage Pool:** Managed via `company_vg` Volume Group with zero-downtime hot-storage expansion.
* **Dynamic Volume Resizing:** Expanded Development volume (`dev_lv`) live by +500MB and safely reduced Backup volume (`backup_lv`) by -500MB.
* **Persistent Mounts:** All XFS/EXT4 filesystems configured in `/etc/fstab` for automated reboot persistence.
* **Disaster Recovery:** Point-in-time LVM snapshots (`lvcreate -s`) configured for instant rollbacks prior to major deployments.

---

## 📂 Departmental Storage Allocation

| Department | Mount Point | Logical Volume | Initial Size | Updated Size | Management Policy |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Development** | `/company/development` | `dev_lv` | 1.5 GB | **2.0 GB** | Extended (+500 MB) for projects |
| **QA** | `/company/qa` | `qa_lv` | 1.0 GB | 1.0 GB | Persistent mount via `/etc/fstab` |
| **HR** | `/company/hr` | `hr_lv` | 500 MB | 500 MB | Persistent mount via `/etc/fstab` |
| **Finance** | `/company/finance` | `finance_lv` | 500 MB | 500 MB | Persistent mount via `/etc/fstab` |
| **Backup** | `/company/backups` | `backup_lv` | 1.0 GB | **500 MB** | Reduced (-500 MB) for reallocation |

---

## 🛠️ Concepts & Tools Applied
* **LVM Core:** Physical Volumes (PV), Volume Groups (VG), Logical Volumes (LV)
* **Storage Scaling:** `pvcreate`, `vgextend`, `lvextend`, `lvreduce`, `resize2fs` / `xfs_growfs`
* **Disaster Recovery:** LVM Point-in-Time Snapshots (`lvcreate -s`)
* **Persistence & Monitoring:** `/etc/fstab`, `mount`, `df -h`
  

---

## Outcome

Successfully implemented a resilient, scalable Enterprise LVM storage architecture meeting all capacity planning, disaster recovery, dynamic resizing, and persistence requirements.

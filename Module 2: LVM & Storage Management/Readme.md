# Module 02: Enterprise Storage Management & LVM Architecture

## Objective
Design, configure, and maintain a high-availability enterprise storage subsystem using Logical Volume Management (LVM) on Enterprise Linux. The setup establishes centralized storage pooling, dynamic volume resizing (extension and shrinking), persistent filesystem mounting, disaster recovery via point-in-time LVM snapshots, and automated monthly storage auditing.

---

## Storage Architecture & Volume Group Pooling

* **Total Initial Physical Storage:** 5 GB across newly provisioned raw storage disks.
* **Centralized Storage Pool:** `company_vg` Volume Group (5 GB base capacity) designed for live online expansion.
* **Hot-Storage Expansion:** Additional 1 GB raw disk integrated into `company_vg` live with zero service downtime.

---

## Departmental Storage Allocation & Mount Summary

Base Directory Path: `/company`

| Department | Target Mount Point | Logical Volume | Baseline Allocation | Updated Allocation | Policy / Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Development** | `/company/development` | `developer` | 1.5 GB | 2.0 GB | Extended (+500 MB) for new project |
| **QA** | `/company/qa` | `QA` | 1.0 GB | 1.0 GB | Persistent mount via `/etc/fstab` |
| **HR** | `/company/hr` | `HR` | 500 MB | 500 MB | Persistent mount via `/etc/fstab` |
| **Finance** | `/company/finance` | `finance` | 500 MB | 500 MB | Persistent mount via `/etc/fstab` |
| **Backup** | `/company/backups` | `backup` | 1.0 GB | 500 MB | Reduced (-500 MB) to reallocate space |

---

## Technical Specifications & Storage Policies

* **Persistent Filesystem Mounts:** All Logical Volumes formatted with enterprise filesystems (EXT4 / XFS) and mapped in `/etc/fstab` to ensure automatic persistence across system reboots.
* **Online Storage Expansion:** Extended `dev_lv` by 500 MB (`lvextend`) to accommodate new project requirements and resized its filesystem live without data loss or downtime.
* **Controlled Storage Reduction:** Safely reduced `backup_lv` capacity by 500 MB (`lvreduce`) to free up storage space while maintaining complete data integrity.
* **Live Storage Infrastructure Scaling:** Initialized newly acquired 1 GB physical disk (`pvcreate`) and dynamically extended `company_vg` (`vgextend`) with zero impact on running workloads.
* **Disaster Recovery & Snapshots:** Created an LVM point-in-time snapshot (`lvcreate -s`) for the Development volume prior to major software upgrades to enable instant rollbacks on deployment failure.
  
---

## Key Linux Concepts Applied

* LVM Architecture (Physical Volumes, Volume Groups, Logical Volumes)
* Online Filesystem & Volume Resizing (`lvextend`, `lvreduce`, `resize2fs` / `xfs_growfs`)
* Hot Storage Expansion (`pvcreate`, `vgextend`)
* Point-in-Time LVM Snapshots & Disaster Recovery Rollback
* System Persistence & Storage Management (`/etc/fstab`, `mount`, `df -h`)
  

---

## Outcome

Successfully implemented a resilient, scalable Enterprise LVM storage architecture meeting all capacity planning, disaster recovery, dynamic resizing, and persistence requirements.

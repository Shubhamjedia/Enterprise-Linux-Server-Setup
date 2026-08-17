# Module 3 : Secure File Transfer & Cross-Server Sync

## Overview
This project sets up secure file transfer and backup synchronization between two Linux servers: **server1** and **server 2**. The goal is to safely transfer and back up department data from the main server to the backup server using SSH-based tools.

---

## Server Setup & Roles
* **server1:** Enterprise Server storing live department data (`/project/company/`).
* **server 2:** Management/Backup Server where files are backed up.
* **Admins:** `itadmin1` and `itadmin2` (Infrastructure team with transfer permissions).

---

## What Was Configured?

* **SSH Key Authentication:** Configured passwordless access using `ssh-keygen` and `ssh-copy-id` for secure, key-based transfers.
* **Full Data Transfer:** Transferred complete project files from **server1** to **server 2** using `scp` and `rsync`.
* **Access Control:** Restricted HR file transfers so only authorized admins (`itadmin1` & `itadmin2`) can send them, blocking regular users.
* **Preserving Permissions:** Backed up Finance directories while maintaining original file permissions, timestamps, and ownership (`rsync -av`).
* **Incremental Synchronization:** Configured `rsync` to sync only modified files in the Development directory instead of re-copying unchanged data.
* **Transfer Auditing:** Created an audit log at `/project/company/file_transfer_report.txt` to track transfer details, time, and status.

---

## Commands Used

* `ssh-keygen` & `ssh-copy-id` (SSH key setup)
* `scp` / `scp -r` (Secure file and directory copy)
* `sftp` (Secure interactive file transfer)
* `rsync -av` (Incremental sync with permission preservation)

---

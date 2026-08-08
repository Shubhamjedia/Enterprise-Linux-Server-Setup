# Module 01: Requirements & Execution Proofs

Is document mein Module 01 ki har requirement aur uske specific execution proof (screenshot) ka direct mapping hai.

---

### Requirement 1: User & Group Creation
* **Requirement:** Create 16 user accounts across 5 department groups (`infra`, `devdept`, `qadept`, `hrdept`, `findept`).
* **Execution Proof:**
<img width="1920" height="310" alt="Screenshot 2026-08-08 153936" src="https://github.com/user-attachments/assets/713a9204-8533-4f36-8cc9-e503db27741e" />



---

### Requirement 2: Department Directory Isolation
* **Requirement:** Set up main department folders (`development`, `qa`, `hr`, `finance`) with `0770` permissions so users cannot access other departments.
* **Execution Proof:**
<img width="1920" height="209" alt="Screenshot 2026-08-08 174209" src="https://github.com/user-attachments/assets/593f847d-11cf-42b1-b715-4029c2178519" />





---

### Requirement 3: Cross-Department ACLs
* **Requirement:** Give specific team leads access to other departments using ACLs (`devlead` -> QA, `hrmanager` -> Finance, `financelead` -> Development).
* **Execution Proof:**
  <img width="1408" height="319" alt="acl2" src="https://github.com/user-attachments/assets/ab2c501f-a81d-4ad9-9903-b0abf006fcb9" />
  
  <img width="1104" height="704" alt="acl" src="https://github.com/user-attachments/assets/4b88f22b-19b5-4307-9ff8-9fdac88a5c83" />


---

### Requirement 4: Shared Collaboration Directory
* **Requirement:** Configure `/company/shared` with Sticky Bit (`1777`) so everyone can create files, but users cannot delete each other's files.
* **Execution Proof:**
  
<img width="1771" height="257" alt="Screenshot 2026-08-08 174825" src="https://github.com/user-attachments/assets/9ccb6eea-d075-4c6f-a465-c1a942b5a9a1" />



---

### Requirement 5: Restricted Backup Directory
* **Requirement:** Restrict `/company/backups` with `0770` permissions so only the Infrastructure team and root can access it.
* **Execution Proof:**
 <img width="1920" height="169" alt="Screenshot 2026-08-08 175157" src="https://github.com/user-attachments/assets/3b9cf838-3be5-4604-a652-64b37d58f411" />


---

### Requirement 6: Automatic Group Inheritance (SGID)
* **Requirement:** Enable SGID (`2770`) on `/company/development` so new files automatically belong to the `devdept` group.
* **Execution Proof:**

---

### Requirement 7: Role-Based Sudo Access
* **Requirement:** Give full sudo access to the `%infra` group (which includes `itadmin1` and `itadmin2`) and block sudo access for all regular department users.
* **Execution Proof:**
  <img width="1920" height="287" alt="Screenshot 2026-08-08 175455" src="https://github.com/user-attachments/assets/d4dcf967-36a4-404e-b443-01b81f920f58" />


---

### Requirement 8: Password Security & Aging Policy
* **Requirement:** Set password security rules (password expiry every 45 days using `chage`) and integrate PAM (`pam_pwhistory`) to remember and restrict the last 5 past passwords.
* **Execution Proof:**
  <img width="1792" height="303" alt="chage" src="https://github.com/user-attachments/assets/bb833c3b-4a7e-4ec1-9b34-ed4ed518da64" />
  <img width="1678" height="285" alt="pam" src="https://github.com/user-attachments/assets/3934f9ae-cf69-4080-8b59-71b9f38af848" />



---

### Requirement 9: User Lifecycle Management
* **Requirement:** Lock resigned employee accounts (`qa03`) with `/usr/sbin/nologin` shell and set auto-expiration dates for temporary interns.
* **Execution Proof:**

---

### Requirement 10: Automated Monthly Audit Script
* **Requirement:** Schedule `audit.script` using cron to run on the 1st of every month and save reports to `audit.txt`.
* **Execution Proof:**
 <img width="1887" height="203" alt="Screenshot 2026-08-08 181451" src="https://github.com/user-attachments/assets/1c3b8b21-27c8-4c7f-a584-bca581534543" />
 <img width="1876" height="172" alt="Screenshot 2026-08-08 181903" src="https://github.com/user-attachments/assets/bd608077-48ec-4969-b10d-d51e6d808bca" />


 ### Complete Audit Script Logic

```bash
# 1. System Metadata Logic
$(date | awk {'print $1"-"$2"-"$3"-"$4'})$(whoami)

# 2. Total User Logic
$(grep -c -i bash$ /etc/passwd)

# 3. Department Wise User Logic
$(grep -c -i developer /etc/passwd)
$(grep -c -i humanresource /etc/passwd)$(grep -c -i qa /etc/passwd)
$(grep -c -i finance /etc/passwd)$(grep -c -i itadmin /etc/passwd)

# 4. Sudo User Logic
$(grep -i sudouser /etc/passwd | awk -F: {'print $1'})

# 5. Locked User Logic
$(grep -i /sbin/nologin$ /etc/passwd | egrep "developer|humanresource|qa|finance|infra" | awk -F: {'print $1'})

# 6. Password Summary Logic
for i in dev1 dev2 dev3 devlead hr1 hr2 hrmanager fin1 fin2 finlead itadmin1 itadmin2 qa1 qa2 qa3 qalead
do
    chage -l $i | egrep -i "last|password expires|warning"
done

# 7. Home Directory Summary Logic
for i in dev1 dev2 dev3 devlead hr1 hr2 hrmanager fin1 fin2 finlead itadmin1 itadmin2 qa1 qa2 qa3 qalead
do
    grep -i /home/$i /etc/passwd | awk -F: {'print $6'}
done

# 8. User Shell Info Logic
for i in dev1 dev2 dev3 devlead hr1 hr2 hrmanager fin1 fin2 finlead itadmin1 itadmin2 qa1 qa2 qa3 qalead
do
    grep -i ^$i /etc/passwd | awk -F: {'print $7'}
done

Script Output

 ```text
===========================================================
         MONTHLY USER AUDIT REPORT
===========================================================

Report Date    : Sunday-02-August-2026
Generated By   : root

===========================================================
1. USER SUMMARY
===========================================================

   total user : 14

===========================================================
   GROUP WISE 
===========================================================

   user in developer group : 5
   user in hr group : 3
   user in qa group : 4
   user in finance group : 3
   user in itadmin group : 2

===========================================================
2. SUDO USER
===========================================================

   sudo user :
         itadmin1
         itadmin2

===========================================================
3. LOCKED USER
===========================================================

   locked user :
        dev1
        qalead
        hr1
        fin1
        itadmin1

===========================================================
4. PASSWORD SUMMARY
===========================================================

  USER : dev1
Last password change					: Aug 01, 2026
Password expires					: Sep 15, 2026
Number of days of warning before password expires	: 7

.........

===========================================================
5. HOME DIRECTORY SUMMARY
===========================================================
  dev1: /home/dev1
  dev2: /home/dev2
  dev3: /home/dev3
  ...
  qalead: /home/qalead

===========================================================
6. USER SHELL INFO
===========================================================

  dev1: /sbin/nologin
  dev2: /bin/bash
  dev3: /bin/bash
  ...
  qalead: /sbin/nologin

===========================================================


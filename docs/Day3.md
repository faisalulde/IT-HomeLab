# Day 3 - File & Permission Management

## Objective

Practice file management, ownership management, permission configuration, access control verification, NTFS permission administration, and shared folder configuration across Linux and Windows systems to simulate common IT Support and System Administration responsibilities.

---

## Environment

### Ubuntu VM

* Hostname: UBUNTU-ITLAB
* Primary User: employee1

### Windows VM

* Hostname: WIN-ITLAB
* Primary User: adminuser

---

## Ubuntu File Management

### Lab Directory Creation

Created a dedicated lab workspace:

```bash
mkdir ~/IT-LAB
cd ~/IT-LAB
```

### Department Folder Creation

Created departmental folders:

```bash
mkdir HR
mkdir IT
mkdir Public
```

### Verification

Verified folder creation:

```bash
ls
```

Result:

```text
HR  IT  Public
```

---

## Linux Ownership Administration

### Ownership Verification

Checked current ownership:

```bash
ls -l
```

Result:

```text
employee1 employee1 HR
```

### Ownership Modification

Transferred ownership of the HR folder:

```bash
sudo chown employee2 HR
```

### Verification

Verified updated ownership:

```bash
ls -l
```

Result:

```text
employee2 employee1 HR
```

---

## Linux Permission Administration

### HR Folder Permissions

Configured owner-only access:

```bash
chmod 700 HR
```

Permissions:

```text
Owner  : Read Write Execute
Group  : None
Others : None
```

### IT Folder Permissions

Configured owner and group access:

```bash
chmod 770 IT
```

Permissions:

```text
Owner  : Read Write Execute
Group  : Read Write Execute
Others : None
```

### Public Folder Permissions

Configured access for all users:

```bash
chmod 777 Public
```

Permissions:

```text
Owner  : Read Write Execute
Group  : Read Write Execute
Others : Read Write Execute
```

### Verification

Verified permissions:

```bash
ls -ld *
```

Result:

```text
drwx------  HR
drwxrwx---  IT
drwxrwxrwx  Public
```

---

## Linux Access Verification

### Access Testing

Switched to the trainer account:

```bash
su - trainer
```

Attempted access:

```bash
cd /home/employee1/IT-LAB/HR
```

Result:

```text
Permission Denied
```

Attempted access:

```bash
cd /home/employee1/IT-LAB/Public
```

Result:

```text
Permission Denied
```

### Root Cause Analysis

Investigation revealed that the parent directory:

```text
/home/employee1
```

restricted traversal by other users.

As Linux evaluates permissions on every directory within a path, access was denied before reaching the target folders.

### Resolution

Modified parent directory permissions:

```bash
chmod 755 /home/employee1
```

Retested access:

```bash
su - trainer
cd /home/employee1/IT-LAB/Public
```

Result:

```text
Access Successful
```

---

## Windows NTFS Permission Administration

Created folder structure:

```text
C:\IT-LAB
├── HR
├── IT
└── Public
```

### HR Folder Configuration

Attempted to remove inherited permissions from the HR folder.

Windows returned:

```text
You can't remove Authenticated Users because this object is inheriting permissions from its parent.
```

### NTFS Inheritance Resolution

Opened:

```text
HR
→ Properties
→ Security
→ Advanced
→ Disable Inheritance
→ Convert inherited permissions into explicit permissions
```

After disabling inheritance, custom permissions were configured successfully.

### HR Folder Permissions

Assigned:

```text
adminuser
```

Permission Level:

```text
Full Control
```

### IT Folder Permissions

Assigned:

```text
helpdeskuser
```

Permission Level:

```text
Modify
```

### Public Folder Permissions

Assigned:

```text
Users
```

Permission Level:

```text
Full Control
```

---

## Windows Access Verification

### adminuser

Verified access:

```text
HR Folder      -> Accessible
IT Folder      -> Accessible
Public Folder  -> Accessible
```

### manager, helpdeskuser, employee

Verified access:

```text
HR Folder      -> Access Denied
IT Folder      -> Accessible
Public Folder  -> Accessible
```

---

## VirtualBox Shared Folder Configuration

### Host Shared Folder

Created:

```text
F:\IT-SHARED
```

### VirtualBox Configuration

Configured on both virtual machines:

```text
Settings
→ Shared Folders
→ Add Folder
```

Settings:

```text
Folder Path : F:\IT-SHARED
Folder Name : IT-SHARED
Auto Mount  : Enabled
Read Only   : Disabled
```

### Windows Verification

Verified shared folder accessibility through File Explorer.

### Ubuntu Verification

Verified shared folder mount:

```bash
mount | grep vbox
```

Verified contents:

```bash
ls /mnt/shared
cat /mnt/shared/test.txt
```

Confirmed successful access to host-shared files.

---

## Skills Practiced

* Linux File Management
* Linux Ownership Administration
* Linux Permission Administration
* Linux Access Control Verification
* Directory Traversal Permission Analysis
* Windows NTFS Permission Administration
* NTFS Permission Inheritance Management
* Access Control Testing
* VirtualBox Shared Folder Configuration
* Cross-Platform File Sharing

---

## Evidence

Screenshots collected:

* ubuntu-file-permissions.png

![ubuntu-file-permissions.png](/screenshots/ubuntu-file-permissions.png)

* linux-ownership.png

![linux-ownership.png](/screenshots/linux-ownership.png)

* linux-permissions.png

![linux-permissions.png](/screenshots/linux-permissions.png)

* test-access-error.png

![test-access-error.png](/screenshots/test-access-error.png)

* test-access-errorfix.png

![test-access-errorfix.png](/screenshots/test-access-errorfix.png)

* windows-ntfs.png

![windows-ntfs.png](/screenshots/windows-ntfs.png)

* windows-configure-permissions-error.png

![windows-configure-permissions-error.png](/screenshots/windows-configure-permissions-error.png)

* windows-configure-permissions-errorfix.png

![windows-configure-permissions-errorfix.png](/screenshots/windows-configure-permissions-errorfix.png)

* windows-hr-permissions.png

![windows-hr-permissions.png](/screenshots/windows-hr-permissions.png)

* windows-it-permissions.png

![windows-it-permissions.png](/screenshots/windows-it-permissions.png)

* windows-public-permissions.png

![windows-public-permissions.png](/screenshots/windows-public-permissions.png)

* windows-shared-folder.png

![windows-shared-folder.png](/screenshots/windows-shared-folder.png)

* ubuntu-shared-folder.png

![ubuntu-shared-folder.png](/screenshots/ubuntu-shared-folder.png)

---

## Outcome

Successfully configured and tested file ownership, file permissions, access controls, NTFS permissions, permission inheritance, and shared folder functionality across Linux and Windows environments.

These tasks align with real-world responsibilities commonly handled by IT Support, Help Desk, Desktop Support, and Junior System Administration roles, with a focus on file systems and access control management.

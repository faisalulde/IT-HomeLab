# Day 2 - User & Account Administration

## Objective

Practice user, group, and account administration tasks on both Linux and Windows systems to simulate common IT Support and Help Desk responsibilities.

---

## Environment

### Ubuntu VM

* Hostname: UBUNTU-ITLAB
* Primary User: employee1

### Windows VM

* Hostname: WIN-ITLAB
* Primary User: adminuser

---

## Ubuntu User Administration

### User Creation

Created the following users:

| Username  | Purpose                   |
| --------- | ------------------------- |
| employee2 | Standard Employee Account |
| trainer   | Training/Test Account     |

Commands Used:

```bash
sudo adduser employee2
sudo adduser trainer
```

### Verification

Verified successful user creation using:

```bash
cat /etc/passwd | grep employee
```

Result:

* employee1 present
* employee2 present

---

## Ubuntu Group Administration

### Groups Created

| Group Name |
| ---------- |
| support    |
| managers   |

Commands Used:

```bash
sudo addgroup support
sudo addgroup managers
```

### Group Membership Assignment

Added users to the support group:

```bash
sudo usermod -aG support employee2
sudo usermod -aG support trainer
```

### Verification

Verified membership using:

```bash
groups employee2
groups trainer
```

Result:

* employee2 belongs to support group
* trainer belongs to support group

---

## Ubuntu Password Administration

### Password Reset

Changed password for trainer account:

```bash
sudo passwd trainer
```

### Account Lock

Locked account:

```bash
sudo passwd -l trainer
```

Verification:

```bash
sudo passwd -S trainer
```

Result:

```text
trainer L
```

Where:

* L = Locked

### Account Unlock

Unlocked account:

```bash
sudo passwd -u trainer
```

Verification:

```bash
sudo passwd -S trainer
```

Result:

```text
trainer P
```

Where:

* P = Password Active

---

## Windows User Administration

Opened:

```text
Computer Management
→ Local Users and Groups
→ Users
```

### User Creation

Created the following local users:

| Username     | Purpose           |
| ------------ | ----------------- |
| helpdeskuser | Help Desk Account |
| employee     | Employee Account  |
| manager      | Manager Account   |

---

## Windows Account Management

Performed the following account administration tasks:

### Disable User Account

Disabled the employee account using:

```text
Right Click User
→ Properties
→ Account is disabled
```

Verified account status by confirming the disabled account icon.

### Enable User Account

Re-enabled the employee account after testing account disable functionality.

---

## Windows Password Administration

Reset password for:

```text
manager
```

Using:

```text
Computer Management
→ Local Users and Groups
→ Users
→ Right Click User
→ Set Password
```

---

## Windows Group Administration

Created local security group:

| Group Name |
|------------|
| ITSupport |

Using:

```text
Computer Management
→ Local Users and Groups
→ Groups
→ New Group
```

Purpose:

* Practice group-based user administration.
* Simulate real-world role-based access management.

### Verification

Verified the ITSupport group was successfully created in Local Users and Groups.

---

## Skills Practiced

* Linux User Administration
* Linux Group Administration
* Windows User Administration
* Windows Group Administration
* Password Administration
* Account Locking and Unlocking
* Account Enable and Disable Operations
* Group Membership Management
* Local Account Administration

---

## Evidence

Screenshots collected:

* ubuntu-user-administration.png

![ubuntu-user-administration.png](/screenshots/ubuntu-user-administration.png)

* ubuntu-password-management.png

![ubuntu-password-management.png](/screenshots/ubuntu-password-management.png)

* windows-create-users.png

![windows-create-users.png](/screenshots/windows-create-users.png)

* windows-disable-user.png

![windows-disable-user.png](/screenshots/windows-disable-user.png)

* windows-reset-password.png

![windows-reset-password.png](/screenshots/windows-reset-password.png)

* windows-create-group.png

![windows-create-group.png](/screenshots/windows-create-group.png)

---

## Outcome

Successfully performed user and account administration tasks across Linux and Windows environments. Activities included user creation, group creation, group membership management, password administration, account locking and unlocking, account enable and disable operations, and local group administration.

These tasks closely reflect common responsibilities performed by IT Support, Help Desk, and System Administration professionals.

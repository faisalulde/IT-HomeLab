# Access Verification Troubleshooting

## Issue

User:

```text
trainer
```

was unable to access directories within:

```text
/home/employee1/IT-LAB
```

---

## Observed Behavior

### Attempt 1

```bash
cd /home/employee1/IT-LAB/HR
```

Result:

```text
Permission Denied
```

### Attempt 2

```bash
cd /home/employee1/IT-LAB/Public
```

Result:

```text
Permission Denied
```

---

## Investigation

### HR Directory

Permissions:

```text
drwx------
```

Configured using:

```bash
chmod 700 HR
```

Ownership:

```text
employee2
```

Only the owner was permitted access.

### Public Directory

Permissions:

```text
drwxrwxrwx
```

Configured using:

```bash
chmod 777 Public
```

Despite having full permissions, access was still denied.

Further investigation revealed that:

```text
/home/employee1
```

restricted traversal for other users.

Linux evaluates permissions on every directory in the path, not only the destination directory.

---

## Resolution

Modified the parent directory permissions:

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

## Lesson Learned

Linux access control depends on:

1. Target directory permissions.
2. Ownership and group membership.
3. Permissions on all parent directories in the path.

Directory traversal permissions can prevent access even when the destination directory is configured with permissive access rights.

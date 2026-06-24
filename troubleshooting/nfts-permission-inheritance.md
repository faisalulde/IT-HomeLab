# NTFS Permission Inheritance Troubleshooting

## Issue

While configuring NTFS permissions on the HR folder, inherited permissions prevented removal of existing security principals.

Error message:

```text
You can't remove Authenticated Users because this object is inheriting permissions from its parent.
```

---

## Root Cause

The HR folder inherited permissions from its parent directory:

```text
C:\IT-LAB
```

Inherited entries cannot be removed directly until inheritance is disabled.

---

## Resolution

Opened:

```text
HR
→ Properties
→ Security
→ Advanced
```

Selected:

```text
Disable Inheritance
```

Then chose:

```text
Convert inherited permissions into explicit permissions
```

This converted inherited entries into editable permissions.

After conversion, unnecessary groups were removed and custom access control entries were configured.

---

## Verification

Configured:

```text
adminuser
```

Permissions:

```text
Full Control
```

Access testing confirmed:

```text
adminuser      -> Accessible
manager        -> Access Denied
helpdeskuser   -> Access Denied
employee       -> Access Denied
```

---

## Lesson Learned

NTFS permissions are inherited from parent folders by default.

When implementing folder-specific access controls, inheritance may need to be disabled before permissions can be customized.

Understanding NTFS inheritance is essential for Windows system administration and access control management.

Great. **Step 2: `Linux/Files-Permissions.md`**

Open **`Linux → Files-Permissions.md`**, delete everything inside, and paste this clean, GitHub-friendly content:

# Linux Files and Permissions

## 1. Introduction

Linux uses a permission system to control who can access, modify, and execute files and directories.

Understanding file permissions is important for:

* Linux server administration
* Security
* User management
* Application deployment
* Cloud infrastructure

---

## 2. Linux File Structure

Linux organizes files and directories in a hierarchical structure.

The root directory is represented by:

```text
/
```

Some important directories are:

| Directory | Purpose                            |
| --------- | ---------------------------------- |
| `/`       | Root directory                     |
| `/home`   | User home directories              |
| `/etc`    | System configuration files         |
| `/var`    | Logs and variable application data |
| `/tmp`    | Temporary files                    |
| `/usr`    | User applications and utilities    |
| `/opt`    | Optional software                  |
| `/root`   | Home directory of the root user    |
| `/dev`    | Device files                       |
| `/proc`   | Process and system information     |

Example:

```bash
ls /
```

---

## 3. File Types

Linux identifies different types of files using symbols.

Run:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 ubuntu ubuntu 25 Sep 26 15:00 test.txt
drwxr-xr-x 2 ubuntu ubuntu 4096 Sep 26 15:01 documents
```

The first character indicates the file type.

| Symbol | File Type     |
| ------ | ------------- |
| `-`    | Regular file  |
| `d`    | Directory     |
| `l`    | Symbolic link |

---

## 4. Understanding File Permissions

A typical permission string looks like this:

```text
-rwxr-xr--
```

It can be divided into four parts:

```text
-   rwx   r-x   r--
│    │     │     │
│    │     │     └── Others
│    │     └──────── Group
│    └────────────── Owner
└─────────────────── File type
```

### Permission Types

| Permission    | Symbol | Meaning                |
| ------------- | ------ | ---------------------- |
| Read          | `r`    | View/read the file     |
| Write         | `w`    | Modify the file        |
| Execute       | `x`    | Execute the file       |
| No permission | `-`    | Permission not granted |

---

## 5. Owner, Group, and Others

Linux permissions are divided into three categories.

### Owner

The user who owns the file.

### Group

Users who belong to the file's assigned group.

### Others

All other users on the system.

Example:

```text
-rwxr-xr--
```

| Category | Permission |
| -------- | ---------- |
| Owner    | `rwx`      |
| Group    | `r-x`      |
| Others   | `r--`      |

This means:

* Owner can read, write, and execute.
* Group can read and execute.
* Others can only read.

---

# 6. Checking File Permissions

Use:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 ubuntu ubuntu 25 Sep 26 15:00 test.txt
```

The important part is:

```text
-rw-r--r--
```

Here:

```text
-    rw-    r--    r--
│     │      │      │
│     │      │      └── Others
│     │      └───────── Group
│     └──────────────── Owner
└────────────────────── File
```

---

# 7. Changing Permissions with `chmod`

`chmod` means **change mode**.

It is used to change file and directory permissions.

### Example

Create a file:

```bash
touch test.txt
```

Check permissions:

```bash
ls -l test.txt
```

Give the owner execute permission:

```bash
chmod u+x test.txt
```

Check again:

```bash
ls -l test.txt
```

---

## 8. Symbolic Permission Method

The symbolic method uses:

* `u` → User/Owner
* `g` → Group
* `o` → Others
* `a` → All users

### Add Permission

Add write permission for the owner:

```bash
chmod u+w test.txt
```

Add read permission for the group:

```bash
chmod g+r test.txt
```

Add execute permission for everyone:

```bash
chmod a+x test.txt
```

### Remove Permission

Remove write permission from the owner:

```bash
chmod u-w test.txt
```

Remove execute permission from others:

```bash
chmod o-x test.txt
```

---

# 9. Numeric Permission Method

Linux permissions can also be represented using numbers.

| Permission    | Value |
| ------------- | ----: |
| Read (`r`)    |     4 |
| Write (`w`)   |     2 |
| Execute (`x`) |     1 |

The values are added together.

### Examples

| Permission | Calculation | Number |
| ---------- | ----------: | -----: |
| `---`      |           0 |      0 |
| `r--`      |           4 |      4 |
| `-w-`      |           2 |      2 |
| `--x`      |           1 |      1 |
| `rw-`      |       4 + 2 |      6 |
| `r-x`      |       4 + 1 |      5 |
| `rwx`      |   4 + 2 + 1 |      7 |

---

## 10. Common `chmod` Examples

### `chmod 644`

```bash
chmod 644 test.txt
```

Permissions:

```text
rw-r--r--
```

Meaning:

* Owner → Read + Write
* Group → Read
* Others → Read

### `chmod 755`

```bash
chmod 755 script.sh
```

Permissions:

```text
rwxr-xr-x
```

Meaning:

* Owner → Read + Write + Execute
* Group → Read + Execute
* Others → Read + Execute

### `chmod 700`

```bash
chmod 700 private.txt
```

Permissions:

```text
rwx------
```

Only the owner has permissions.

---

# 11. Changing File Ownership

The `chown` command changes the owner of a file or directory.

Syntax:

```bash
sudo chown username filename
```

Example:

```bash
sudo chown ubuntu test.txt
```

Change owner and group:

```bash
sudo chown ubuntu:ubuntu test.txt
```

Check the result:

```bash
ls -l test.txt
```

---

# 12. Changing Group Ownership

The `chgrp` command changes the group associated with a file.

Example:

```bash
sudo chgrp developers test.txt
```

Check:

```bash
ls -l test.txt
```

---

# 13. Directory Permissions

Directories also have read, write, and execute permissions.

### Read (`r`)

Allows a user to list the contents of a directory.

### Write (`w`)

Allows a user to create, delete, or rename files inside the directory, subject to other permission rules.

### Execute (`x`)

Allows a user to access/traverse the directory.

Example:

```bash
mkdir project
ls -ld project
```

The `-d` option displays the directory itself rather than its contents.

---

# 14. Default Permissions and `umask`

`umask` controls the default permissions assigned when new files and directories are created.

Check the current value:

```bash
umask
```

Example:

```text
0022
```

The exact default permissions depend on the system and application, but commonly:

* New files do not receive execute permission by default.
* New directories can receive execute permission.

---

# 15. Special Permissions

Linux also provides special permission bits.

The main special permissions are:

| Permission | Purpose                                                          |
| ---------- | ---------------------------------------------------------------- |
| SUID       | Runs a file with the owner's privileges                          |
| SGID       | Runs with group privileges / affects directory group inheritance |
| Sticky Bit | Restricts deletion of files in shared directories                |

Example:

```bash
ls -ld /tmp
```

You may see a permission similar to:

```text
drwxrwxrwt
```

The `t` represents the sticky bit.

---

# 16. Useful Commands

| Command  | Purpose                           |
| -------- | --------------------------------- |
| `ls -l`  | View file permissions             |
| `ls -ld` | View directory permissions        |
| `chmod`  | Change permissions                |
| `chown`  | Change owner                      |
| `chgrp`  | Change group                      |
| `umask`  | View default permission mask      |
| `stat`   | Display detailed file information |

---

# 17. Practical Exercise

## Step 1 — Create a Practice Directory

```bash
mkdir permissions-practice
cd permissions-practice
```

## Step 2 — Create a File

```bash
touch test.txt
```

Check its permissions:

```bash
ls -l test.txt
```

## Step 3 — Add Content

```bash
nano test.txt
```

Add:

```text
This file is used for Linux permissions practice.
```

Save and exit.

View the file:

```bash
cat test.txt
```

## Step 4 — Change Permissions

Set permission to `644`:

```bash
chmod 644 test.txt
```

Check:

```bash
ls -l test.txt
```

## Step 5 — Change Permission to `600`

```bash
chmod 600 test.txt
```

Check:

```bash
ls -l test.txt
```

Expected permission:

```text
-rw-------
```

## Step 6 — Restore Permission

```bash
chmod 644 test.txt
```

Check again:

```bash
ls -l test.txt
```

---

# 18. Screenshots for Documentation

Take screenshots of the following commands.

### Screenshot 1 — File Permissions

```bash
touch test.txt
ls -l test.txt
```

### Screenshot 2 — Changing Permissions

```bash
chmod 644 test.txt
ls -l test.txt
```

### Screenshot 3 — Numeric Permissions

```bash
chmod 600 test.txt
ls -l test.txt
```

### Screenshot 4 — Ownership

```bash
ls -l test.txt
whoami
```

If you practice `chown`, also show:

```bash
sudo chown ubuntu:ubuntu test.txt
ls -l test.txt
```

---

# 19. Learning Outcome

After completing this section, I should be able to:

* Understand the Linux file system.
* Identify different file types.
* Understand read, write, and execute permissions.
* Understand owner, group, and others.
* Check permissions using `ls -l`.
* Change permissions using `chmod`.
* Understand numeric permissions such as `644`, `755`, and `700`.
* Change file ownership using `chown`.
* Change group ownership using `chgrp`.
* Understand the purpose of `umask`.
* Understand basic special permissions.

---

## Conclusion

Linux file permissions provide an important layer of security.

Understanding ownership and permissions helps administrators control access to files, directories, applications, and system resources.

These concepts will be used later when configuring **Linux users, groups, SSH access, services, and cloud servers**.



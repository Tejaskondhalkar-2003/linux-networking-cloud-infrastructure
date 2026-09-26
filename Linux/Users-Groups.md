# Linux Users and Groups

## 1. Introduction

Linux is a multi-user operating system. Multiple users can access the same Linux system while having different permissions and access levels.

Linux uses **users** and **groups** to control access to files, directories, applications, and system resources.

Understanding users and groups is important for:

* Linux server administration
* Access control
* File permissions
* SSH access
* Cloud server management
* System security

---

# 2. Linux Users

A **user** is an account that can log in to and use a Linux system.

Each user generally has:

* A username
* A user ID (UID)
* A home directory
* A default group
* A login shell
* File permissions

Check the current user:

```bash
whoami
```

Example output:

```text
ubuntu
```

---

# 3. Checking User Information

## `id`

The `id` command displays information about a user.

```bash
id
```

Example:

```text
uid=1000(ubuntu) gid=1000(ubuntu) groups=1000(ubuntu)
```

You can also check another user:

```bash
id ubuntu
```

---

## `who`

Shows users currently logged into the system.

```bash
who
```

---

## `w`

Displays logged-in users and additional information such as what they are doing.

```bash
w
```

---

## `users`

Displays usernames of currently logged-in users.

```bash
users
```

---

# 4. User Configuration Files

Linux stores important user information in system files.

## `/etc/passwd`

Contains basic information about Linux users.

View the file:

```bash
cat /etc/passwd
```

A typical entry looks like:

```text
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
```

The fields represent:

| Field          | Meaning                                |
| -------------- | -------------------------------------- |
| Username       | User's login name                      |
| `x`            | Password information stored separately |
| UID            | User ID                                |
| GID            | Primary Group ID                       |
| Comment        | User description                       |
| Home Directory | User's home directory                  |
| Shell          | Default login shell                    |

---

## `/etc/group`

Contains information about groups.

```bash
cat /etc/group
```

---

## `/etc/shadow`

Stores password-related information in a protected format.

```bash
sudo cat /etc/shadow
```

> **Note:** Access to `/etc/shadow` is restricted because it contains sensitive authentication information.

---

# 5. Creating a User

The `adduser` command can be used to create a new user.

Example:

```bash
sudo adduser testuser
```

Linux will ask for:

* Password
* Full name
* Additional information

You can press **Enter** to skip optional information.

---

## Verify the User

Check whether the user exists:

```bash
id testuser
```

You can also check:

```bash
grep testuser /etc/passwd
```

---

# 6. Switching Users

The `su` command allows you to switch to another user.

```bash
su - testuser
```

Verify the current user:

```bash
whoami
```

Return to the previous user:

```bash
exit
```

---

# 7. Running Commands as Another User

The `sudo` command allows an authorized user to run commands with elevated privileges.

Example:

```bash
sudo whoami
```

Output:

```text
root
```

This means the command was executed with root privileges.

---

# 8. Root User

The **root** user is the Linux administrator account.

Root has very high privileges and can:

* Create or delete users
* Install software
* Change system configuration
* Change file ownership
* Modify permissions
* Start or stop services

Check the current user:

```bash
whoami
```

If the output is:

```text
root
```

you are operating as the root user.

> **Important:** Avoid using root privileges unnecessarily. Use `sudo` only when administrative access is required.

---

# 9. Linux Groups

A **group** is a collection of users.

Groups make it easier to manage permissions for multiple users.

For example, instead of giving permissions to five users individually, you can create a group and give permissions to the group.

---

# 10. Checking Groups

Check the groups of the current user:

```bash
groups
```

You can also check a specific user:

```bash
groups ubuntu
```

Using `id`:

```bash
id ubuntu
```

---

# 11. Creating a Group

Use `groupadd` to create a new group.

Example:

```bash
sudo groupadd developers
```

Check whether the group exists:

```bash
getent group developers
```

---

# 12. Adding a User to a Group

Use `usermod` to add a user to a group.

Example:

```bash
sudo usermod -aG developers testuser
```

### Meaning of the options

| Option | Meaning              |
| ------ | -------------------- |
| `-a`   | Append               |
| `-G`   | Supplementary groups |

The `-aG` combination adds the user to the group without removing the user from existing supplementary groups.

---

## Verify Group Membership

Run:

```bash
groups testuser
```

Or:

```bash
id testuser
```

You should see the `developers` group.

---

# 13. Changing a User's Primary Group

The `usermod` command can also change a user's primary group.

Example:

```bash
sudo usermod -g developers testuser
```

Check:

```bash
id testuser
```

---

# 14. Removing a User from a Group

On Ubuntu, `gpasswd` can be used to remove a user from a supplementary group.

Example:

```bash
sudo gpasswd -d testuser developers
```

Verify:

```bash
groups testuser
```

---

# 15. Deleting a User

Use `userdel` to delete a user.

Example:

```bash
sudo userdel testuser
```

If you also want to remove the user's home directory:

```bash
sudo userdel -r testuser
```

> **Warning:** The `-r` option deletes the user's home directory and its contents. Use it carefully.

---

# 16. Deleting a Group

Use `groupdel` to delete a group.

Example:

```bash
sudo groupdel developers
```

> The group should not be the primary group of an existing user.

---

# 17. User Home Directories

Each normal Linux user generally has a home directory.

For example:

```text
/home/ubuntu
/home/testuser
```

Check the current user's home directory:

```bash
echo $HOME
```

Example:

```text
/home/ubuntu
```

List home directories:

```bash
ls /home
```

---

# 18. User Shell

A shell provides an interface between the user and the Linux operating system.

Common Linux shells include:

* Bash
* Zsh
* Fish
* Sh

Check the current shell:

```bash
echo $SHELL
```

Example:

```text
/bin/bash
```

---

# 19. Checking the Current User

The following commands are useful for identifying the current user:

```bash
whoami
```

```bash
id
```

```bash
groups
```

```bash
echo $HOME
```

---

# 20. Practical Exercise

This exercise demonstrates basic user and group management.

## Step 1 — Create a Test User

```bash
sudo adduser testuser
```

Verify:

```bash
id testuser
```

---

## Step 2 — Create a Group

Create a group called `developers`:

```bash
sudo groupadd developers
```

Verify:

```bash
getent group developers
```

---

## Step 3 — Add the User to the Group

```bash
sudo usermod -aG developers testuser
```

Verify:

```bash
groups testuser
```

---

## Step 4 — Check User Information

```bash
id testuser
```

You should see information about:

* UID
* GID
* Primary group
* Supplementary groups

---

## Step 5 — Switch to the Test User

```bash
su - testuser
```

Check the current user:

```bash
whoami
```

Expected output:

```text
testuser
```

Return to the previous user:

```bash
exit
```

---

## Step 6 — Remove the Test User

After completing the exercise:

```bash
sudo userdel -r testuser
```

---

## Step 7 — Remove the Test Group

```bash
sudo groupdel developers
```

Verify:

```bash
getent group developers
```

If there is no output, the group has been removed.

---

# 21. Useful Commands Reference

| Command        | Purpose                                    |
| -------------- | ------------------------------------------ |
| `whoami`       | Display current username                   |
| `id`           | Display user and group IDs                 |
| `who`          | Show logged-in users                       |
| `w`            | Show logged-in users and activity          |
| `users`        | Show logged-in usernames                   |
| `groups`       | Show group membership                      |
| `adduser`      | Create a user                              |
| `useradd`      | Create a user                              |
| `usermod`      | Modify a user                              |
| `userdel`      | Delete a user                              |
| `groupadd`     | Create a group                             |
| `groupdel`     | Delete a group                             |
| `gpasswd`      | Manage group membership                    |
| `getent group` | Check group information                    |
| `su`           | Switch user                                |
| `sudo`         | Execute a command with elevated privileges |
| `passwd`       | Change a user's password                   |
| `echo $HOME`   | Display home directory                     |
| `echo $SHELL`  | Display current shell                      |

---

# 22. Important Files Reference

| File           | Purpose                        |
| -------------- | ------------------------------ |
| `/etc/passwd`  | Basic user account information |
| `/etc/shadow`  | Password-related information   |
| `/etc/group`   | Group information              |
| `/etc/sudoers` | Sudo configuration             |
| `/home`        | User home directories          |

---

# 23. Screenshots for Documentation

Take screenshots while performing the practical exercise.

### Screenshot 1 — Current User

Run:

```bash
whoami
id
groups
```

---

### Screenshot 2 — Create User

Run:

```bash
sudo adduser testuser
id testuser
```

---

### Screenshot 3 — Create Group

Run:

```bash
sudo groupadd developers
getent group developers
```

---

### Screenshot 4 — Add User to Group

Run:

```bash
sudo usermod -aG developers testuser
groups testuser
```

---

### Screenshot 5 — Switch User

Run:

```bash
su - testuser
whoami
```

Then:

```bash
exit
```

---

### Screenshot 6 — User and Group Information

Run:

```bash
id testuser
```

This screenshot should clearly show the user's UID, GID, and group membership.

---

# 24. Learning Outcome

After completing this section, I should be able to:

* Understand Linux users and groups.
* Check the current logged-in user.
* Create and delete users.
* Create and delete groups.
* Add users to groups.
* Remove users from groups.
* Understand UID and GID.
* Switch between users.
* Understand the purpose of `sudo`.
* Identify important user and group configuration files.
* Understand the relationship between users, groups, and file permissions.

---

## Conclusion

Linux users and groups are an important part of system administration and security.

Users identify individual accounts, while groups allow permissions to be managed for multiple users.

These concepts work together with **Linux file permissions** and will be useful when configuring **SSH access, services, applications, and cloud servers**.


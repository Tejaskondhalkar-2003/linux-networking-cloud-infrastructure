Yes. The previous version had too many sections and code blocks. For a GitHub `.md` file, this cleaner structure will be much easier to read.

Replace the entire content of **`Linux/CLI-Commands.md`** with this:

# Linux CLI Commands

## 1. Introduction

Linux Command Line Interface (CLI) is used to interact with a Linux operating system by entering commands in the terminal.

These commands are commonly used for:

* Navigating directories
* Creating and managing files
* Checking system information
* Managing software
* Checking network connectivity
* Performing basic troubleshooting

---

## 2. Directory Navigation

### `pwd` — Print Working Directory

Displays the current directory.

```bash
pwd
```

**Example:**

```text
/home/ubuntu
```

### `ls` — List Directory Contents

Displays files and directories.

```bash
ls
```

Useful options:

```bash
ls -l    # Detailed listing
ls -a    # Show hidden files
ls -la   # Detailed listing including hidden files
```

### `cd` — Change Directory

Used to move between directories.

```bash
cd /home/ubuntu
```

Go to the parent directory:

```bash
cd ..
```

Go to the user's home directory:

```bash
cd ~
```

---

## 3. Creating Files and Directories

### `mkdir` — Make Directory

Creates a new directory.

```bash
mkdir linux-practice
```

Create multiple directories:

```bash
mkdir folder1 folder2 folder3
```

### `touch` — Create File

Creates an empty file.

```bash
touch example.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt
```

---

## 4. Copying and Moving Files

### `cp` — Copy

Copies files or directories.

```bash
cp example.txt backup.txt
```

Copy a directory:

```bash
cp -r folder1 folder2
```

### `mv` — Move or Rename

Rename a file:

```bash
mv oldname.txt newname.txt
```

Move a file:

```bash
mv example.txt /home/ubuntu/Documents/
```

---

## 5. Removing Files and Directories

### `rm` — Remove

Delete a file:

```bash
rm example.txt
```

Delete a directory and its contents:

```bash
rm -r folder1
```

> **Warning:** Use `rm` carefully because deleted files may not be easily recoverable.

---

## 6. Viewing and Editing Files

### `cat` — Display File Contents

Displays the contents of a file.

```bash
cat example.txt
```

### `less` — View Large Files

Displays a file one page at a time.

```bash
less example.txt
```

Press `q` to exit.

### `head` — Beginning of a File

```bash
head example.txt
```

### `tail` — End of a File

```bash
tail example.txt
```

### `nano` — Text Editor

Used to create or edit text files.

```bash
nano example.txt
```

Useful shortcuts:

| Shortcut   | Action  |
| ---------- | ------- |
| `Ctrl + O` | Save    |
| `Enter`    | Confirm |
| `Ctrl + X` | Exit    |

---

## 7. Searching Files and Text

### `find` — Search for Files

Search for a specific file:

```bash
find /home/ubuntu -name "example.txt"
```

### `grep` — Search Text

Search for text inside a file:

```bash
grep "Linux" example.txt
```

Case-insensitive search:

```bash
grep -i "linux" example.txt
```

---

## 8. System Information

### `whoami`

Displays the currently logged-in user.

```bash
whoami
```

### `hostname`

Displays the system hostname.

```bash
hostname
```

### `uname`

Displays Linux system information.

```bash
uname -a
```

### `date`

Displays the current date and time.

```bash
date
```

### `uptime`

Shows how long the system has been running.

```bash
uptime
```

---

## 9. Disk and Memory Management

### `df` — Disk Space

Displays available disk space.

```bash
df -h
```

The `-h` option displays information in a human-readable format.

### `du` — Directory Size

Displays the size of a directory.

```bash
du -sh folder1
```

### `free` — Memory Usage

Displays RAM and swap memory usage.

```bash
free -h
```

---

## 10. Basic Networking Commands

### `ip addr`

Displays network interfaces and IP addresses.

```bash
ip addr
```

### `ip route`

Displays the routing table.

```bash
ip route
```

### `ping`

Tests network connectivity.

```bash
ping google.com
```

To send only four packets:

```bash
ping -c 4 google.com
```

### `ss`

Displays network connections and listening ports.

```bash
ss -tuln
```

### `curl`

Tests connectivity to a web server.

```bash
curl https://example.com
```

---

## 11. Package Management

Ubuntu uses the `apt` package manager to install and manage software.

### Update Package Information

```bash
sudo apt update
```

### Upgrade Packages

```bash
sudo apt upgrade
```

### Install a Package

Example: Install Nginx.

```bash
sudo apt install nginx
```

### Remove a Package

```bash
sudo apt remove nginx
```

---

## 12. `sudo` Command

`sudo` allows an authorized user to execute commands with administrator privileges.

Example:

```bash
sudo apt update
```

Another example:

```bash
sudo systemctl restart nginx
```

> **Note:** Use `sudo` carefully because administrator commands can modify important system settings.

---

## 13. Command History

### `history`

Displays previously executed commands.

```bash
history
```

You can also press the **Up Arrow** key to access previously executed commands.

---

## 14. Clear the Terminal

### `clear`

Clears the terminal screen.

```bash
clear
```

Keyboard shortcut:

```text
Ctrl + L
```

---

# 15. Command Reference

| Command    | Purpose                                   |
| ---------- | ----------------------------------------- |
| `pwd`      | Show current directory                    |
| `ls`       | List files and directories                |
| `cd`       | Change directory                          |
| `mkdir`    | Create directory                          |
| `touch`    | Create file                               |
| `cp`       | Copy files/directories                    |
| `mv`       | Move or rename                            |
| `rm`       | Delete files/directories                  |
| `cat`      | Display file contents                     |
| `less`     | View files page by page                   |
| `nano`     | Edit files                                |
| `find`     | Search for files                          |
| `grep`     | Search text                               |
| `whoami`   | Show current user                         |
| `hostname` | Show hostname                             |
| `uname`    | Show system information                   |
| `df -h`    | Show disk usage                           |
| `du -sh`   | Show directory size                       |
| `free -h`  | Show memory usage                         |
| `ip addr`  | Show IP addresses                         |
| `ip route` | Show routing table                        |
| `ping`     | Test network connectivity                 |
| `ss`       | Show network connections                  |
| `curl`     | Test web connectivity                     |
| `apt`      | Manage software packages                  |
| `sudo`     | Execute commands with elevated privileges |
| `history`  | Show command history                      |
| `clear`    | Clear terminal                            |

---

# 16. Practical Exercise

The following exercise demonstrates basic Linux CLI operations.

### Step 1 — Create a Practice Directory

```bash
mkdir linux-practice
cd linux-practice
```

### Step 2 — Create a File

```bash
touch test.txt
ls -l
```

### Step 3 — Add Content to the File

Open the file:

```bash
nano test.txt
```

Add:

```text
This is my Linux CLI practice file.
```

Save and exit.

### Step 4 — View the File

```bash
cat test.txt
```

### Step 5 — Copy the File

```bash
cp test.txt backup.txt
ls -l
```

### Step 6 — Rename the Copy

```bash
mv backup.txt backup-test.txt
ls -l
```

### Step 7 — Check System Information

```bash
whoami
hostname
uname -a
```

### Step 8 — Check Network Information

```bash
ip addr
ip route
ping -c 4 google.com
```

### Step 9 — Clean Up

Return to the parent directory:

```bash
cd ..
```

Remove the practice directory:

```bash
rm -r linux-practice
```

---

# 17. Screenshots for Documentation

Take screenshots while performing the practical exercise.

### Screenshot 1 — Directory and File Creation

Show:

```bash
pwd
ls
mkdir linux-practice
cd linux-practice
touch test.txt
ls -l
```

### Screenshot 2 — File Editing and Viewing

Show:

```bash
nano test.txt
cat test.txt
```

### Screenshot 3 — File Operations

Show:

```bash
cp test.txt backup.txt
mv backup.txt backup-test.txt
ls -l
```

### Screenshot 4 — System Information

Show:

```bash
whoami
hostname
uname -a
```

### Screenshot 5 — Network Information

Show:

```bash
ip addr
ip route
ping -c 4 google.com
```

---

# 18. Learning Outcome

After completing this section, I should be able to:

* Navigate the Linux file system.
* Create, copy, move, rename, and delete files.
* Create and manage directories.
* View and edit files using the terminal.
* Search for files and text.
* Check system information.
* Check disk and memory usage.
* Check IP addresses and routing information.
* Test network connectivity.
* Install and manage packages using `apt`.
* Understand the basic use of `sudo`.

---

## Conclusion

Linux CLI commands are an important foundation for Linux administration and cloud infrastructure.

These commands will be used in the next sections for:

* File permissions
* User and group management
* Process and service management
* SSH configuration
* Networking
* Cloud server deployment



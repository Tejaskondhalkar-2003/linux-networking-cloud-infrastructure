
# Linux Processes and Services

## 1. Introduction

A **process** is a running instance of a program or application.

A **service** is a program that runs in the background and provides a specific function to the system or other applications.

Understanding processes and services is important for:

* Linux system administration
* Server monitoring
* Troubleshooting
* Application management
* Cloud infrastructure
* Network services

---

# 2. What is a Process?

A process is a program that is currently running.

For example, when you open a terminal, a shell process is running.

Each process has a unique **Process ID (PID)**.

You can view running processes using:

```bash
ps
```

---

# 3. Viewing Processes

## `ps`

Displays processes associated with the current terminal.

```bash
ps
```

Example:

```text
PID TTY          TIME CMD
1234 pts/0    00:00:00 bash
1250 pts/0    00:00:00 ps
```

---

## `ps aux`

Displays detailed information about running processes.

```bash
ps aux
```

Important columns include:

| Column    | Meaning                          |
| --------- | -------------------------------- |
| `USER`    | User running the process         |
| `PID`     | Process ID                       |
| `%CPU`    | CPU usage                        |
| `%MEM`    | Memory usage                     |
| `STAT`    | Process status                   |
| `START`   | Process start time               |
| `COMMAND` | Command that started the process |

---

# 4. Process IDs

Every running process has a unique Process ID called a **PID**.

Find the PID of a process:

```bash
pgrep bash
```

Or:

```bash
pidof bash
```

You can also search using:

```bash
ps aux | grep bash
```

> **Note:** `grep` may also display the search command itself. This is normal.

---

# 5. `top` Command

`top` provides a real-time view of system processes.

```bash
top
```

It displays:

* CPU usage
* Memory usage
* Running processes
* Process IDs
* System load
* System uptime

To exit `top`:

```text
q
```

---

# 6. `htop` Command

`htop` is an interactive process viewer.

It may not be installed by default.

Install it with:

```bash
sudo apt update
sudo apt install htop
```

Run:

```bash
htop
```

To exit:

```text
F10
```

or press:

```text
q
```

---

# 7. Finding a Process

The `pgrep` command searches for processes by name.

Example:

```bash
pgrep ssh
```

Another example:

```bash
pgrep nginx
```

You can also use:

```bash
ps aux | grep nginx
```

---

# 8. Stopping a Process

The `kill` command sends a signal to a process.

First find the PID:

```bash
pgrep process_name
```

Then use:

```bash
kill PID
```

Example:

```bash
kill 1234
```

> Replace `1234` with the actual PID of the process you want to stop.

---

# 9. Forcefully Stopping a Process

If a process does not stop normally, `kill -9` can terminate it forcefully.

```bash
kill -9 PID
```

Example:

```bash
kill -9 1234
```

> **Warning:** Use `kill -9` carefully. Try a normal `kill` first.

---

# 10. Process Priority

Linux processes have a priority value called **nice value**.

The `nice` command can start a process with a specified priority.

Example:

```bash
nice -n 10 command
```

The `renice` command changes the priority of an existing process.

```bash
renice 10 -p PID
```

> Process priority should be changed carefully, especially on production servers.

---

# 11. Background and Foreground Processes

A command normally runs in the foreground.

Example:

```bash
sleep 60
```

The terminal waits until the command finishes.

Press:

```text
Ctrl + Z
```

to suspend the process.

To continue it in the background:

```bash
bg
```

To bring it back to the foreground:

```bash
fg
```

---

# 12. Running a Command in the Background

Add `&` at the end of a command.

Example:

```bash
sleep 60 &
```

The command runs in the background.

Check background jobs:

```bash
jobs
```

---

# 13. What is a Linux Service?

A service is a program that normally runs in the background.

Examples include:

* SSH server
* Web server
* Database server
* Network services
* Logging services

Modern Ubuntu systems commonly use **systemd** to manage services.

The main command used is:

```bash
systemctl
```

---

# 14. Checking Service Status

Use:

```bash
systemctl status service-name
```

Example:

```bash
systemctl status ssh
```

If Nginx is installed:

```bash
systemctl status nginx
```

The status output can show:

* Whether the service is running
* Whether it starts automatically
* Recent log information
* Process ID
* Service state

---

# 15. Starting a Service

Start a service using:

```bash
sudo systemctl start service-name
```

Example:

```bash
sudo systemctl start nginx
```

Check its status:

```bash
systemctl status nginx
```

---

# 16. Stopping a Service

Stop a service using:

```bash
sudo systemctl stop service-name
```

Example:

```bash
sudo systemctl stop nginx
```

Check:

```bash
systemctl status nginx
```

---

# 17. Restarting a Service

Restart a service using:

```bash
sudo systemctl restart service-name
```

Example:

```bash
sudo systemctl restart nginx
```

Restarting is commonly used after changing a service configuration.

---

# 18. Reloading a Service

Some services support configuration reloads without completely restarting the service.

Example:

```bash
sudo systemctl reload nginx
```

A reload is useful when configuration changes need to be applied while minimizing service interruption.

---

# 19. Enabling a Service at Boot

To automatically start a service when the system boots:

```bash
sudo systemctl enable service-name
```

Example:

```bash
sudo systemctl enable nginx
```

---

# 20. Disabling a Service at Boot

To prevent a service from automatically starting at boot:

```bash
sudo systemctl disable service-name
```

Example:

```bash
sudo systemctl disable nginx
```

---

# 21. Checking Whether a Service is Enabled

Use:

```bash
systemctl is-enabled service-name
```

Example:

```bash
systemctl is-enabled nginx
```

Possible output:

```text
enabled
```

or:

```text
disabled
```

---

# 22. Checking Whether a Service is Active

Use:

```bash
systemctl is-active service-name
```

Example:

```bash
systemctl is-active nginx
```

Possible output:

```text
active
```

or:

```text
inactive
```

---

# 23. Listing Running Services

To list active services:

```bash
systemctl list-units --type=service --state=running
```

This can be useful when troubleshooting a Linux server.

---

# 24. Listing Failed Services

To find services that have failed:

```bash
systemctl --failed
```

This is a useful troubleshooting command.

---

# 25. Viewing Service Logs

Linux services commonly generate logs that can be viewed using `journalctl`.

View logs for a service:

```bash
sudo journalctl -u service-name
```

Example:

```bash
sudo journalctl -u ssh
```

View recent logs:

```bash
sudo journalctl -u ssh -n 50
```

Follow new log entries in real time:

```bash
sudo journalctl -u ssh -f
```

Press:

```text
Ctrl + C
```

to stop following the logs.

---

# 26. Process vs Service

| Process                             | Service                                 |
| ----------------------------------- | --------------------------------------- |
| A running instance of a program     | Background program providing a function |
| Has a PID                           | Usually managed by a service manager    |
| Can run in foreground or background | Usually runs in the background          |
| Can be managed using `kill`         | Commonly managed using `systemctl`      |
| Example: `bash`, `python`           | Example: `ssh`, `nginx`                 |

---

# 27. Useful Process Commands

| Command   | Purpose                                |
| --------- | -------------------------------------- |
| `ps`      | Show current processes                 |
| `ps aux`  | Show detailed process information      |
| `top`     | Monitor processes in real time         |
| `htop`    | Interactive process monitor            |
| `pgrep`   | Find process IDs                       |
| `pidof`   | Find process IDs by program name       |
| `kill`    | Send a signal to a process             |
| `kill -9` | Forcefully terminate a process         |
| `jobs`    | Show shell background jobs             |
| `bg`      | Continue a suspended job in background |
| `fg`      | Bring a background job to foreground   |
| `nice`    | Start a process with a priority        |
| `renice`  | Change process priority                |

---

# 28. Useful Service Commands

| Command                | Purpose                         |
| ---------------------- | ------------------------------- |
| `systemctl status`     | Check service status            |
| `systemctl start`      | Start a service                 |
| `systemctl stop`       | Stop a service                  |
| `systemctl restart`    | Restart a service               |
| `systemctl reload`     | Reload service configuration    |
| `systemctl enable`     | Enable service at boot          |
| `systemctl disable`    | Disable service at boot         |
| `systemctl is-active`  | Check if service is active      |
| `systemctl is-enabled` | Check if service starts at boot |
| `systemctl --failed`   | Show failed services            |
| `journalctl`           | View system/service logs        |

---

# 29. Practical Exercise

## Step 1 — View Running Processes

Run:

```bash
ps
```

Then:

```bash
ps aux
```

---

## Step 2 — Monitor Processes

Run:

```bash
top
```

Observe:

* CPU usage
* Memory usage
* Process IDs
* Running processes

Exit using:

```text
q
```

---

## Step 3 — Create a Background Process

Run:

```bash
sleep 60 &
```

Check the background job:

```bash
jobs
```

You can also find it using:

```bash
pgrep sleep
```

---

## Step 4 — Stop the Practice Process

Find the PID:

```bash
pgrep sleep
```

Then stop it:

```bash
kill PID
```

Replace `PID` with the number returned by the previous command.

---

# 30. Practical Service Exercise

Ubuntu normally has an SSH service when an SSH server is installed.

Check the SSH service:

```bash
systemctl status ssh
```

If SSH is not installed and you are working on a practice VM, you can install it with:

```bash
sudo apt update
sudo apt install openssh-server
```

Then check:

```bash
systemctl status ssh
```

---

## Start SSH

```bash
sudo systemctl start ssh
```

Check:

```bash
systemctl is-active ssh
```

---

## Enable SSH at Boot

```bash
sudo systemctl enable ssh
```

Check:

```bash
systemctl is-enabled ssh
```

---

## View SSH Logs

```bash
sudo journalctl -u ssh -n 50
```

---

# 31. Nginx Service Practice

If you want to practice with a web server, install Nginx:

```bash
sudo apt update
sudo apt install nginx
```

Check the service:

```bash
systemctl status nginx
```

Start Nginx:

```bash
sudo systemctl start nginx
```

Check:

```bash
systemctl is-active nginx
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

View Nginx logs:

```bash
sudo journalctl -u nginx -n 50
```

> Nginx will be useful later when we deploy a service on the Ubuntu server.

---

# 32. Screenshots for Documentation

Take screenshots while performing the practical exercises.

### Screenshot 1 — Running Processes

Run:

```bash
ps
ps aux
```

---

### Screenshot 2 — Process Monitoring

Run:

```bash
top
```

Take a screenshot showing the running processes and system resource information.

Exit using:

```text
q
```

---

### Screenshot 3 — Background Process

Run:

```bash
sleep 60 &
jobs
pgrep sleep
```

---

### Screenshot 4 — SSH Service

Run:

```bash
systemctl status ssh
systemctl is-active ssh
systemctl is-enabled ssh
```

---

### Screenshot 5 — Service Logs

Run:

```bash
sudo journalctl -u ssh -n 20
```

---

### Screenshot 6 — Nginx Service

If Nginx is installed, run:

```bash
systemctl status nginx
systemctl is-active nginx
```

---

# 33. Learning Outcome

After completing this section, I should be able to:

* Understand what a Linux process is.
* Understand Process IDs (PIDs).
* View running processes.
* Monitor CPU and memory usage.
* Find processes using `pgrep`.
* Stop processes using `kill`.
* Run commands in the background.
* Understand Linux services.
* Manage services using `systemctl`.
* Start, stop, restart, and reload services.
* Enable services at system boot.
* Check failed services.
* View service logs using `journalctl`.
* Perform basic process and service troubleshooting.

---

## Conclusion

Processes and services are essential components of a Linux server.

Processes represent running programs, while services provide background functionality such as SSH and web hosting.

Understanding how to monitor and manage them is important for **Linux administration, troubleshooting, networking, and cloud infrastructure**.

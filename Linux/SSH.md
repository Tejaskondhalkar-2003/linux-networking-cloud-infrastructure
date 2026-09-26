# Linux SSH

## 1. Introduction

**SSH (Secure Shell)** is a network protocol used to securely connect to and manage a remote computer over a network.

SSH is commonly used for:

* Remote Linux server administration
* Cloud server management
* Secure file transfers
* Running commands on remote servers
* Managing applications and services
* Troubleshooting remote systems

SSH normally uses **TCP port 22**.

---

# 2. How SSH Works

SSH uses a client-server model.

```text
SSH Client                         SSH Server
   │                                  │
   │──── Connection Request ─────────>│
   │                                  │
   │<──── Authentication ────────────>│
   │                                  │
   │──── Encrypted Commands ─────────>│
   │                                  │
   │<──── Command Output ─────────────│
```

### SSH Client

The computer from which you connect.

Example:

```bash
ssh username@server-ip
```

### SSH Server

The remote Linux machine accepting SSH connections.

The SSH server is commonly provided by **OpenSSH Server**.

---

# 3. SSH Port

The default SSH port is:

```text
TCP 22
```

Check whether SSH is listening:

```bash
sudo ss -tuln | grep :22
```

Example:

```text
LISTEN 0 128 0.0.0.0:22 0.0.0.0:*
```

> The SSH port can be changed, but TCP port 22 is the standard default.

---

# 4. Installing OpenSSH Server

On Ubuntu, install the SSH server using:

```bash
sudo apt update
sudo apt install openssh-server
```

Check the SSH service:

```bash
systemctl status ssh
```

If the service is running, you should see:

```text
Active: active (running)
```

---

# 5. Starting SSH

If the SSH service is not running:

```bash
sudo systemctl start ssh
```

Check:

```bash
systemctl status ssh
```

---

# 6. Enabling SSH at Boot

To automatically start SSH when the server boots:

```bash
sudo systemctl enable ssh
```

Check:

```bash
systemctl is-enabled ssh
```

Expected output:

```text
enabled
```

---

# 7. Checking SSH Status

Use:

```bash
systemctl status ssh
```

You can also check whether it is active:

```bash
systemctl is-active ssh
```

Expected output:

```text
active
```

---

# 8. Finding the Server IP Address

Use:

```bash
ip addr
```

Look for an address such as:

```text
192.168.1.10
```

You can also use:

```bash
hostname -I
```

Example:

```text
192.168.1.10
```

The exact IP address depends on your network or cloud environment.

---

# 9. Connecting to a Remote Server

The basic SSH syntax is:

```bash
ssh username@server-ip
```

Example:

```bash
ssh ubuntu@192.168.1.10
```

Replace:

* `ubuntu` with the remote username.
* `192.168.1.10` with the actual server IP address.

---

# 10. SSH with a Custom Port

If SSH is running on a port other than 22, use the `-p` option.

```bash
ssh -p 2222 username@server-ip
```

Example:

```bash
ssh -p 2222 ubuntu@192.168.1.10
```

---

# 11. First-Time SSH Connection

When connecting to a server for the first time, SSH may display a message asking whether you trust the server's host key.

Example:

```text
The authenticity of host '192.168.1.10' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

If the server identity has been verified, enter:

```text
yes
```

SSH then stores the server's host key locally.

---

# 12. SSH Password Authentication

If password authentication is enabled, SSH asks for the user's password.

Example:

```bash
ssh ubuntu@192.168.1.10
```

You may see:

```text
ubuntu@192.168.1.10's password:
```

Enter the password.

> Passwords are not displayed while typing in the terminal. This is normal.

---

# 13. SSH Key Authentication

SSH keys provide an alternative to password authentication.

An SSH key pair contains:

* **Private key**
* **Public key**

The private key remains on the client.

The public key is placed on the server.

```text
SSH Client                         SSH Server
   │                                  │
   │ Private Key                      │ Public Key
   │     🔑                           │ 🔐
   │                                  │
   └────── Secure Authentication ────┘
```

> Never share your private SSH key.

---

# 14. Generate an SSH Key Pair

On the client machine:

```bash
ssh-keygen -t ed25519
```

You can press **Enter** to accept the default file location.

The keys are normally stored under:

```text
~/.ssh/
```

Check the files:

```bash
ls -la ~/.ssh/
```

You may see:

```text
id_ed25519
id_ed25519.pub
```

### Important

```text
id_ed25519
```

is the **private key**.

```text
id_ed25519.pub
```

is the **public key**.

Never share the private key.

---

# 15. Copying the Public Key to the Server

The `ssh-copy-id` command can copy your public key to a remote server.

```bash
ssh-copy-id username@server-ip
```

Example:

```bash
ssh-copy-id ubuntu@192.168.1.10
```

After successful configuration, you can connect using the SSH key.

```bash
ssh ubuntu@192.168.1.10
```

---

# 16. SSH Configuration File

The SSH server configuration file is:

```text
/etc/ssh/sshd_config
```

View the file:

```bash
sudo nano /etc/ssh/sshd_config
```

Before making changes, it is a good practice to create a backup:

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup
```

---

# 17. Checking SSH Configuration

Before restarting SSH after configuration changes, check the configuration syntax:

```bash
sudo sshd -t
```

If there is no output, the configuration syntax is generally valid.

> Always check the configuration before restarting SSH, especially when working on a remote server.

---

# 18. Restarting SSH

After making a valid configuration change:

```bash
sudo systemctl restart ssh
```

Check:

```bash
systemctl status ssh
```

---

# 19. SSH Logs

SSH activity can be inspected using `journalctl`.

View recent SSH logs:

```bash
sudo journalctl -u ssh -n 50
```

Follow SSH logs in real time:

```bash
sudo journalctl -u ssh -f
```

Stop following the logs:

```text
Ctrl + C
```

---

# 20. Testing SSH Port Connectivity

You can check whether TCP port 22 is reachable.

Using `nc`:

```bash
nc -zv server-ip 22
```

Example:

```bash
nc -zv 192.168.1.10 22
```

If `nc` is not installed:

```bash
sudo apt install netcat-openbsd
```

---

# 21. Checking Listening Ports

Use:

```bash
sudo ss -tuln
```

To specifically check SSH:

```bash
sudo ss -tuln | grep :22
```

---

# 22. Disconnecting from SSH

To close an SSH session:

```bash
exit
```

You can also press:

```text
Ctrl + D
```

---

# 23. SSH File Transfer

SSH can also be used for secure file transfers.

## `scp`

`scp` stands for **Secure Copy Protocol**.

Copy a local file to a remote server:

```bash
scp test.txt username@server-ip:/home/username/
```

Example:

```bash
scp test.txt ubuntu@192.168.1.10:/home/ubuntu/
```

Copy a remote file to the local machine:

```bash
scp username@server-ip:/home/username/test.txt .
```

---

# 24. `sftp`

SFTP provides an interactive secure file transfer session.

Connect to a server:

```bash
sftp username@server-ip
```

Example:

```bash
sftp ubuntu@192.168.1.10
```

Useful SFTP commands:

| Command | Purpose                 |
| ------- | ----------------------- |
| `ls`    | List remote files       |
| `pwd`   | Show remote directory   |
| `cd`    | Change remote directory |
| `get`   | Download a file         |
| `put`   | Upload a file           |
| `exit`  | Close SFTP session      |

Example:

```bash
get test.txt
```

Upload:

```bash
put test.txt
```

---

# 25. SSH Security Practices

When managing an SSH server:

* Use strong passwords when password authentication is enabled.
* Prefer SSH key authentication where appropriate.
* Never share private SSH keys.
* Keep Ubuntu and OpenSSH updated.
* Use a firewall to restrict unnecessary ports.
* Avoid logging in as root directly when possible.
* Give users only the permissions they need.
* Monitor SSH authentication logs.
* Verify server identity before accepting a new host key.

---

# 26. SSH and Firewall

If a firewall is enabled, SSH must be allowed before connecting remotely.

For Ubuntu's UFW firewall:

```bash
sudo ufw allow ssh
```

Check firewall status:

```bash
sudo ufw status
```

You may see:

```text
22/tcp    ALLOW
```

> On a cloud server, network access may also be controlled by the cloud provider's security rules or security groups.

---

# 27. SSH Troubleshooting

## Problem 1 — Connection Refused

Check whether SSH is running:

```bash
systemctl status ssh
```

Check port 22:

```bash
sudo ss -tuln | grep :22
```

---

## Problem 2 — Connection Timed Out

Possible areas to check:

1. Server IP address
2. Network connectivity
3. Firewall
4. Cloud security rules
5. SSH port
6. Server availability

Test connectivity:

```bash
ping server-ip
```

---

## Problem 3 — Permission Denied

Check:

* Username
* Password
* SSH key
* User permissions
* SSH server configuration

Check SSH logs:

```bash
sudo journalctl -u ssh -n 50
```

---

## Problem 4 — SSH Service Not Found

Check whether OpenSSH Server is installed:

```bash
dpkg -l | grep openssh-server
```

Install if necessary:

```bash
sudo apt update
sudo apt install openssh-server
```

---

# 28. Useful SSH Commands Reference

| Command                 | Purpose                     |
| ----------------------- | --------------------------- |
| `ssh user@ip`           | Connect to a remote server  |
| `ssh -p PORT user@ip`   | Connect using a custom port |
| `ssh-keygen`            | Generate SSH keys           |
| `ssh-copy-id`           | Copy public key to a server |
| `scp`                   | Securely copy files         |
| `sftp`                  | Secure file transfer        |
| `systemctl status ssh`  | Check SSH service           |
| `systemctl start ssh`   | Start SSH                   |
| `systemctl restart ssh` | Restart SSH                 |
| `systemctl enable ssh`  | Enable SSH at boot          |
| `ss -tuln`              | Show listening ports        |
| `journalctl -u ssh`     | View SSH logs               |
| `sshd -t`               | Check SSH configuration     |
| `exit`                  | Close SSH session           |

---

# 29. Practical Exercise

## Step 1 — Check SSH Installation

```bash
dpkg -l | grep openssh-server
```

If it is not installed:

```bash
sudo apt update
sudo apt install openssh-server
```

---

## Step 2 — Check SSH Service

```bash
systemctl status ssh
```

Then:

```bash
systemctl is-active ssh
```

---

## Step 3 — Check SSH Port

```bash
sudo ss -tuln | grep :22
```

---

## Step 4 — Find the Server IP

```bash
hostname -I
```

or:

```bash
ip addr
```

---

## Step 5 — Test SSH Locally

On a practice Ubuntu server, you can test the SSH service locally:

```bash
ssh localhost
```

If prompted to confirm the host, verify the server identity and enter `yes` if appropriate.

After connecting:

```bash
whoami
hostname
```

Then disconnect:

```bash
exit
```

---

## Step 6 — Generate an SSH Key

On your client machine:

```bash
ssh-keygen -t ed25519
```

Check:

```bash
ls -la ~/.ssh/
```

---

# 30. Screenshots for Documentation

Take screenshots while performing the practical exercise.

### Screenshot 1 — SSH Installation and Status

Show:

```bash
dpkg -l | grep openssh-server
systemctl status ssh
```

---

### Screenshot 2 — SSH Port

Show:

```bash
sudo ss -tuln | grep :22
```

The screenshot should show SSH listening on TCP port 22 if the service is configured with the default port.

---

### Screenshot 3 — Server IP

Show:

```bash
hostname -I
```

or:

```bash
ip addr
```

---

### Screenshot 4 — SSH Local Connection

Show:

```bash
ssh localhost
```

Then:

```bash
whoami
hostname
```

Finally:

```bash
exit
```

---

### Screenshot 5 — SSH Key Generation

Show:

```bash
ssh-keygen -t ed25519
ls -la ~/.ssh/
```

**Do not expose the contents of your private key in the screenshot.**

---

### Screenshot 6 — SSH Logs

Show:

```bash
sudo journalctl -u ssh -n 20
```

---

# 31. Learning Outcome

After completing this section, I should be able to:

* Explain what SSH is.
* Understand the SSH client-server model.
* Identify the default SSH port.
* Install OpenSSH Server.
* Start and enable the SSH service.
* Check SSH service status.
* Find a Linux server's IP address.
* Connect to a remote Linux server using SSH.
* Understand password and key-based authentication.
* Generate an SSH key pair.
* Understand public and private SSH keys.
* Transfer files using `scp` and `sftp`.
* Check SSH ports and logs.
* Perform basic SSH troubleshooting.
* Apply basic SSH security practices.

---

## Conclusion

SSH is one of the most important tools for managing Linux servers remotely.

It provides secure remote access and is widely used in **Linux administration, cloud computing, networking, DevOps, and server management**.

The SSH knowledge from this section will be used later when connecting to and managing the **Ubuntu cloud server**.


# Linux, Networking & Cloud Infrastructure

## Project Overview

This project demonstrates practical learning and hands-on implementation of **Linux administration, networking fundamentals, and cloud infrastructure**.

The project covers Linux command-line operations, file permissions, users and groups, processes, services, SSH, IP addressing, DNS, ports, firewalls, cloud security groups, and Linux server deployment.

---

## Objectives

The main objectives of this project are:

* Learn Linux command-line operations
* Understand Linux files and permissions
* Manage users and groups
* Understand processes and services
* Configure and use SSH
* Understand IP addressing
* Learn basic DNS concepts
* Understand network ports
* Configure a Linux firewall
* Understand cloud security groups
* Deploy a Linux server
* Deploy and test a web service
* Practice basic troubleshooting

---

# Project Structure

```text
.
├── Cloud/
│   ├── Linux-Server-Deployment.md
│   └── Security-Groups.md
│
├── Linux/
│   ├── CLI-Commands.md
│   ├── Files-Permissions.md
│   ├── Processes-Services.md
│   ├── SSH.md
│   └── Users-Groups.md
│
├── Networking/
│   ├── DNS.md
│   ├── Firewall.md
│   ├── IP-Addressing.md
│   └── Ports.md
│
├── screenshots/
│   └── README.md
│
└── README.md
```

---

# Linux

## 1. Linux CLI Commands

File:

`Linux/CLI-Commands.md`

Topics covered:

* Directory navigation
* File and directory creation
* Copying and moving files
* Removing files
* Viewing files
* Searching
* System information
* Disk and memory information
* Basic networking commands
* Package management

---

## 2. Files and Permissions

File:

`Linux/Files-Permissions.md`

Topics covered:

* Linux file system
* File types
* Read, write, and execute permissions
* File ownership
* `chmod`
* `chown`
* `chgrp`
* `umask`
* Special permissions

---

## 3. Users and Groups

File:

`Linux/Users-Groups.md`

Topics covered:

* Linux users
* Root user
* User management
* Groups
* Adding and removing users
* Adding users to groups
* Important Linux account files

---

## 4. Processes and Services

File:

`Linux/Processes-Services.md`

Topics covered:

* Processes
* Process IDs
* `ps`
* `top`
* `kill`
* Background processes
* systemd
* `systemctl`
* `journalctl`
* Service management

---

## 5. SSH

File:

`Linux/SSH.md`

Topics covered:

* SSH fundamentals
* SSH client/server model
* SSH connection
* SSH keys
* OpenSSH
* SSH security
* SCP and SFTP
* SSH troubleshooting

---

# Networking

## 6. IP Addressing

File:

`Networking/IP-Addressing.md`

Topics covered:

* IPv4
* IPv6
* Private IP
* Public IP
* Static and dynamic IP
* DHCP
* Subnet masks
* Default gateway
* Basic network troubleshooting

---

## 7. DNS

File:

`Networking/DNS.md`

Topics covered:

* DNS fundamentals
* DNS resolution
* DNS records
* `nslookup`
* `dig`
* DNS troubleshooting

---

## 8. Network Ports

File:

`Networking/Ports.md`

Topics covered:

* Network ports
* TCP and UDP
* Common ports
* Listening ports
* `ss`
* `nc`
* Port troubleshooting

---

## 9. Firewall

File:

`Networking/Firewall.md`

Topics covered:

* Firewall fundamentals
* UFW
* Allowing ports
* Blocking ports
* Firewall rules
* Firewall troubleshooting

---

# Cloud

## 10. Cloud Security Groups

File:

`Cloud/Security-Groups.md`

Topics covered:

* Security groups
* Inbound rules
* Outbound rules
* Network access control
* Least privilege
* Security group troubleshooting

---

## 11. Linux Server Deployment

File:

`Cloud/Linux-Server-Deployment.md`

The practical deployment includes:

```text
Create VM
    ↓
Configure Network
    ↓
Configure Security Group
    ↓
Connect using SSH
    ↓
Update Linux
    ↓
Configure Firewall
    ↓
Install Nginx
    ↓
Test Web Server
```

---

# Practical Implementation

The project includes hands-on Linux server deployment.

The deployed server was used to practice:

```text
Linux
Networking
SSH
Firewall
Cloud Security
Web Server
Troubleshooting
```

---

# Technologies and Tools

The project uses:

* Linux / Ubuntu
* Bash
* SSH
* IP networking
* DNS
* TCP/IP
* UFW
* Cloud Virtual Machine
* Cloud Security Groups
* Nginx
* GitHub

---

# Important Commands

Some of the commands used in this project include:

```bash
pwd
ls
cd
mkdir
touch
cp
mv
rm
cat
grep
find
```

Linux administration:

```bash
chmod
chown
chgrp
useradd
usermod
ps
top
kill
systemctl
journalctl
```

Networking:

```bash
ip addr
ip route
ip link
ping
ss
nslookup
dig
curl
```

Firewall:

```bash
sudo ufw status
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

Server deployment:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install nginx -y
sudo systemctl status nginx
curl http://localhost
```

---

# Security Practices

During this project, the following security practices were followed:

* Use SSH for secure remote administration
* Avoid exposing unnecessary ports
* Use firewall rules
* Use cloud security groups
* Follow the principle of least privilege
* Keep Linux packages updated
* Do not upload private keys
* Do not upload passwords or API keys
* Avoid exposing sensitive credentials in screenshots

---

# Troubleshooting Approach

A basic troubleshooting approach used in this project:

```text
Identify the problem
       ↓
Check service status
       ↓
Check IP configuration
       ↓
Check routing
       ↓
Check listening ports
       ↓
Check firewall
       ↓
Check cloud security rules
       ↓
Test connectivity
       ↓
Check logs
```

Useful commands:

```bash
systemctl status <service>
ip addr
ip route
ss -tuln
sudo ufw status
ping <IP>
curl <URL>
journalctl
```

---

# Screenshots

Practical screenshots are stored in:

```text
screenshots/
```

The screenshots demonstrate:

* Linux commands
* IP configuration
* DNS testing
* Network ports
* Firewall configuration
* Security group configuration
* SSH connection
* Linux server deployment
* Nginx web server

---

# Learning Outcomes

After completing this project, I gained practical understanding of:

* Linux command-line administration
* Linux permissions
* User and group management
* Process and service management
* SSH
* IP addressing
* DNS
* Network ports
* Firewalls
* Cloud security groups
* Linux server deployment
* Web server deployment
* Basic network troubleshooting

---

# Conclusion

This project provided hands-on experience with Linux, networking, and cloud infrastructure.

The combination of Linux administration, networking configuration, security controls, SSH, and cloud server deployment provides a foundation for further learning in **network engineering, cloud computing, system administration, and cybersecurity**.

---

## Project Status

```text
Linux Fundamentals       ✓
File Permissions         ✓
Users & Groups           ✓
Processes & Services     ✓
SSH                      ✓
IP Addressing            ✓
DNS                      ✓
Network Ports            ✓
Firewall                 ✓
Cloud Security Groups    ✓
Linux Server Deployment  ✓
```

---

## Author

**Tejas Kondhalkar**

B.E. Electronics & Telecommunication Engineering

Interested in:

* Networking
* Linux
* Cloud Computing
* Technical Support
* Cybersecurity

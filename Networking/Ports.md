# Networking — Network Ports

## 1. Introduction

A **network port** is a logical endpoint used by applications and services for network communication.

An IP address identifies a device, while a port helps identify a particular service running on that device.

Example:

```text
192.168.1.10:22
```

Here:

```text
IP Address → 192.168.1.10
Port       → 22
```

---

## 2. Port Number Range

TCP and UDP port numbers range from:

```text
0 - 65535
```

They are commonly divided into:

| Range       | Type                  |
| ----------- | --------------------- |
| 0–1023      | Well-known ports      |
| 1024–49151  | Registered ports      |
| 49152–65535 | Dynamic/private ports |

---

## 3. Common Network Ports

|  Port | Protocol | Common Service |
| ----: | -------- | -------------- |
| 20/21 | TCP      | FTP            |
|    22 | TCP      | SSH            |
|    23 | TCP      | Telnet         |
|    25 | TCP      | SMTP           |
|    53 | TCP/UDP  | DNS            |
| 67/68 | UDP      | DHCP           |
|    80 | TCP      | HTTP           |
|   110 | TCP      | POP3           |
|   143 | TCP      | IMAP           |
|   443 | TCP      | HTTPS          |
|  3389 | TCP      | RDP            |

Port usage can vary depending on the application and configuration.

---

## 4. TCP and UDP

### TCP

TCP is connection-oriented.

It provides reliable and ordered communication.

Examples:

* HTTP
* HTTPS
* SSH

### UDP

UDP is connectionless and has lower protocol overhead.

Examples:

* DNS queries
* DHCP
* Streaming and real-time applications

---

## 5. Check Listening Ports

Use:

```bash
ss -tuln
```

Meaning:

```text
-t → TCP
-u → UDP
-l → Listening
-n → Numeric addresses and ports
```

For more information:

```bash
ss -tulpn
```

---

## 6. Check a Specific Port

For example, check whether SSH is listening:

```bash
sudo ss -tulpn | grep :22
```

Check HTTP:

```bash
sudo ss -tulpn | grep :80
```

Check HTTPS:

```bash
sudo ss -tulpn | grep :443
```

---

## 7. Test a Port Using Netcat

If `nc` is installed:

```bash
nc -zv localhost 22
```

Example:

```text
Connection to localhost 22 port [tcp/ssh] succeeded!
```

The exact output may vary.

---

## 8. Port and Service Relationship

Example:

```text
SSH Server
    |
    ↓
TCP Port 22
    |
    ↓
SSH Client
```

Another example:

```text
Web Server
    |
    ↓
TCP Port 80/443
    |
    ↓
Web Browser
```

---

## 9. Port Troubleshooting

If a service cannot be accessed:

### Step 1 — Check whether the service is running

```bash
systemctl status ssh
```

### Step 2 — Check whether the port is listening

```bash
ss -tuln
```

### Step 3 — Check firewall rules

```bash
sudo ufw status
```

### Step 4 — Check cloud security rules

For a cloud server, also check the configured security group/firewall rules.

---

## 10. Practical Exercise

Run:

```bash
ss -tuln
```

Then:

```bash
sudo ss -tulpn
```

Check whether SSH is listening:

```bash
sudo ss -tulpn | grep :22
```

If available:

```bash
nc -zv localhost 22
```

Take screenshots of the results.

---

## 11. Learning Outcomes

I learned:

* What network ports are
* TCP and UDP
* Common network ports
* How to check listening ports
* How ports relate to services
* Basic port troubleshooting

---

## 12. Conclusion

Ports allow multiple network services to operate on the same device.

Understanding ports is important for Linux administration, networking, firewall configuration, cloud security, and cybersecurity.


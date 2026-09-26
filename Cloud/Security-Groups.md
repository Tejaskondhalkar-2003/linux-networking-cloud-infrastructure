# Cloud — Security Groups

## 1. Introduction

A **Security Group** is a virtual network security control used by cloud platforms to control network traffic to and from cloud resources.

For example, a Linux server may require:

```text
SSH   → TCP 22
HTTP  → TCP 80
HTTPS → TCP 443
```

Only required traffic should be allowed.

---

## 2. Security Group Concept

Basic flow:

```text
Internet
   |
   ↓
Security Group
   |
   ↓
Cloud Server
```

The security group evaluates network traffic according to configured rules.

---

## 3. Inbound Rules

Inbound rules control traffic coming **towards** a cloud resource.

Example:

| Protocol | Port | Source   | Purpose |
| -------- | ---: | -------- | ------- |
| TCP      |   22 | Your IP  | SSH     |
| TCP      |   80 | Internet | HTTP    |
| TCP      |  443 | Internet | HTTPS   |

For SSH, restricting access to your own IP address is generally preferable to allowing SSH from everywhere when the cloud environment permits it.

---

## 4. Outbound Rules

Outbound rules control traffic leaving the cloud resource.

Example:

```text
Server
  |
  ↓
Outbound Rule
  |
  ↓
Internet
```

The exact default outbound policy depends on the cloud provider and configuration.

---

## 5. Security Group vs Linux Firewall

A cloud server can have multiple layers of network control.

```text
Internet
   |
   ↓
Cloud Security Group
   |
   ↓
Linux Firewall
   |
   ↓
Linux Server
   |
   ↓
Application
```

### Security Group

Controls traffic at the cloud/network level.

### Linux Firewall

Controls traffic inside the operating system.

Both can work together.

---

## 6. Example

Suppose an Ubuntu server runs:

```text
SSH  → 22
HTTP → 80
```

Security group:

```text
Inbound:
TCP 22 → Allowed
TCP 80 → Allowed
```

Linux firewall:

```text
22/tcp  → ALLOW
80/tcp  → ALLOW
```

Both layers must permit the traffic for the service to be reachable.

---

## 7. Security Best Practices

### Use Least Privilege

Allow only the ports that are required.

### Restrict SSH

Instead of:

```text
0.0.0.0/0
```

use a restricted source such as your own public IP when appropriate.

### Avoid Unnecessary Ports

Do not expose services that are not required.

### Review Rules

Regularly check security group rules and remove unnecessary access.

---

## 8. Example Configuration

For a basic web server:

```text
Inbound:

SSH
Protocol: TCP
Port: 22
Source: Your IP

HTTP
Protocol: TCP
Port: 80
Source: 0.0.0.0/0

HTTPS
Protocol: TCP
Port: 443
Source: 0.0.0.0/0
```

The exact configuration depends on the cloud provider and application requirements.

---

## 9. Testing Connectivity

After configuring a security group, test SSH:

```bash
ssh username@server-ip
```

Test HTTP:

```bash
curl http://server-ip
```

Check listening ports on the server:

```bash
ss -tuln
```

---

## 10. Troubleshooting

If SSH does not work, check:

```text
1. Is the server running?
2. Is the correct public IP being used?
3. Is TCP port 22 allowed in the security group?
4. Is SSH running on the server?
5. Is the Linux firewall allowing SSH?
6. Is the username correct?
7. Is the SSH key/password correct?
```

Check SSH:

```bash
systemctl status ssh
```

Check firewall:

```bash
sudo ufw status
```

Check listening ports:

```bash
ss -tuln
```

---

## 11. Practical Exercise

Create or inspect a cloud server security group.

Document:

```text
Server:
Operating System:
Public IP:
Security Group:
```

Record the required inbound ports:

```text
22 → SSH
80 → HTTP
443 → HTTPS
```

Take screenshots of the security group configuration.

> **Security:** Do not include private keys, passwords, access tokens, or other sensitive credentials in GitHub screenshots.

---

## 12. Learning Outcomes

I learned:

* What cloud security groups are
* Inbound and outbound rules
* How security groups control network access
* Difference between security groups and Linux firewalls
* Least-privilege network access
* Basic cloud network troubleshooting

---

## 13. Conclusion

Security groups provide an important network security layer for cloud resources.

A secure configuration should expose only the ports required by the server and applications.


# Networking — Firewall

## 1. Introduction

A **firewall** controls network traffic based on configured rules.

It can allow or block connections according to factors such as:

* Source
* Destination
* Port
* Protocol
* Network interface

Basic concept:

```text
Internet
   |
   ↓
Firewall
   |
   ↓
Server
```

---

## 2. Why Firewalls Are Used

Firewalls help control which network connections can reach a system.

For example, a server may need:

```text
SSH   → Port 22
HTTP  → Port 80
HTTPS → Port 443
```

Other unnecessary inbound connections can be blocked.

---

## 3. UFW

**UFW (Uncomplicated Firewall)** is a firewall management tool commonly used on Ubuntu.

Check its status:

```bash
sudo ufw status
```

Detailed status:

```bash
sudo ufw status verbose
```

---

## 4. Enable UFW Safely

Before enabling UFW on a remote server, make sure SSH access is allowed.

Allow SSH:

```bash
sudo ufw allow 22/tcp
```

Then enable the firewall:

```bash
sudo ufw enable
```

Check:

```bash
sudo ufw status
```

> **Important:** On a remote/cloud server, enabling a firewall without allowing SSH first can lock you out.

---

## 5. Allow a Port

Allow HTTP:

```bash
sudo ufw allow 80/tcp
```

Allow HTTPS:

```bash
sudo ufw allow 443/tcp
```

---

## 6. Block a Port

Example:

```bash
sudo ufw deny 23/tcp
```

Port 23 is commonly associated with Telnet.

---

## 7. Delete a Firewall Rule

List rules with numbers:

```bash
sudo ufw status numbered
```

Delete a rule:

```bash
sudo ufw delete <rule-number>
```

---

## 8. Allow SSH

The simple method:

```bash
sudo ufw allow ssh
```

Or:

```bash
sudo ufw allow 22/tcp
```

---

## 9. Default Firewall Policies

You can configure default policies:

```bash
sudo ufw default deny incoming
```

```bash
sudo ufw default allow outgoing
```

This creates a common server configuration where incoming connections are denied unless specifically allowed.

---

## 10. Example Server Firewall

A basic web server might use:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing

sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

sudo ufw enable
```

This allows:

```text
SSH   → 22
HTTP  → 80
HTTPS → 443
```

while blocking other unsolicited incoming connections according to the firewall's rules.

---

## 11. Check Firewall Rules

```bash
sudo ufw status numbered
```

Example:

```text
22/tcp   ALLOW
80/tcp   ALLOW
443/tcp  ALLOW
```

The exact output depends on the configured system.

---

## 12. Practical Exercise

On a test Linux environment:

```bash
sudo ufw status
```

Allow SSH:

```bash
sudo ufw allow 22/tcp
```

Allow HTTP:

```bash
sudo ufw allow 80/tcp
```

Check:

```bash
sudo ufw status numbered
```

Take a screenshot.

---

## 13. Firewall Troubleshooting

If a service is not reachable, check:

### Service

```bash
systemctl status <service>
```

### Listening port

```bash
ss -tuln
```

### Local firewall

```bash
sudo ufw status
```

### Cloud firewall/security group

Check the cloud provider's network security rules.

---

## 14. Learning Outcomes

I learned:

* What a firewall is
* Why firewalls are used
* Basic UFW commands
* How to allow and deny ports
* How to check firewall rules
* Basic firewall troubleshooting

---

## 15. Conclusion

A firewall is an important security control for Linux servers and cloud infrastructure.

Firewall rules should allow only the network traffic required by the services running on the server.


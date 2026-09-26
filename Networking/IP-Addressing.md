# Networking — IP Addressing

## 1. Introduction

An **IP address (Internet Protocol address)** is an address assigned to a device on a network.

It helps identify devices and allows them to communicate with each other.

Example:

```text
192.168.1.10
```

In Linux, IP address information can be checked using:

```bash
ip addr
```

or:

```bash
hostname -I
```

---

## 2. IPv4

IPv4 uses a **32-bit address**.

Example:

```text
192.168.1.10
```

An IPv4 address contains four decimal numbers separated by dots.

Each number can range from `0` to `255`.

---

## 3. IPv6

IPv6 uses a **128-bit address**.

Example:

```text
2001:db8::1
```

IPv6 provides a much larger address space than IPv4.

---

## 4. Private IP Addresses

Private IP addresses are commonly used inside local networks.

Common private IPv4 ranges:

| Range          | Example      |
| -------------- | ------------ |
| 10.0.0.0/8     | 10.0.0.5     |
| 172.16.0.0/12  | 172.16.10.20 |
| 192.168.0.0/16 | 192.168.1.10 |

Example:

```text
Computer → 192.168.1.10
Router    → 192.168.1.1
```

---

## 5. Public IP Address

A public IP address is used for communication over the Internet.

A cloud server may have:

```text
Private IP → Internal communication
Public IP  → Internet communication
```

---

## 6. Static and Dynamic IP

### Static IP

A static IP is manually assigned and normally remains unchanged.

Example:

```text
Server → 192.168.1.100
```

### Dynamic IP

A dynamic IP is normally assigned automatically using DHCP.

```text
Device → DHCP Server → IP Address
```

---

## 7. DHCP

**DHCP (Dynamic Host Configuration Protocol)** automatically provides network configuration.

It can provide:

* IP address
* Subnet mask
* Default gateway
* DNS server

---

## 8. Subnet Mask

A subnet mask identifies the network and host portions of an IPv4 address.

Example:

```text
IP Address:  192.168.1.10
Subnet Mask: 255.255.255.0
```

CIDR notation:

```text
192.168.1.10/24
```

`/24` means 24 bits are used for the network portion.

---

## 9. Default Gateway

A default gateway is normally the router used to communicate with other networks.

Example:

```text
Computer
192.168.1.10
      |
      ↓
Gateway
192.168.1.1
      |
      ↓
Internet
```

Check the gateway:

```bash
ip route
```

---

## 10. Check IP Address in Linux

```bash
ip addr
```

or:

```bash
hostname -I
```

---

## 11. Check Network Interfaces

```bash
ip link
```

Common interfaces include:

```text
eth0
ens33
enp0s3
wlan0
lo
```

`lo` is the loopback interface.

---

## 12. Check Routing Table

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
```

---

## 13. Test Connectivity

Test the loopback interface:

```bash
ping 127.0.0.1
```

Test Internet connectivity:

```bash
ping 8.8.8.8
```

Test DNS and Internet connectivity:

```bash
ping google.com
```

Stop the command using:

```text
Ctrl + C
```

---

## 14. Basic Network Troubleshooting

A simple troubleshooting sequence:

```text
1. Check network interface
        ↓
2. Check IP address
        ↓
3. Check default gateway
        ↓
4. Ping gateway
        ↓
5. Ping Internet IP
        ↓
6. Test DNS
```

Commands:

```bash
ip link
ip addr
ip route
ping <gateway-ip>
ping 8.8.8.8
ping google.com
```

---

## 15. Practical Exercise

Run:

```bash
ip addr
hostname -I
ip link
ip route
ping 127.0.0.1
ping 8.8.8.8
ping google.com
```

Take screenshots of the output and save them in the `screenshots` folder.

---

## 16. Learning Outcomes

After completing this section, I learned:

* IPv4 and IPv6
* Private and public IP addresses
* Static and dynamic IP addresses
* DHCP
* Subnet masks
* Default gateway
* Linux network commands
* Basic network troubleshooting

---

## 17. Conclusion

IP addressing is a fundamental part of networking.

Linux provides commands such as `ip addr`, `ip route`, and `ping` to inspect and troubleshoot network configuration.

These concepts are useful when working with Linux servers, cloud infrastructure, networking, and cybersecurity.


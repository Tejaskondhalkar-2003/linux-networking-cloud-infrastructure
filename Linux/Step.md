Absolutely. Here is the **complete sequence from start to finish** for your Linux Server Deployment assignment. You can save this and repeat the whole project later.

# Linux Server Deployment — Complete Step-by-Step

## PART 1 — AWS EC2 Server

### Step 1: Open AWS

Go to AWS Console → **EC2** → **Instances** → **Launch instance**.

### Step 2: Create the instance

Use:

* **Name:** `Linux-Cloud-Server`
* **OS:** Ubuntu Server LTS
* **Instance type:** Use the eligible small/free-tier option available to your AWS account
* **Key pair:** Create a new key pair

  * Example: `linux-server-key`
  * Type: `.pem`
  * Download it to your computer

⚠️ **Never upload the `.pem` file to GitHub.**

---

## PART 2 — Security Group

During EC2 creation, configure:

### Inbound rules

| Type | Port | Source        |
| ---- | ---: | ------------- |
| SSH  |   22 | My IP         |
| HTTP |   80 | Anywhere IPv4 |

Then click **Launch instance**.

---

# PART 3 — Connect to Ubuntu

### Step 3: Open CMD

Press:

**Windows + R → `cmd` → Enter**

### Step 4: Go to Downloads

```cmd
cd C:\Users\Tejas\Downloads
```

Check your key:

```cmd
dir
```

You should see:

```text
linux-server-key.pem
```

### Step 5: Get Public IPv4

AWS Console → EC2 → Instances → select your server.

Copy:

**Public IPv4 address**

Example:

```text
13.xxx.xxx.xxx
```

### Step 6: SSH into server

In CMD:

```cmd
ssh -i linux-server-key.pem ubuntu@YOUR_PUBLIC_IP
```

Example:

```cmd
ssh -i linux-server-key.pem ubuntu@13.234.56.78
```

If asked:

```text
Are you sure you want to continue connecting?
```

Type:

```text
yes
```

You should see:

```text
ubuntu@ip-172-31-xx-xx:~$
```

✅ You are now inside your Linux server.

---

# PART 4 — Check Linux Server

### Step 7: Check current user

```bash
whoami
```

Expected:

```text
ubuntu
```

### Step 8: Check hostname

```bash
hostname
```

### Step 9: Check Ubuntu version

```bash
cat /etc/os-release
```

📸 **Screenshot 1 — Linux Server Connection**

Take a screenshot showing the terminal and these commands/results.

---

# PART 5 — IP Addressing

### Step 10: Check IP address

```bash
ip addr
```

Look for:

```text
inet 172.31.xx.xx
```

### Step 11: Simple IP command

```bash
hostname -I
```

### Step 12: Check routing

```bash
ip route
```

📸 **Screenshot 2 — IP Address**

📸 **Screenshot 3 — IP Route**

---

# PART 6 — Update Linux

### Step 13: Update package list

```bash
sudo apt update
```

### Step 14: Upgrade packages

```bash
sudo apt upgrade -y
```

You may see the Ubuntu message about **ESM Apps**. That's normal. You don't need to enable ESM for this assignment.

---

# PART 7 — Test Network Connectivity

### Step 15: Test Internet using IP

```bash
ping -c 4 8.8.8.8
```

You should get replies such as:

```text
64 bytes from 8.8.8.8
```

### Step 16: Test DNS

```bash
ping -c 4 google.com
```

If you get replies, both Internet connectivity and DNS are working.

📸 **Screenshot 4 — Connectivity Test**

---

# PART 8 — Configure Linux Firewall

### Step 17: Check UFW

```bash
sudo ufw status
```

### Step 18: Allow SSH

```bash
sudo ufw allow 22/tcp
```

### Step 19: Allow HTTP

```bash
sudo ufw allow 80/tcp
```

### Step 20: Enable firewall

```bash
sudo ufw enable
```

If it asks:

```text
Command may disrupt existing ssh connections. Proceed with operation (y|n)?
```

Type:

```text
y
```

### Step 21: Check firewall

```bash
sudo ufw status
```

You should see something similar to:

```text
22/tcp    ALLOW
80/tcp    ALLOW
```

📸 **Screenshot 5 — UFW Firewall**

---

# PART 9 — Install Web Server

Now we're going to deploy an actual service on the Linux server.

### Step 22: Install Nginx

```bash
sudo apt install nginx -y
```

Wait until installation finishes.

### Step 23: Check Nginx

```bash
sudo systemctl status nginx
```

Look for:

```text
Active: active (running)
```

📸 **Screenshot 6 — Nginx Running**

Press **Q** to exit the status screen.

---

# PART 10 — Make Nginx Start Automatically

### Step 24:

```bash
sudo systemctl enable nginx
```

### Step 25: Verify

```bash
sudo systemctl is-enabled nginx
```

Expected:

```text
enabled
```

---

# PART 11 — Check Port 80

### Step 26:

```bash
sudo ss -tuln | grep :80
```

You should see something listening on port 80.

Example:

```text
LISTEN ... 0.0.0.0:80
```

📸 **Screenshot 7 — Port 80**

---

# PART 12 — Test Nginx Locally

### Step 27:

```bash
curl http://localhost
```

You should get HTML output containing something related to:

```text
Welcome to nginx!
```

📸 **Screenshot 8 — Curl Nginx**

---

# PART 13 — Test From Your Computer

Go back to your normal Windows browser.

Enter:

```text
http://YOUR_PUBLIC_IP
```

For example:

```text
http://13.234.56.78
```

You should see the:

**Welcome to nginx!**

webpage.

📸 **Screenshot 9 — Nginx Webpage**

🎉 This proves that your Linux server is accessible from the Internet and is serving a web service.

---

# PART 14 — Final Verification

Run these commands again:

### Server information

```bash
hostname
```

### IP

```bash
ip addr
```

### Route

```bash
ip route
```

### Firewall

```bash
sudo ufw status
```

### Nginx

```bash
sudo systemctl status nginx
```

### Port

```bash
sudo ss -tuln | grep :80
```

### Web service

```bash
curl http://localhost
```

If all are working, your **practical Linux server deployment is complete.** ✅

---

# PART 15 — Screenshots Folder

You already have:

```text
screenshots/
└── README.md
```

Don't create another folder.

Put your screenshots there, for example:

```text
screenshots/
├── 01-EC2-Instance.png
├── 02-SSH-Connection.png
├── 03-IP-Address.png
├── 04-IP-Route.png
├── 05-Connectivity-Test.png
├── 06-UFW-Firewall.png
├── 07-Nginx-Running.png
├── 08-Port-80.png
└── 09-Nginx-Webpage.png
```

---

# PART 16 — GitHub

Your existing project structure should remain:

```text
Cloud/
├── Linux-Server-Deployment.md
└── Security-Groups.md

Linux/
├── CLI-Commands.md
├── Files-Permissions.md
├── Processes-Services.md
├── SSH.md
└── Users-Groups.md

Networking/
├── DNS.md
├── Firewall.md
├── IP-Addressing.md
└── Ports.md

screenshots/
├── 01-EC2-Instance.png
├── 02-SSH-Connection.png
├── 03-IP-Address.png
├── 04-IP-Route.png
├── 05-Connectivity-Test.png
├── 06-UFW-Firewall.png
├── 07-Nginx-Running.png
├── 08-Port-80.png
└── 09-Nginx-Webpage.png

README.md
```

Then push everything to GitHub.

⚠️ Before pushing, make sure these are **NOT** inside the repository:

```text
*.pem
AWS access keys
AWS secret keys
passwords
tokens
```

---

# PART 17 — Final Submission

Your assignment requires:

### 1. GitHub Repository Link

Copy your GitHub repository URL.

### 2. LinkedIn Post

Create a short post showing that you completed:

* Linux CLI
* Files & permissions
* Users & groups
* Processes & services
* SSH
* IP addressing
* DNS
* Ports
* Firewall
* Security groups
* AWS Linux server deployment
* Nginx deployment
* Connectivity testing

Then copy your LinkedIn post URL.

---

## ⭐ The easiest order to remember

```text
AWS EC2
   ↓
Create Ubuntu Server
   ↓
Security Group
   ↓
Download .pem
   ↓
CMD
   ↓
SSH
   ↓
whoami / hostname
   ↓
ip addr
   ↓
ip route
   ↓
apt update
   ↓
ping
   ↓
UFW Firewall
   ↓
Install Nginx
   ↓
systemctl status nginx
   ↓
Port 80
   ↓
curl localhost
   ↓
Browser → Public IP
   ↓
Screenshots
   ↓
GitHub
   ↓
LinkedIn
```

**This is the sequence I recommend you follow every time.** If you're doing it now, start at **Step 7 (`whoami`)** because your AWS server is already running and you're already connected to Ubuntu.

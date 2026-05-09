# 🔐 SSH Hardening Lab

This project demonstrates how to secure SSH access on a Linux server using industry-standard hardening techniques.  
The lab was completed on a CentOS/RHEL-based virtual machine as part of my Linux System Administration practice portfolio.

---

# 📌 Objectives

The purpose of this lab was to:

- Understand how SSH works
- Configure secure remote access
- Harden SSH against unauthorized access
- Disable insecure authentication methods
- Implement SSH key authentication
- Improve Linux server security practices
- Troubleshoot SSH connectivity issues

---

# 🖥️ Environment

| Component | Details |
|---|---|
| OS | CentOS / RHEL |
| Access Method | SSH |
| Client Machine | Linux VM / Windows |
| Server Role | Linux Server |
| Authentication | SSH Keys |

---

# 📖 SSH Overview

SSH (Secure Shell) is a secure network protocol used to remotely access and manage Linux servers.

SSH provides:

- Encrypted communication
- Secure remote terminal access
- File transfers using SCP/SFTP
- Secure automation and administration

Default SSH Port:

```bash
22
```

SSH service:

```bash
sshd
```

---

# 🏗️ SSH Architecture

```text
+-------------------+
| Client Machine    |
| (Administrator)   |
+---------+---------+
          |
          | SSH Connection (Encrypted)
          |
          v
+-------------------+
| Linux Server      |
| sshd Service      |
+-------------------+
```

SSH Process Flow:

1. Client initiates SSH connection
2. Server presents identity
3. Authentication occurs
4. Encrypted session is established
5. Administrator gains remote shell access

---

# ⚙️ Basic SSH Commands

## Connect to a Server

```bash
ssh username@server-ip
```

Example:

```bash
ssh admin@192.168.1.20
```

---

## Check SSH Service Status

```bash
systemctl status sshd
```

---

## Start SSH Service

```bash
sudo systemctl start sshd
```

---

## Enable SSH at Boot

```bash
sudo systemctl enable sshd
```

---

## Restart SSH Service

```bash
sudo systemctl restart sshd
```

---

## Test SSH Configuration

```bash
sshd -t
```

---

# 🔑 SSH Key Authentication

SSH keys provide a more secure alternative to passwords.

## Types of Keys

| Key Type | Purpose |
|---|---|
| Private Key | Stored securely on client |
| Public Key | Copied to server |

---

# 🔐 Generate SSH Keys

```bash
ssh-keygen -t rsa -b 4096
```

Files created:

```text
~/.ssh/id_rsa
~/.ssh/id_rsa.pub
```

---

# 📤 Copy Public Key to Server

```bash
ssh-copy-id user@server-ip
```

Example:

```bash
ssh-copy-id admin@192.168.1.20
```

---

# 🔒 SSH Hardening Configuration

SSH configuration file:

```bash
/etc/ssh/sshd_config
```

---

## Security Improvements Implemented

### 1. Disable Root Login

```bash
PermitRootLogin no
```

Why?

- Prevents direct root access
- Reduces brute-force attack risk

---

### 2. Disable Password Authentication

```bash
PasswordAuthentication no
```

Why?

- Forces SSH key authentication
- Prevents password guessing attacks

---

### 3. Change Default SSH Port

Example:

```bash
Port 2222
```

Why?

- Reduces automated scanning attempts

---

### 4. Limit User Access

```bash
AllowUsers admin
```

Why?

- Restricts SSH access to authorized users only

---

### 5. Disable Empty Passwords

```bash
PermitEmptyPasswords no
```

---

### 6. Configure Idle Timeout

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

Why?

- Automatically disconnects inactive sessions

---

# 🔥 Firewall Configuration

Open SSH port in firewall:

```bash
sudo firewall-cmd --permanent --add-port=2222/tcp
sudo firewall-cmd --reload
```

Verify:

```bash
firewall-cmd --list-all
```

---

# 📷 Screenshots

## SSH Service Running

_Add screenshot here_

```text
Example:
systemctl status sshd
```

---

## Successful SSH Login

_Add screenshot here_

---

## SSH Key Generation

_Add screenshot here_

---

## SSH Configuration File

_Add screenshot here_

---

# 🧪 Verification Tests

## Test SSH Connection

```bash
ssh -p 2222 admin@192.168.1.20
```

---

## Confirm Password Login is Disabled

Attempt login without SSH key.

Expected result:

```text
Permission denied (publickey)
```

---

#   Troubleshooting Notes

## Problem: SSH Service Fails to Start

Check configuration syntax:

```bash
sshd -t
```

Check logs:

```bash
journalctl -xe
```

---

## Problem: Connection Refused

Verify:

- SSH service is running
- Firewall allows SSH port
- Correct IP address used

Commands:

```bash
systemctl status sshd
ss -tulnp | grep ssh
```

---

## Problem: Permission Denied (publickey)

Verify permissions:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

## Problem: Cannot Connect After Changing Port

Specify custom port:

```bash
ssh -p 2222 user@server-ip
```

---

# 📚 Key Linux Concepts Practiced

- SSH Administration
- Linux Security
- Firewall Management
- User Authentication
- Service Management
- SSH Key Management
- Remote Administration

---

# ✅ Skills Demonstrated

- SSH Hardening
- Linux Server Administration
- Security Best Practices
- Troubleshooting
- Firewall Configuration
- SSH Key Authentication
- Linux Networking

---

# 🚀 Future Improvements

Possible enhancements:

- Configure Fail2Ban
- Implement MFA for SSH
- Restrict access by IP
- Configure intrusion detection
- Automate hardening using Ansible



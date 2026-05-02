# 🚀 Evilginx3 - Complete Deployment Guide
## From VPS Setup to Campaign Deployment

> **⚠️ LEGAL DISCLAIMER**: This guide is for **AUTHORIZED PENETRATION TESTING ONLY**. Unauthorized use is illegal. Always obtain written permission before conducting security assessments.

---

## 📑 Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [VPS Selection & Setup](#2-vps-selection--setup)
3. [Domain Configuration](#3-domain-configuration)
4. [Server Installation](#4-server-installation)
5. [Evilginx3 Installation](#5-evilginx3-installation)
6. [SSL/TLS Certificate Setup](#6-ssltls-certificate-setup)
7. [Phishlet Configuration](#7-phishlet-configuration)
8. [Redirector Setup (Turnstile)](#8-redirector-setup-turnstile)
9. [Lure Creation & Distribution](#9-lure-creation--distribution)
10. [Campaign Monitoring](#10-campaign-monitoring)
11. [Session Harvesting](#11-session-harvesting)
12. [Advanced Evasion Techniques](#12-advanced-evasion-techniques)
13. [Operational Security](#13-operational-security)
14. [Troubleshooting](#14-troubleshooting)
15. [Post-Engagement Cleanup](#15-post-engagement-cleanup)

---

## 1. Prerequisites

### 1.1 Required Resources

**Infrastructure:**
- VPS with minimum 2GB RAM, 2 CPU cores, 20GB storage
- Domain name(s) for phishing
- Cloudflare account (free tier sufficient)
- SSH client (Terminal, PuTTY, etc.)

**Knowledge Requirements:**
- Basic Linux command line
- Understanding of DNS records
- Familiarity with web hosting concepts
- Authorization documentation for red team engagement

### 1.2 Recommended Tools

```bash
# Local machine tools
- SSH client
- Text editor (VS Code, Sublime, etc.)
- Web browser with developer tools
- Email client for testing
```

---

## 2. VPS Selection & Setup

### 2.1 VPS Provider Selection

**Recommended Providers:**

| Provider | Pros | Cons | Starting Price |
|----------|------|------|----------------|
| **DigitalOcean** | Easy setup, good docs | Popular (may be flagged) | $6/month |
| **Vultr** | Good performance, flexible | Limited regions | $6/month |
| **Linode** | Reliable, established | Moderate pricing | $5/month |
| **Hetzner** | Cheap, EU-based | Limited US presence | €4.5/month |
| **AWS Lightsail** | AWS ecosystem | Complex pricing | $5/month |

**Selection Criteria:**
- ✅ Accept cryptocurrency/privacy-focused payment
- ✅ Don't require extensive KYC
- ✅ Allow port 80/443 traffic
- ✅ Good network performance
- ✅ Located near target audience

### 2.2 VPS Creation

**Example: DigitalOcean Setup**

1. **Create Account:**
   ```
   - Sign up at digitalocean.com
   - Verify email
   - Add payment method
   ```

2. **Create Droplet:**
   ```
   Choose an image: Ubuntu 22.04 LTS x64
   Choose a plan: Basic $12/month (2GB RAM, 2 CPUs)
   Choose a datacenter: Closest to targets
   Authentication: SSH keys (recommended) or password
   Hostname: Choose something neutral (e.g., web-server-01)
   ```

3. **Save VPS Details:**
   ```
   IP Address: xxx.xxx.xxx.xxx
   Root password: (if not using SSH keys)
   SSH key: (your private key)
   ```

### 2.3 Initial VPS Access

**Connect via SSH:**

```bash
# If using password
ssh root@YOUR_VPS_IP

# If using SSH key
ssh -i ~/.ssh/id_rsa root@YOUR_VPS_IP
```

**First Login Security Steps:**

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Create non-root user (optional but recommended)
adduser evilginx
usermod -aG sudo evilginx

# Configure firewall
ufw allow 22/tcp    # SSH
ufw allow 80/tcp    # HTTP
ufw allow 443/tcp   # HTTPS
ufw allow 53/tcp    # DNS
ufw allow 53/udp    # DNS
ufw enable

# Verify firewall status
ufw status
```

### 2.4 SSH Hardening (Optional)

```bash
# Edit SSH config
nano /etc/ssh/sshd_config

# Recommended changes:
Port 2222                        # Change default port
PermitRootLogin no               # Disable root login
PasswordAuthentication no        # Disable password auth (SSH keys only)
PubkeyAuthentication yes         # Enable SSH key auth

# Restart SSH
systemctl restart sshd

# Reconnect using new port
ssh -p 2222 root@YOUR_VPS_IP


To get all the deployment guides, reach out to t.me/officialmonsterz

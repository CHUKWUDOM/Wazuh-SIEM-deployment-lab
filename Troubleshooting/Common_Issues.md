# Common Issues & Troubleshooting Guide

This document outlines common problems encountered during Wazuh single-node deployment on Ubuntu Desktop and their solutions.

---

## 📑 Table of Contents

- [1. Dashboard Not Accessible](#1-dashboard-not-accessible)
- [2. Wazuh Services Not Starting](#2-wazuh-services-not-starting)
- [3. High Memory Usage](#3-high-memory-usage)
- [4. Installation Script Fails](#4-installation-script-fails)
- [5. Login Credentials Lost](#5-login-credentials-lost)
- [6. Certificate Warning in Browser](#6-certificate-warning-in-browser)
- [7. Port Already in Use Error](#7-port-already-in-use-error)
- [8. Wazuh Indexer Not Starting (Memory Issue)](#8-wazuh-indexer-not-starting-memory-issue)
- [9. Services Not Starting After Reboot](#9-services-not-starting-after-reboot)
- [Security Reminder](#security-reminder)
- [Lessons Learned](#lessons-learned)

---

## 1️⃣ Dashboard Not Accessible

**Issue:**  
`https://localhost:8443` not loading

### Possible Causes

- Port forwarding not configured properly  
- Wazuh dashboard service not running  
- Firewall blocking port 443  
- Wrong host port used  

---

### 🔍 Step 1 – Verify Dashboard Service

```bash
sudo systemctl status wazuh-dashboard

```
#### Expected output:

```bash
active (running)
```

#### If inactive:
```bash
sudo systemctl restart wazuh-dashboard
```

### 🔍 Step 2 – Verify Port Forwarding (VirtualBox)

#### Ensure:
```bash
Host Port → 8443

Guest Port → 443

Access URL:https://localhost:8443
```

### 🔍 Step 3 – Check Listening Ports
```bash
sudo ss -tulnp | grep 443
```

### This confirms Wazuh dashboard is listening on port 443.<br>
<br>

## 2️⃣ Wazuh Services Not Starting
### Check Service Status
```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
```

### Restart All Services
```bash
sudo systemctl restart wazuh-manager
sudo systemctl restart wazuh-indexer
sudo systemctl restart wazuh-dashboard
```

### Check Logs for Errors
```bash
sudo journalctl -xe
```

### Or specifically:
```bash
sudo journalctl -u wazuh-indexer
```

### Common Causes

* Low memory
* Corrupted installation
* Incomplete package update
<br><br>


## 3️⃣ High Memory Usage

 Wazuh Indexer is resource-intensive.

### Monitor Usage
```bash
htop
```

 If RAM usage exceeds available memory:

### Solutions

* Close unnecessary applications
* Increase VM RAM to 6GB (if host allows)
* Stop unused services temporarily:

```bash
sudo systemctl stop snapd
```
<br><br>

## 4️⃣ Installation Script Fails

  If installation stops unexpectedly:

### Step 1 – Update System
```bash
sudo apt update && sudo apt upgrade -y
```
### Step 2 – Re-run Installer
```bash
sudo bash wazuh-install.sh -a
```
<br><br>

## 5️⃣ Login Credentials Lost
### Locate Password File

  If still in install directory:
  
```bash
sudo cat wazuh-passwords.txt
```

  If not:
```bash
sudo find / -name "wazuh-passwords.txt" 2>/dev/null
```

### Check Internal Users File
```bash
sudo cat /usr/share/wazuh-indexer/opensearch-security/internal_users.yml
```

  ⚠️ Passwords are hashed here and not readable in plain text.
<br><br>

## 6️⃣ Certificate Warning in Browser

  When accessing:
  
```bash
https://localhost:8443
```

You may see:

*"Connection not secure"*<br>

This is expected because Wazuh uses a self-signed certificate.

Click:

#### Advanced → Proceed

For production environments, replace with a valid SSL certificate.

<br><br>

## 7️⃣ Port Already in Use Error

Check if port 443 is occupied:
```bash
sudo lsof -i :443
```

If another service is using it:
* Stop that service
* Or change Wazuh dashboard port configuration


## 8️⃣ Wazuh Indexer Not Starting (Memory Issue)

Check logs:
```bash
sudo journalctl -u wazuh-indexer
```

If memory-related:
* Increase VM RAM
* Reduce heap size manually (advanced configuration)

<br><br>

## 9️⃣ Services Not Starting After Reboot

Sometimes services may not auto-start.

Enable them:

```bash
sudo systemctl enable wazuh-manager
sudo systemctl enable wazuh-indexer
sudo systemctl enable wazuh-dashboard
```


🧠 Lessons Learned

* Wazuh Indexer is the most resource-heavy component.
* NAT networking requires correct port forwarding.
* Service validation using systemctl is essential.
* Monitoring logs using journalctl is critical for diagnosing issues.



##  1. What is UFW?

**UFW (Uncomplicated Firewall)** is a simple command-line interface for managing **iptables/nftables**.  
It allows beginners and administrators to apply firewall rules in an easy and readable way.

Example:

```bash
ufw allow 22
ufw deny 80
```

---

##  2. UFW Installation

### **Debian / Ubuntu**
```bash
sudo apt update
sudo apt install ufw -y
```

### **Arch Linux**
```bash
sudo pacman -S ufw
```

### **CentOS / RHEL**
```bash
sudo yum install epel-release -y
sudo yum install ufw -y
```

---

##  3. Essential Commands (Use When Setting Up for the First Time)

### **Check UFW Status**
```bash
sudo ufw status verbose
```

### **Enable UFW**
```bash
sudo ufw enable
```

### **Set Default Policies**
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

### **Add Rules Afterwards**  
(see the rules section below)

---

##  4. Important UFW Configuration Files

All UFW configuration files are stored in:

```
/etc/ufw/
```

### **File Overview**

| File | Purpose |
|------|---------|
| **ufw.conf** | Main settings file (enable/disable, logging, IPv6). |
| **before.rules** | Rules applied BEFORE user rules (ICMP, NAT, loopback). |
| **after.rules** | Rules applied AFTER user rules (final deny/logging). |
| **user.rules** | User-created IPv4 rules via `ufw allow/deny`. |
| **user6.rules** | User-created IPv6 rules. |
| **before6.rules** | IPv6 system rules. |
| **after6.rules** | IPv6 final rules. |
| **applications.d/** | App profiles like OpenSSH, Nginx, Apache. |

These matter for pentesters and sysadmins because they show **exactly how the system enforces firewall behavior underneath UFW commands**.

---

##  5. UFW Logging

Logs are saved in:

```
/var/log/ufw.log
```

Enable logging:

```bash
sudo ufw logging on
```

Levels: `off | low | medium | high | full`

---

##  6. How to List All Rules

### **Numbered Rules (best for deleting specific entries):**
```bash
sudo ufw status numbered
```

### **Normal List:**
```bash
sudo ufw status
```

---

##  7. How to Allow Ping (ICMP)

```bash
sudo ufw allow proto icmp
```

Or to specifically allow echo-request:

```bash
sudo ufw allow icmp
```

---

##  8. Basic Firewall Rules (10 Essential Ones)

### 1. Allow SSH
```bash
sudo ufw allow 22
```

### 2. Allow HTTP
```bash
sudo ufw allow 80
```

### 3. Allow HTTPS
```bash
sudo ufw allow 443
```

### 4. Allow OpenSSH profile
```bash
sudo ufw allow OpenSSH
```

### 5. Deny Telnet
```bash
sudo ufw deny 23
```

### 6. Deny FTP
```bash
sudo ufw deny 21
```

### 7. Allow a specific IP
```bash
sudo ufw allow from 192.168.1.10
```

### 8. Allow a subnet
```bash
sudo ufw allow from 192.168.1.0/24
```

### 9. Allow a port range
```bash
sudo ufw allow 3000:4000/tcp
```

### 10. Default security posture
```bash
sudo ufw default deny incoming
```

---

##  9. NAT Rules (2 Examples)

These are added to:

```
/etc/ufw/before.rules
```

### ** Masquerading (Source NAT)**
```bash
-A POSTROUTING -s 192.168.1.0/24 -o eth0 -j MASQUERADE
```

### ** Port Forwarding (Destination NAT)**

Forward port **8080 → internal server 192.168.1.10:80**

```bash
*nat
:PREROUTING ACCEPT [0:0]
-A PREROUTING -p tcp --dport 8080 -j DNAT --to-destination 192.168.1.10:80
COMMIT
```

Reload UFW:

```bash
sudo ufw reload
```

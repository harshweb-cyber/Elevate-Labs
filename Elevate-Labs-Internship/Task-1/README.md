# Task 1 — Scan Your Local Network for Open Ports

**Objective**  
Learn to discover open ports on devices in your local network to understand network exposure and highlight potential security risks.

---

## Introduction

### Nmap
**Nmap (Network Mapper)** is an open-source utility for network discovery and security auditing. It scans hosts to identify live systems, open ports, running services and versions, and possible vulnerabilities. Nmap is widely used by IT and security professionals for penetration testing, network inventory, and monitoring network health.

### Wireshark
**Wireshark** is a powerful, open-source network protocol analyzer used to capture and inspect data packets in real time. It helps administrators and security analysts troubleshoot network issues, analyze protocol behavior, and detect suspicious activity. Wireshark provides detailed protocol decoding and flexible filtering options for deep packet inspection.

> **Ethics & Legal Notice:** Only run scans and packet captures on networks and systems you own or when you have explicit written permission to test. Unauthorized scanning or packet capture is illegal and unethical.

---

## Install Process

### Nmap
1. Visit: https://nmap.org/download.html  
2. Download the appropriate installer for your OS and follow the installation instructions.

### Wireshark
1. Visit: https://www.wireshark.org/download.html  
2. Download a stable release for your OS and install. On Linux you may need to add your user to the `wireshark` group or run captures with elevated privileges.

---

## Scan Details (Lab setup)
- **Local IP Range scanned:** `192.168.1.0/24`  
- **Scan type used:** TCP SYN scan (`-sS`) over common ports (default 1000 ports)

**Command used (example):**
```bash
# Discover live hosts and perform a SYN scan on the subnet
sudo nmap -sS 192.168.1.0/24 -oA scans/192-168-1-0-24_syn
```

---

## Nmap Analysis — Summary
- **Total hosts up:** 6  
- **Notable open services found:** HTTP, Telnet, DNS, LDAP, AJP (Tomcat), SMB (Windows file sharing)  
- **Potential risks identified:**
  - Unencrypted Telnet (port 23) — high risk: should be disabled or replaced with SSH.
  - SMB services (ports 139/445) — patch and harden to mitigate worms and exploits (e.g., EternalBlue).
  - AJP (port 8009) — check for Ghostcat (CVE-2020-1938) if Tomcat/AJP is exposed.
  - LDAP (port 389) — should be protected with TLS (LDAPS / StartTLS) to avoid plaintext credentials.

---

## Detailed Host Findings

1. **Host:** `192.168.1.1`  
   **MAC:** (China Mobile Group Device)  
   **Open ports:** `23/tcp (telnet)`, `53/tcp (domain/DNS)`, `80/tcp (http)`, `49152/tcp (unknown)`  
   **Filtered:** `5555/tcp (freeciv)`  
   **Remarks:** Likely a router/gateway. Presence of Telnet/HTTP management interfaces is risky — consider disabling Telnet and enabling HTTPS/SSH admin.

2. **Host:** `192.168.1.2`    
   **Ports:** All 1000 scanned TCP ports closed.  
   **Remarks:** Active host with no exposed services — likely a client device or a device not offering network services.

3. **Host:** `192.168.1.4`  
   **MAC:** `` (Amazon Technologies)  
   **Open port:** `8009/tcp (ajp13)`  
   **Remarks:** AJP suggests a Tomcat/application server. Verify AJP is secured or restricted; check for Ghostcat vulnerability.

4. **Host:** `192.168.1.6`  
   **MAC:** `` (Xiaomi Communications)  
   **Ports:** All 1000 scanned TCP ports closed.  
   **Remarks:** Likely an IoT/mobile device with no exposed services.

5. **Host:** `192.168.1.8`  
   **MAC:** `` (AzureWave Technology)  
   **Open ports:** `135/tcp (msrpc)`, `139/tcp (netbios-ssn)`, `445/tcp (microsoft-ds)`, `902/tcp (iss-realsecure/vmware)`, `912/tcp (apex-mesh)`  
   **Remarks:** Typically a Windows host or device exposing SMB/NetBIOS; strongly recommend patching and limiting access via firewall rules.

6. **Host:** `192.168.1.11`  
   **MAC:** (Unknown)  
   **Open port:** `389/tcp (ldap)`  
   **Remarks:** Directory/identity service likely in use — secure with LDAPS and restrict access to trusted hosts only.

---

## Recommended Remediation / Hardening Steps
- **Replace Telnet** with **SSH** (or disable remote CLI if not needed). Use key-based authentication for SSH.
- **Apply OS and application patches** for hosts running SMB/Windows services.
- **Restrict management interfaces** (HTTP, AJP) to management VLANs or specific IP addresses; prefer HTTPS and authenticated management portals.
- **Enable encryption** for directory services (LDAP → LDAPS on 636) and other sensitive protocols.
- **Use host-based and network firewalls** to block unnecessary ports by default.
- **Network segmentation:** separate IoT/guest devices from critical infrastructure using VLANs.
- **Regular scans & monitoring:** schedule periodic Nmap scans and use IDS/monitoring to detect suspicious scanning or unusual traffic.

---

## Wireshark — Tips for Correlation & SYN Scan Detection
If you captured traffic in Wireshark, use this **display filter** to show only TCP SYN packets (SYN set, ACK not set), which indicates connection attempts such as those used by SYN scans:

```
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

**Capture BPF filter** (only capture SYN packets, reduces capture size):
```
tcp[13] & 0x02 != 0 and tcp[13] & 0x10 == 0
```

**Analysis tips**
- Look for a single source IP sending many SYNs to many destination ports — that is indicative of scanning activity.
- Check for corresponding SYN/ACK or RST replies to determine which ports are open or closed.
- Use *Statistics → Endpoints/Conversations* to identify top talkers and scanning patterns.

---

## Example Files / Output
- Save Nmap output in machine-readable and human-readable formats:
```bash
sudo nmap -sS -sV -O 192.168.1.0/24 -oA scans/192-168-1-0-24_full
# Produces: scans/192-168-1-0-24_full.nmap, .xml and .gnmap
```

- Save Wireshark captures as `.pcapng` files and include screenshots of interesting TCP streams.

---

## References
- Nmap: https://nmap.org  
- Wireshark: https://www.wireshark.org

---

## Notes
- Always sanitize any output before sharing publicly (remove real IPs, MAC addresses, credentials, or private data).  
- Use this procedure for learning and authorized assessments only.

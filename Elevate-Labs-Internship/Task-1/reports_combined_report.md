# Combined Report Template — Nmap & Wireshark Analysis

**Title:** Network Analysis of 192.168.1.0/24  
**Author:** Harsh Malik  
**Date:** 13-11-2025

## 1. Objective
- Discover hosts and services on the subnet.
- Capture and analyze network traffic for suspicious behavior.

## 2. Environment
- Testbed: Isolated lab network (list VMs/IPs here)
- Tools: Nmap 7.95, Wireshark (version)

## 3. Nmap Scan Details
**Command used:**  
```
sudo nmap -sS 192.168.1.0/24 -oA scans/192-168-1-0-24_syn
```

**Raw Nmap output (sanitized):**
```
Starting Nmap 7.95 ( https://nmap.org ) at 2025-11-13 0546 EST
Nmap scan report for 192.168.1.1
Host is up (0.0049s latency).
Not shown: 995 closed tcp ports (reset)
PORT      STATE    SERVICE
23/tcp    open     telnet
53/tcp    open     domain
80/tcp    open     http
5555/tcp  filtered freeciv
49152/tcp open     unknown
MAC Address: 44:C8:44:22:C9:6C (China Mobile Group Device)

Nmap scan report for 192.168.1.2
Host is up (0.0061s latency).
All 1000 scanned ports on 192.168.1.2 are in ignored states.
Not shown: 1000 closed tcp ports (reset)
MAC Address: BA:C7:0D:59:37:DA (Unknown)

Nmap scan report for 192.168.1.4
Host is up (0.0056s latency).
Not shown: 999 closed tcp ports (reset)
PORT     STATE SERVICE
8009/tcp open  ajp13
MAC Address: 7C:64:05:59:C7:E9 (Amazon Technologies)

Nmap scan report for 192.168.1.6
Host is up (0.0069s latency).
All 1000 scanned ports on 192.168.1.6 are in ignored states.
Not shown: 1000 closed tcp ports (reset)
MAC Address: E8:5E:8B:9F:48:6D (Xiaomi Communications)

Nmap scan report for 192.168.1.8
Host is up (0.0016s latency).
Not shown: 995 filtered tcp ports (no-response)
PORT    STATE SERVICE
135/tcp open  msrpc
139/tcp open  netbios-ssn
445/tcp open  microsoft-ds
902/tcp open  iss-realsecure
912/tcp open  apex-mesh
MAC Address: 10:68:35:A7:D8:B8 (AzureWave Technology)

Nmap scan report for 192.168.1.11
Host is up (0.0000060s latency).
Not shown: 999 closed tcp ports (reset)
PORT    STATE SERVICE
389/tcp open  ldap

Nmap done: 256 IP addresses (6 hosts up) scanned in 7.63 seconds
```

## 4. Nmap Findings Summary
- **Hosts up:** 6  
- **Notable services:** HTTP, Telnet, DNS, LDAP, AJP, SMB  
- **Risks & notes:** Telnet exposure, AJP on 8009, LDAP plaintext, SMB services exposure

## 5. Wireshark Capture Details
**Capture file:** `captures/192-168-1-4_http_capture.pcapng` (example)  
**Capture filter used (BPF):** `host 192.168.1.4`  
**Display filter for SYN packets:** `tcp.flags.syn == 1 && tcp.flags.ack == 0`

**Observations:**  
- TCP SYN packets from scanning host to many destination ports indicate scanning behavior.  
- HTTP traffic observed to `192.168.1.4:80`; no TLS (plaintext HTTP).  
- DNS queries to external domains present during browsing sessions.

## 6. Correlation
- Nmap shows `192.168.1.4` with AJP (8009); Wireshark captured TCP connections to port 80 (HTTP) on that host — likely a web server fronting an application container.
- `192.168.1.8` shows SMB ports open; packet captures include NetBIOS and SMB negotiation packets confirming service presence.

## 7. Recommendations
- Disable Telnet; enable SSH for remote management.  
- Restrict AJP and management ports to admin VLANs.  
- Implement LDAPS for directory services.  
- Patch SMB/Windows systems and apply firewall rules.  
- Segment IoT devices into their own VLAN with limited access.

## 8. Conclusion
This scan and capture exercise identified several hosts exposing management and legacy services. Hardening, patching, and encryption are recommended to reduce the attack surface in the lab environment.

## 9. Appendices
- Attach full sanitized Nmap outputs and the `.pcapng` capture files.  
- Provide screenshots of Wireshark TCP stream follow and highlighted packets.

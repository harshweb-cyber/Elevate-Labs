---

# Malware Analysis Report — *sample-1.eml*

### **Source: ANY.RUN Sandbox Analysis**

### **Verdict: No Threats Detected**

---

## 1. Overview

This report summarizes the dynamic and static analysis of the file **sample-1.eml**, performed using the ANY.RUN sandbox environment. The purpose is to identify possible Indicators of Compromise (IoCs), malicious behavior, process anomalies, file system artifacts, and network connections generated during execution.

Although the sandbox result states **“No threats detected”**, analysis still reports all observable behaviors for threat-hunting completeness.

---

# 2. **High-Priority Indicators of Compromise (IoCs)**

*(These are the items you should highlight in your forensic report.)*

### **2.1 File Hashes**

| Type   | Hash                                                               |
| ------ | ------------------------------------------------------------------ |
| MD5    | `4CA6586577DA9BC304FC0E11CC0A1F53`                                 |
| SHA1   | `1A301B3D06A0ABCF7F9B97E4DF076A802331DC99`                         |
| SHA256 | `35EF116A75E5E46E6859B49B60A23B4DDFE5F91D1368E0FC67A16DF698CB96E0` |

These unique identifiers can be used to check threat databases (VirusTotal, MISP, ThreatFox).

---

### **2.2 MIME & File Type**

* **MIME:** `message/rfc822`
* **File type:** Standard email `.eml`
  No executable payloads embedded.

---

### **2.3 Processes Spawned (Unusual for .eml Execution)**

| PID  | Process Name | Notes                                            |
| ---- | ------------ | ------------------------------------------------ |
| 7516 | OUTLOOK.EXE  | Loaded the .eml                                  |
| 7944 | ai.exe       | Microsoft Office AI Host                         |
| 2772 | slui.exe     | Windows activation client (triggered indirectly) |

**Observation:**
`.eml` files should normally only open in email clients.
The presence of **slui.exe** indicates a Windows licensing check triggered, but no malicious activity.

---

### **2.4 Network Connections Made**

All connections marked **whitelisted (Microsoft / Office CDN)**:

* `settings-win.data.microsoft.com`
* `ecs.office.com`
* `omex.cdn.office.net`
* `activation-v2.sls.microsoft.com`
* `ocsp.digicert.com`
* `crl.microsoft.com`
* `bing.com`
* `login.live.com`
* etc.

No suspicious domains, no Tor traffic, no C2 patterns.

---

### **2.5 Dropped / Modified Files**

OUTLOOK.EXE interacted with:

* TokenBroker cache files (`*.tbres`)
* Office Add-in cache (`OfficeSharedEntities*.bin`)
* Outlook RoamCache XML
* Cryptnet URL cache files

⚠ **No malicious artifacts dropped**, only standard Microsoft Office/Outlook operations.

---

## 3. Execution Environment (Sandbox)

* **OS:** Windows 10 Pro x64
* **Environment:** Fully instrumented ANY.RUN sandbox
* **Network:** Enabled
* **Duration:** 60 seconds
* **Privacy:** Public
* **MITM Proxy:** Off
* **Evasion Protection:** Off

---

## 4. Behavioral Analysis

### ✔ Observed Normal Behavior

* Outlook opened the `.eml` and parsed it.
* AI Host component (`ai.exe`) triggered—normal for Office add-ins.
* Several certificate validation requests occurred (CRL, OCSP).
* Windows activation client (`slui.exe`) executed normally.

### No Suspicious Behavior Observed

* No malware process injection
* No persistence mechanisms
* No registry modifications
* No exploit behavior
* No file encryption or ransomware traces
* No attempts to download payloads
* No suspicious scripts or macros

###  Important Note

Even though scans show *no malware*, emails may still contain:

* **Phishing links**
* **Social engineering content**
* **Embedded tracking resources**

Ensure manual review of the email body.

---

##  5. Network Traffic Summary

### **HTTP Requests**

Multiple GET requests made to:

* Microsoft CRLs (Certificate Revocation Lists)
* Digicert OCSP validation servers
* Office 365 update servers

All marked:

> **Reputation: Whitelisted**

### **DNS Queries**

Domains resolved include:

* `ecs.office.com`
* `settings-win.data.microsoft.com`
* `bing.com`
* `google.com`
  All benign and trusted.

---

##  6. File System Activity

Standard Outlook-related file operations:

* Outlook PST/OST handling
* TokenBroker cache access
* Cryptnet URL cache creation
* Office Add-in caching
* Template updates (`~$rmalEmail.dotm`)

No suspicious executables or scripts were created.

---

##  7. Process Tree Summary

```
OUTLOOK.EXE
 ├── ai.exe  (Office AI host)
 └── slui.exe (Windows Activation Client)
```

No malicious child processes.

---

##  8. Threat Assessment Summary

| Category                  | Result    |
| ------------------------- | --------- |
| **Malicious Indicators**  |  None    |
| **Suspicious Indicators** |  None    |
| **Info-only Indicators**  |  Present |
| **Dropped Executables**   |  None    |
| **C2 Connections**        |  None    |
| **Payload Delivery**      |  None    |
| **Exploit Behavior**      |  None    |

Overall verdict by sandbox:

> **No Threats Detected**

---

##  9. Conclusion

The `.eml` file **does not contain any active malware**, nor does it demonstrate behavior consistent with malicious attachments or exploit kits. All processes, network connections, and file modifications align with legitimate Outlook and Windows background operations.

**However:**
Email-based attacks may still leverage:

* Malicious links
* Fake sender identity
* Phishing content

A manual email body review is recommended to rule out **phishing and social engineering**.

---

##  10. IoC Summary Block (Copy/Paste Ready)

```
File Hashes:
MD5: 4CA6586577DA9BC304FC0E11CC0A1F53
SHA1: 1A301B3D06A0ABCF7F9B97E4DF076A802331DC99
SHA256: 35EF116A75E5E46E6859B49B60A23B4DDFE5F91D1368E0FC67A16DF698CB96E0

File Type: message/rfc822 (.eml)

Processes Spawned:
OUTLOOK.EXE
ai.exe
slui.exe

Network Connections:
settings-win.data.microsoft.com
ecs.office.com
omex.cdn.office.net
activation-v2.sls.microsoft.com
ocsp.digicert.com
crl.microsoft.com
etc.
(All whitelisted)

Dropped Files:
Microsoft Office cache & token files only (benign)
```

---

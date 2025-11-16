---

# **Malware Analysis Report — sample-1077.eml**

### **ANY.RUN Sandbox Summary (No Threats Detected)**

**File Type:** `.eml` (Email message)
**Verdict:** **No Malware Detected**
**Platform:** Windows 10 Professional (64-bit)

---

# **1. High-Priority Indicators of Compromise (IoCs)**

### **File Hashes (Important for Threat Intelligence & Blacklisting)**

| Type       | Value                                                                           |
| ---------- | ------------------------------------------------------------------------------- |
| **MD5**    | `1216E237544F77D4F2B967F2D79D051A`                                              |
| **SHA1**   | `2E3107C97055DDDC5166466958D1846F1EE19400`                                      |
| **SHA256** | `51E70916ED035685DE2DDE3513D8AC831A5BD2098F83E5D3C0FE665D086911DA`              |
| **SSDEEP** | `384:KjYoHI4QMZX+SYJpRo3eqI5HAGIIlOIxII0tIISII2Iu22L:Kj1HI41ZX+SCpRoFI9dIIlOI…` |

These hashes strongly identify the sample across security tools, SIEMs, EDR systems, and blocklists.

---

### **Network IoCs (Domains / IPs Contacted)**

**ALL TRAFFIC MARKED AS *WHITELISTED / LEGITIMATE***

Even though the sample is clean, we still list network IoCs:

| Domain                            | IP            | Reputation  |
| --------------------------------- | ------------- | ----------- |
| `settings-win.data.microsoft.com` | 51.124.78.146 | Whitelisted |
| `officeclient.microsoft.com`      | 52.109.32.97  | Whitelisted |
| `ecs.office.com`                  | 52.123.128.14 | Whitelisted |
| `ocsp.digicert.com`               | 23.63.118.230 | Whitelisted |
| `login.live.com`                  | 20.190.159.2  | Whitelisted |
| `crl.microsoft.com`               | 95.101.78.32  | Whitelisted |
| `www.bing.com`                    | Multiple      | Whitelisted |

**No malicious or suspicious connections detected.**

---

### **Processes Observed**

Only **benign processes** executed:

| PID  | Process       | Description               |
| ---- | ------------- | ------------------------- |
| 7424 | `OUTLOOK.EXE` | Opened the .eml file      |
| 7964 | `ai.exe`      | Microsoft AI Host         |
| 3460 | `slui.exe`    | Windows Activation Client |

**No malicious processes, no injections, and no dropped malware.**

---

### **Suspicious / Dropped Files**

Although no threats detected, ANY.RUN flagged **8 suspicious files** created by Outlook (normal behavior).

Examples:

* `OfficeSharedEntitiesUpdated.bin`
* Cryptnet cache files
* TokenBroker cache
* Office WebService cache
  (No malicious signatures; normal for Outlook operations.)

---

# 📨 **2. General Email Analysis**

### ✔ **Email Type:** RFC 822 (standard email format)

### ✔ **Lines:** Very long 347-line email

### ✔ **MIME:** message/rfc822

### ✔ **Opened with:** Microsoft Outlook

No malicious payloads, macros, or attachments were executed.

---

#  **3. Behavioral Analysis Summary**

### **✔ No malicious behavior:**

* No process injection
* No file drops
* No registry modification
* No privilege escalation
* No network attacks
* No exploit activity
* No suspicious scripts or macros

### **✔ Network Activity:**

Contains only Microsoft & Digicert certificate validation — standard Outlook behavior.

---

#  **4. TRiD File Type Identification**

* **`.eml | Email message (Var. 5)` (100% match)**

---

#  **5. Manual Phishing Checks (Recommended for All EML Files)**

Even though the file is clean, ALWAYS perform these checks:

### ** Header Analysis**

* Check **Return-Path**, **From**, **Reply-To**
* Verify domain alignment (**SPF**, **DKIM**, **DMARC**)
* Inspect sending mail server & IP reputation

### ** Body Analysis**

* Look for:

  * Urgent language ("act now", "your account is locked")
  * Grammar errors
  * Suspicious links (hover before clicking)
  * Requests for personal information or login details

### ** URL Inspection**

* Hover over links
* Check for:

  * Misspelled domains
  * Shortened links
  * Redirect chains

### ** Attachment Analysis**

* Dangerous formats: `.exe`, `.scr`, `.js`, `.vbs`, `.docm`, `.xlsm`
* For `.eml`, check embedded links/scripts

### ** Reverse Search the Sender**

* Spoofed business domains
* Unverified public email addresses

### ** Check Reputation Services**

* VirusTotal
* AbuseIPDB
* URLHaus

---

#  **6. Conclusion**

The `.eml` file **sample-1077.eml** shows:

* No malware behavior
* No suspicious or malicious indicators
* All domains and processes belong to trusted Microsoft ecosystem
* All IoCs clean

This sample is **safe** and contains **no threat indicators**.

---
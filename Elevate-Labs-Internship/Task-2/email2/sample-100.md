---

# **Sample-100 Email Forensic Report**

### **IoC-Focused Analysis (Based on Any.Run Sandbox Report)**

### **File: `sample-100.eml`**

### **Verdict: No Threats Detected**

---

## **1. Overview**

This report summarizes the analysis of the email file **sample-100.eml**, executed in a Windows 10 sandbox environment.
No malware behavior, suspicious artifacts, or malicious network activity were detected.

However, all **Indicators of Compromise (IoCs)** have been extracted for reference and correlation.

---

# **2. Indicators of Compromise (High Priority)**

## **2.1 File Hashes (MAIN IOCs)**

| Type       | Hash                                                               |
| ---------- | ------------------------------------------------------------------ |
| **MD5**    | `4DD77CA48BA1C3437713B8DD8B4EFF7E`                                 |
| **SHA1**   | `34096D58535F2C201B15FB577BB9316BE5B8EFE5`                         |
| **SHA256** | `9FB2E491E28E6848614AE9539E2F685EE5C75357339505998B91FB9B89B3127E` |
| **SSDEEP** | `192:I006uT+iv2fXCMzy8tq5a8WTv1IfEKqfWsd313GesvYwHsgOTvfcn+7ejXdG` |

> **Use these for VirusTotal, SIEM correlation, and threat hunting.**

---

## **2.2 File Information**

* **MIME Type:** `message/rfc822`
* **File Type:** RFC 822 Email
* **Encoding:** UTF-8
* **Lines:** 396
* **CRLF line endings**

---

# **3. Behavioral Summary**

During execution, the following programs ran:

### **Executed Processes**

1. **OUTLOOK.EXE** – Loaded the .eml file
2. **ai.exe** – Microsoft Office AI Helper
3. **slui.exe** – Windows Activation Client

No malicious processes, injections, persistence, or suspicious activity were detected.

---

# **4. File Activity (Potential IoCs)**

These files were created/read/modified by Outlook while parsing the email.
They are **not malicious**, but included for completeness.

Common Outlook-related cache files:

* `C:\Users\admin\AppData\Local\Microsoft\TokenBroker\Cache\*.tbres`
* `C:\Users\admin\AppData\Local\Microsoft\Office\16.0\AddInClassifierCache\OfficeSharedEntities*.bin`
* `C:\Users\admin\AppData\Local\Microsoft\Outlook\RoamCache\*.dat`
* `C:\Users\admin\AppData\LocalLow\Microsoft\CryptnetUrlCache\*`

> These are normal for Outlook processing emails.

---

# **5. Network Indicators**

### **Main Observation:**

**All network connections were to Microsoft or trusted certificate services.**
No suspicious command-and-control (C2) traffic.

### **Domains Queried** *(ALL WHITELISTED)*:

* `settings-win.data.microsoft.com`
* `ecs.office.com`
* `ocsp.digicert.com`
* `crl.microsoft.com`
* `login.live.com`
* `office.net`
* `messaging.lifecycle.office.com`
* `update.microsoft.com`

### **IP Addresses Accessed**

(All legitimate Microsoft / Akamai CDNs)

Examples:

* `52.123.128.14`
* `23.63.118.230`
* `95.101.78.32`
* `4.231.128.59`

> None of these are malicious.

---

# **6. Suspicious / Malicious Indicators**

According to Any.Run:

* **0 malicious indicators**
* **0 suspicious indicators**
* **0 anomalies**
* **0 malware signatures**

Thus, the email is **safe**.

---

# **7. Analysis Conclusion**

Based on static and dynamic analysis:

No malware launched
No scripts dropped
No malicious links contacted
No attachments executed
No persistence or registry modifications

### **Final Verdict:**

**The email is benign. No malware behavior observed.**

---

# **8. Recommendations**

Even though this specific sample is safe, include these steps in email forensics:

### **When Reviewing Emails Manually**

* Check sender domain authenticity
* Inspect message headers (SPF, DKIM, DMARC)
* Hover over links (check real destination)
* Look for suspicious attachments (.exe, .js, .vbs, .html)
* Check for grammar mistakes/social engineering
* Validate unexpected requests for payments, OTPs, passwords
* If unsure, open attachments in a sandbox

---

# **9. Summary for SOC / Research Use**

| Category           | Details                                   |
| ------------------ | ----------------------------------------- |
| **Sample Name**    | sample-100.eml                            |
| **Threat Level**   | None                                      |
| **Hash IoCs**      | Included above                            |
| **Network IoCs**   | Microsoft only                            |
| **Behavior**       | Clean                                     |
| **Recommendation** | No threat, but store IoCs for correlation |

---
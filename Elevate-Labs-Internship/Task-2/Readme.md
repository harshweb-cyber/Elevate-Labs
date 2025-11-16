

# Manual Phishing Email Analysis (Must-Do Checks)

Even if automated tools report *“No Malware Found,”* phishing emails often bypass antivirus detection because they rely on *social engineering*.
Therefore, manual verification is essential.

Below are the **mandatory steps** you must follow to manually inspect any suspicious `.eml` file:


## 1. Verify Sender Details

### **Check the “From” Address**

* Look for small spelling errors (e.g., `micorsoft-support@...`, `amaz0n-help@...`)
* Confirm the domain is legitimate

  *  `support@paypal.com`
  *  `support@paypal-secure-check.net`

### **Compare “From” vs “Reply-To”**

Attackers often spoof the “From” field but use a different “Reply-To”.

Example:

```
From: support@microsoft.com
Reply-To: techsupport@outlook.com
```

Mismatch = **high phishing risk**.



## 2. Analyze Subject & Body Content

Look for typical phishing triggers:

* Urgency: *“Verify immediately or your account will be closed”*
* Threats: *“Unauthorized login detected”*
* Rewards: *“You won a prize!”*
* Generic greeting: *“Dear User”*, *“Dear Customer”*

### **Language Indicators**

* Grammar mistakes
* Odd formatting
* Unprofessional tone



## 3. Inspect All URLs (Without Clicking)

Hover over links and check if:

* The displayed text ≠ actual URL
* The URL contains suspicious domains, numbers, or IPs

Examples of bad indicators:
```
* `http://192.168.0.55/login`
* `http://microsoft-login-security.xyz`
```
Use online tools:

* VirusTotal
* URLScan.io



## 4. Check Attachments Carefully

Flag suspicious extensions:
```
* `.exe`, `.bat`, `.cmd`, `.vbs`, `.ps1`
* `.docm`, `.xlsm` (macro-enabled)
* `.zip`, `.rar`, `.iso`
* PDFs with embedded links or scripts
```
If sender is unknown → **never open attachments**.



## 5. Inspect Email Headers (Full Header Analysis)

Check:

* **SPF**
* **DKIM**
* **DMARC**

If they fail:


spf=fail
dkim=none
dmarc=fail


→ Sender is likely spoofed.

Also check **Received-From** flow:

* Look for unexpected foreign servers
* Multiple untrusted hops



##  6. Watch for Tracking Pixels or Remote Images

Indicators:

* HTML emails requesting to “Load remote content”
* Hidden images like `1x1 pixel.gif`
* Unusual external image servers

This is commonly used to track victims.



## 7. Look for Requests for Sensitive Information

Legitimate organizations **never** ask for:

* Passwords
* OTPs
* Credit card PIN
* Aadhaar/PAN info
* Banking data

If email asks for these → **it's phishing**.



## 8. Analyze Tone & Intention

Phishing often uses:

* Fear
* Urgency
* Rewards
* Authority pressure

If the message is designed to trigger a quick emotional response → beware.



## 9. Inspect Branding & Design

Check for:

* Blurry logos
* Wrong colors
* Slight deviations from official templates
* Fake signatures

Compare with a legitimate email from the same company.



## 10. Recommended Tools for Manual Review

* ANY.RUN Email Analyzer
* emlAnalyzer
* MXToolBox Header Analyzer
* VirusTotal (URL/File)
* URLscan.io
* OLETools (office files)



#  Quick Phishing Detection Checklist


[ ] Sender address looks legitimate
[ ] From and Reply-To match
[ ] No urgent or threatening language
[ ] No grammar/spelling errors
[ ] Links point to correct domain
[ ] URLs verified in VirusTotal/URLscan
[ ] Attachments safe (no suspicious extensions)
[ ] SPF/DKIM/DMARC pass in header
[ ] No brand spoofing indicators
[ ] No request for sensitive information



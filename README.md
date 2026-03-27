
# 🛡️ SOC Investigation Report: Revenue.ie Smishing Campaign
**Analyst:** Sarath Pulicherla  
**Focus:** Infrastructure Analysis, 🚨 Phishing Investigation Report – Revenue SMS Scam

---

## 📌 1. Introduction

This project presents a real-world phishing investigation conducted from a **Security Operations Center (SOC)** perspective.

A suspicious SMS claiming to be from Revenue (Irish Tax Authority) was received, offering a tax refund and asking the user to log in via a provided link.

Instead of immediately assuming it was malicious, a structured investigation process was followed to verify its legitimacy.

---

## 📩 2. Incident Overview

### 🔹 What Happened?
- Received an SMS claiming tax refund
- Included a login link
- Website looked similar to official Revenue page

### 🔹 Suspicious Indicators
- Domain was **not** official (`.com` instead of `.ie`)
- Website buttons were **not working**
- Redirection behavior was unusual

---

## 🧠 3. Key Cybersecurity Terms 

### 🔐 Phishing
A type of cyber attack where attackers trick users into entering sensitive information (like passwords or bank details) on fake websites.

### 🌐 Domain
The name of a website (example: google.com)

### 🔗 Subdomain
A smaller part of a domain (example: mail.google.com)

### 📡 DNS (Domain Name System)
A system that converts domain names into IP addresses (like a phonebook for the internet)

### 🧾 WHOIS
A tool used to check who owns a domain and when it was created

### 🌍 IP Address
A unique number assigned to every server on the internet

### 🛡️ Cloudflare
A service that protects and hides the real server behind a website

### 🔒 SSL/TLS
Encryption used to secure websites (HTTPS)

### 🚨 IOC (Indicators of Compromise)
Evidence that suggests a system or website is malicious

---

## 🔍 4. Investigation Methodology

---

### 🔎 4.1 SMS Evidence

![SMS Evidence](Evidence/sms.png)

✔ Shows the original phishing message  
✔ Contains suspicious link  

---

### 🌐 4.2 Phishing Website

![Phishing Page](Evidence/phishing_page.png)

✔ Fake login page mimicking Revenue  
✔ Requests sensitive user data  

---

### ⚠️ 4.3 Broken Website Behavior

![Broken UI](Evidence/phishing_page.png)

✔ Buttons do not work  
✔ Page reloads instead of navigating  

👉 Indicates a **fake/static phishing page**

---

### 🧾 4.4 WHOIS Analysis

![WHOIS + DNS](Evidence/whois_dns_lookup.png)

### Result:
- No match found for domain

### Meaning:
- Domain is hidden OR newly created  
- Legitimate organizations do not hide domain details  

---

### 🌍 4.5 DNS Resolution

![DNS Analysis](Evidence/whois_dns_lookup.png)

### Result:
- IP Addresses:
  - 104.21.83.22
  - 172.67.167.84

### Meaning:
- Hosted via Cloudflare  
- Real server is hidden  

---

### 🌐 4.6 Nameserver Analysis

![Nameserver Info](Evidence/dns_ns_ip_analysis.png)

### Result:
- arvind.ns.cloudflare.com  
- annalise.ns.cloudflare.com  

### Meaning:
- Uses Cloudflare DNS  
- Not official government infrastructure  

---

### ❌ 4.7 Root Domain Check

![Root Domain](Evidence/dns_ns_ip_analysis.png)

### Result:
- No output from `dig`

### Meaning:
- Root domain is inactive  
- Only phishing subdomain is active  

👉 Advanced phishing technique  

---

### 🌍 4.8 IP Address Analysis

![IP WHOIS](Evidence/dns_ns_ip_analysis.png)

### Result:
- IP belongs to Cloudflare  

### Meaning:
- Attacker is hiding real server  
- Makes tracking difficult  

---

### 🧪 4.9 URLScan Analysis

![URLScan](Evidence/urlscan.png)

### Key Findings:
- Domain created recently  
- No classification yet  
- SSL valid for 3 months  

### Meaning:
- Early-stage phishing attack  
- Not yet detected by tools  

---

## 🚨 5. Key Findings

- Newly created domain 🚩  
- Fake domain impersonating Revenue 🚩  
- Cloudflare used for anonymity ⚠️  
- Root domain inactive 🚩  
- Broken website functionality 🚩  
- Not yet flagged by security tools ⚠️  

---

## 🧾 6. Indicators of Compromise (IOCs)

| Type | Value |
|------|------|
| Domain | revenue.onlinetax-credit.com |
| Root Domain | onlinetax-credit.com |
| IP Address | 104.21.83.22 |
| IP Address | 172.67.167.84 |
| Nameservers | arvind.ns.cloudflare.com |
| Nameservers | annalise.ns.cloudflare.com |

---

## ⚠️ 7. Risk Analysis

### 🔴 Risks
- Credential theft  
- Identity fraud  
- Financial loss  

### 💥 Impact
If user enters data:
- Attacker can access tax account  
- Change bank details  
- Steal refunds  

---

## 🧠 8. MITRE ATT&CK Mapping

| Technique | Description |
|----------|------------|
| T1566 | Phishing |
| T1204 | User Execution |
| T1056 | Credential Capture |

---

## 🛡️ 9. Recommendations

- Do not click unknown SMS links  
- Always verify official domains  
- Use Multi-Factor Authentication (MFA)  
- Report suspicious messages  

---

## 📊 10. Conclusion

This investigation confirms a **high-confidence phishing attack**.

The attacker used:
- Domain impersonation  
- Cloudflare infrastructure  
- Selective DNS setup  

This case highlights the importance of:
- Manual investigation  
- Critical thinking  
- Not relying only on automated tools  

---

## 📸 11. Evidence

All screenshots are stored in the `Evidence/` folder.

---

## 🙋‍♂️ 12. Author

**Sarath Pulicherla**  
Aspiring SOC Analyst | Cybersecurity Enthusiastisk Assessment & Public Safety  
**Case ID:** IR-2026-03-IE

---

## 1. Executive Summary
This report documents a **True Positive** Smishing attack targeting Irish citizens. The attacker impersonated the **Revenue Commissioners** to harvest sensitive data (PPS Numbers, DOB, and Bank Credentials). This investigation follows the **NIST Incident Response Lifecycle** to detect, analyze, and contain the threat.

---

## 2. Technical Investigation (Step-by-Step)

### A. Initial Access (The SMS Lure)
The attack started with a high-urgency SMS regarding a tax repayment.
* **Malicious URL:** `https://revenue.onlinetax-credit.com`

<p align="center">
  <img src="01.Suspicious%20Png.png" width="350" title="Malicious SMS Lure">
  <br><i>Figure 1: Original Smishing SMS received by the target.</i>
</p>

### B. Infrastructure & OSINT Analysis
Using **urlscan.io** and **Whois**, I identified the following:
* **Registrar:** NICENIC INTERNATIONAL GROUP (Often used for malicious registrations).
* **IP Address:** 104.21.83.22 (Proxied via Cloudflare to hide the actual host).

<p align="center">
  <img src="08.Urlscan.png" width="700" title="urlscan.io Analysis Results">
</p>

### C. Defense Evasion (Cloaking)
The site utilized **User-Agent Filtering**. It redirected desktop browsers to the real `revenue.ie` while showing the phishing page only to mobile users. This prevents automated security scanners from flagging the site.

<p align="center">
  <img src="02.phishing%20page.png" width="350" title="Mobile Phishing Page">
</p>

---

## 3. Data Misuse & Impact Analysis (Critical)
If a victim submits their data, the attacker can perform:
1. **Financial Drain:** Diverting tax refunds or logging into bank accounts.
2. **Identity Theft:** Using PPS numbers to apply for fraudulent loans or social welfare.
3. **Secondary Attacks:** Selling the "validated" victim list to other criminal groups.

---

## 4. Cybersecurity Framework Mapping

### 🛡️ MITRE ATT&CK Mapping
| Tactic | Technique ID | Description |
| :--- | :--- | :--- |
| **Initial Access** | T1566.002 | Phishing: Spearphishing Link (via SMS). |
| **Reconnaissance** | T1594 | Search Victim-Owned Websites (Cloning Revenue UI). |
| **Defense Evasion** | T1564.010 | Infrastructure Hiding via Cloudflare Proxy. |

### 🚨 NIST Incident Response Lifecycle
* **Detection:** Identified domain mismatch (`.com` vs `.ie`).
* **Analysis:** Verified malicious behavior using a Virtual Machine and OSINT.
* **Containment:** Reported the URL to **Google Safe Browsing** for global blocking.

---

## 5. Lessons Learned & Recommendations
* **Always Check the TLD:** Government sites in Ireland use `.ie`, never `.com`.
* **Zero Trust:** Never trust a link from an SMS, even if it looks professional.
* **Mitigation:** Organizations should implement **SPF** and **DMARC** to prevent their brand from being used in phishing.

---

## 6. Glossary for Non-Technical Readers
* **Smishing:** Phishing via SMS.
* **SPF (Sender Policy Framework):** An "Approved Guest List" for email. 
* **DMARC:** An "Instruction Manual" telling servers to block fake emails. 
* **True Positive:** A confirmed real threat.

---
**Status:** 🛡️ Site Reported & Contained  
<p align="center">
  <img src="09.Report%20google.png" width="700" title="Google Safe Browsing Report">
</p>


# 🛡️ SOC Investigation Report: Revenue.ie Smishing Campaign
**Analyst:** Sarath Pulicherla  
**Focus:** Infrastructure Analysis, Risk Assessment & Public Safety  
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

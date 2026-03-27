# 🛡️ Incident Report: Revenue.ie Smishing & Identity Theft Analysis
**Analyst:** Sarath Pulicherla | **Date:** March 27, 2026 | **Status:** Confirmed Malicious

---

## 1. Executive Summary
This project documents a real-world investigation into a **Smishing** attack targeting Irish citizens. The attacker impersonated the **Revenue Commissioners** to steal PPS numbers and banking data.

---

## 2. Technical Investigation

### A. Initial Access (The Hook)
The attack arrived via SMS with a high-pressure lure regarding tax repayments.
* **Lure:** "MyGOV: Your Tax credit for 2025/2026 repayment is now due."
* **Link:** `https://revenue.onlinetax-credit.com`

<p align="center">
  <img src="01.Suspicious%20Png.jpeg" width="400" alt="SMS Evidence">
</p>

### B. Infrastructure & OSINT Analysis
Using **urlscan.io** and Linux terminal tools, I identified the backend infrastructure.
* **IP Address:** 104.21.83.22 (Proxied via Cloudflare)
* **Registrar:** NICENIC INTERNATIONAL GROUP CO., LIMITED
* **Domain Age:** Created February 25, 2024

<p align="center">
  <img src="08.Urlscan.png" width="600" alt="urlscan Analysis">
</p>

### C. Defense Evasion (Cloaking)
The site uses **User-Agent Filtering**. It serves the phishing page to mobile users but redirects desktop users to the real site to hide from scanners.

<p align="center">
  <img src="02.phishing%20page.jpeg" width="400" alt="Phishing Page">
</p>

---

## 3. Impact & Risk Management
### ⚠️ Data Misuse Scenarios
* **Financial Fraud:** Attackers can divert tax refunds by gaining access to myAccount portals.
* **Identity Theft:** PPS numbers and DOBs can be sold or used to apply for fraudulent loans.

### 🛡️ Mitigation Strategies
* **SPF (Sender Policy Framework):** A "Guest List" for email that tells the internet which servers are officially allowed to send mail for a company.
* **DMARC:** An "Instruction Manual" for email servers. It tells them what to do with fake emails—like blocking them entirely.

---

## 4. Cybersecurity Frameworks
* **MITRE ATT&CK:** T1566.002 (Spearphishing Link via SMS).
* **NIST IR Lifecycle:** Performed Detection, Analysis, and Containment.

## 5. Containment (Take-Down)
Reported the URL to **Google Safe Browsing** to protect the public.

<p align="center">
  <img src="09.Report%20google.png" width="600" alt="Report Confirmation">
</p>

---

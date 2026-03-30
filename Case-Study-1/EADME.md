# 🚨 Phishing Investigation Report – Revenue SMS Scam

---

## 📌 1. Introduction

This project presents a real-world phishing investigation conducted using a **Security Operations Center (SOC)** approach.

A suspicious SMS claiming to be from Revenue (Irish Tax Authority) was received. The message attempted to lure the user into clicking a malicious link and entering sensitive information such as PPS number, date of birth, and account credentials.

Instead of assuming it as malicious immediately, a structured investigation methodology was followed to validate the threat.

---

## 📩 2. Incident Overview

- **Source:** SMS (Social Engineering Vector)
- **Attack Type:** Phishing / Credential Harvesting
- **Target:** General public (Revenue users)
- **Malicious URL:** `revenue.onlinetax-credit.com`

### 🚨 Initial Suspicion Indicators

- Domain mismatch (`.com` vs official `.ie`)
- Urgency-based message (tax refund bait)
- Suspicious website behavior
- Request for sensitive personal and financial data

---

## 🧠 3. Key Terminology (Beginner Friendly)

- **Phishing:** A cyber attack where attackers impersonate trusted entities to steal sensitive information.
- **Domain:** The address of a website (e.g., google.com).
- **Subdomain:** A subdivision of a domain (e.g., login.google.com).
- **DNS (Domain Name System):** Translates domain names into IP addresses.
- **WHOIS:** A service used to retrieve domain registration details.
- **IP Address:** A unique identifier assigned to servers.
- **Cloudflare:** A service that acts as a proxy, hiding the actual server.
- **IOC (Indicators of Compromise):** Evidence indicating malicious activity.

---

## 🔍 4. Investigation Methodology

---

### 📱 4.1 Suspicious SMS Evidence

<p align="center">
  <img src="images/01_Suspicious.png" width="150">
</p>

✔ SMS contains phishing link  
✔ Uses social engineering (tax refund lure)

---

### 🌐 4.2 Phishing Website Analysis

<p align="center">
  <img src="images/02_phishing_page.png" width="150">
</p>

✔ Website mimics legitimate Revenue login  
✔ Requests sensitive user credentials  

---

### ⚠️ 4.3 Website Behavior Analysis

- Navigation links not functional  
- Buttons reload same page  
- No real backend interaction  

👉 Indicates a **static phishing page designed for credential harvesting**

---

### 🧾 4.4 WHOIS Analysis

<p align="center">
  <img src="images/03_whois_result.png" width="500">
</p>

### Findings:
- No WHOIS record found  

### Interpretation:
- Domain may be newly registered or hidden  
- Legitimate organizations maintain transparent records  

---

### 🌍 4.5 DNS Resolution

<p align="center">
  <img src="images/04_dns_resolution.png" width="500">
</p>

### Findings:
- IP Addresses:
  - `104.21.83.22`
  - `172.67.167.84`

### Interpretation:
- Hosted behind Cloudflare  
- Real origin server is masked  

---

### 🌐 4.6 Nameserver Analysis

<p align="center">
  <img src="images/05_nameserver_info.png" width="500">
</p>

### Findings:
- arvind.ns.cloudflare.com  
- annalise.ns.cloudflare.com  

### Interpretation:
- Cloudflare-managed DNS  
- No association with official government infrastructure  

---

### ❌ 4.7 Root Domain Analysis

<p align="center">
  <img src="images/06_root_domain_check.png" width="500">
</p>

### Findings:
- No DNS resolution for root domain  

### Interpretation:
- Only phishing subdomain is active  
- Indicates **selective deployment strategy** used by attackers  

---

### 🌍 4.8 IP Address Analysis

<p align="center">
  <img src="images/07_ip_analysis.png" width="500">
</p>

### Findings:
- IP belongs to Cloudflare network  

### Interpretation:
- Used to hide attacker infrastructure  
- Prevents direct attribution  

---

### 🧪 4.9 URLScan Analysis

<p align="center">
  <img src="images/08_Urlscan.png" width="500">
</p>

### Findings:
- Domain created recently  
- No classification in threat intelligence databases  
- TLS certificate valid for short duration  

### Interpretation:
- Early-stage phishing campaign  
- Not yet widely detected  

---

### 📊 4.10 External Validation (Google Safe Browsing)

<p align="center">
  <img src="images/09_google_report.png" width="500">
</p>

### Findings:
- No classification  

### Interpretation:
- Confirms newly launched phishing infrastructure  

---

## 🚨 5. Key Technical Findings

- Newly registered domain (high-risk indicator)
- Domain impersonation targeting Revenue users
- Cloudflare used for anonymization
- Subdomain-only activation (evasion technique)
- Static phishing page behavior
- Not detected by automated tools

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

### 💥 Potential Impact
- Unauthorized account access  
- Bank detail manipulation  
- Fraudulent transactions  

---

## 🧠 8. MITRE ATT&CK Mapping

| Technique ID | Technique |
|-------------|----------|
| T1566 | Phishing |
| T1204 | User Execution |
| T1056 | Credential Capture |

---

## 🛡️ 9. Security Recommendations

- Avoid clicking links from unknown SMS messages  
- Verify official domains before entering credentials  
- Enable Multi-Factor Authentication (MFA)  
- Use trusted security tools  
- Report phishing attempts to authorities  

---

## 📚 10. Lessons Learned

- Newly created phishing domains often bypass detection tools  
- Manual investigation is critical in early-stage threats  
- DNS and domain analysis provide strong indicators  
- Cloudflare infrastructure is frequently abused by attackers  
- User awareness is the first line of defense  

---

## 📊 11. Conclusion

This investigation confirms a **high-confidence phishing attack**.

The attacker leveraged:
- Domain impersonation  
- Cloudflare proxy infrastructure  
- Selective DNS configuration  

This case demonstrates the importance of:
- Structured investigation  
- Critical thinking  
- Real-world analysis beyond automated tools  

---

## 📸 12. Evidence

All screenshots are included in this repository.

---

## 🙋‍♂️ 13. Author

**Sarath Pulicherla**  
Aspiring SOC Analyst | Cybersecurity Learner

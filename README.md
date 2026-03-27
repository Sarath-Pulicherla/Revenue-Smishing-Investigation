# 🚨 Phishing Investigation Report – Revenue SMS Scam

---

## 📌 Introduction

This project documents a real-world phishing investigation conducted from a Security Operations Center (SOC) perspective.

A suspicious SMS claiming to be from Revenue (Irish Tax Authority) was received, offering a tax refund and requesting login through a provided link. Due to multiple red flags, a structured investigation was performed.

---

## 📩 Incident Overview

- **Source:** SMS message  
- **Theme:** Tax refund scam  
- **URL:** revenue.onlinetax-credit.com  

### 🚨 Initial Red Flags
- Domain mismatch (.com instead of official .ie)
- Suspicious website behavior
- Request for sensitive user data

---

## 🧠 Key Concepts (Simple)

- **Phishing:** Fake message/website used to steal sensitive data  
- **Domain:** Website name  
- **DNS:** Converts domain → IP address  
- **WHOIS:** Domain registration details  
- **IP Address:** Server identity  
- **Cloudflare:** Service used to hide real server  
- **IOC:** Evidence of attack  

---

## 🔍 Investigation Steps

### 📱 SMS Evidence
![SMS](Evidence/01_suspicious.png)

---

### 🌐 Phishing Page
![Phishing](Evidence/02_phishing_page.png)

---

### 🧾 WHOIS Analysis
![WHOIS](Evidence/03_whois_result.png)

**Finding:**
- No WHOIS record → suspicious / hidden domain

---

### 🌍 DNS Resolution
![DNS](Evidence/04_dns_resolution.png)

**Finding:**
- IPs:
  - 104.21.83.22  
  - 172.67.167.84  

➡ Hosted via Cloudflare (masking real server)

---

### 🌐 Nameserver Analysis
![Nameserver](Evidence/05_nameserver_info.png)

**Finding:**
- Cloudflare DNS used  
- Not official infrastructure  

---

### ❌ Root Domain Check
![Root Domain](Evidence/06_root_domain_check.png)

**Finding:**
- No output  
➡ Only phishing subdomain active  

---

### 🌍 IP Analysis
![IP](Evidence/07_ip_analysis.png)

**Finding:**
- Belongs to Cloudflare  
➡ Used for anonymity  

---

### 🧪 URLScan Analysis
![URLScan](Evidence/08_urlscan.png)

**Finding:**
- Newly created domain  
- Not yet flagged  
➡ Early-stage phishing  

---

### 📊 Google Safe Browsing
![Google](Evidence/09_google_report.png)

**Finding:**
- No classification  
➡ Confirms new attack  

---

## 🚨 Key Findings

- Newly created domain 🚩  
- Fake Revenue impersonation 🚩  
- Cloudflare masking ⚠️  
- Root domain inactive 🚩  
- Fake website behavior 🚩  
- Not detected by tools ⚠️  

---

## 🧾 Indicators of Compromise (IOCs)

- revenue.onlinetax-credit.com  
- 104.21.83.22  
- 172.67.167.84  
- arvind.ns.cloudflare.com  
- annalise.ns.cloudflare.com  

---

## ⚠️ Risk Analysis

### Risks:
- Credential theft  
- Identity fraud  
- Financial loss  

### Impact:
- Account takeover  
- Bank detail manipulation  
- Refund theft  

---

## 🧠 MITRE ATT&CK

- T1566 – Phishing  
- T1204 – User Execution  
- T1056 – Credential Capture  

---

## 📚 Lessons Learned

- New phishing sites are often undetected  
- Manual investigation is critical  
- DNS & domain analysis are powerful  
- Cloudflare is commonly abused by attackers  
- User awareness is key defense  

---

## 📊 Conclusion

This investigation confirms a **high-confidence phishing attack**.

The attacker used:
- Domain impersonation  
- Cloudflare infrastructure  
- Selective DNS setup  

---

## 📸 Evidence

All screenshots are stored in the `Evidence/` folder.

---

## 🙋‍♂️ Author

Sarath Pulicherla  
Aspiring SOC Analyst

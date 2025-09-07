
#  Phishing Email Analysis & Investigation Project  

## 🔹 Overview  
This project simulates a **real-world phishing campaign** and documents the **SOC analyst investigation process** from email delivery to artifact collection and reporting. The phishing email was crafted to appear as a **voicemail notification from Office**, leading victims to a fake login page where credentials could be harvested.  

The project demonstrates both the **attacker’s perspective** (hosting a phishing page, logging credentials) and the **defender’s perspective** (analyzing the phishing email, capturing traffic with Wireshark, and extracting IOCs).  

---

## 🔹 Skills & Tasks Demonstrated  
The lab covers a wide range of **Phishing Email Investigation and Analysis tasks**, including:

<p float="left">  
<code>Email Header Review</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Threat Analysis</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Spoofing Detection</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Malicious Link Analysis</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Networking & Traffic Analysis</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Credential Harvesting Awareness</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Incident Response Workflows</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>IOC Extraction & Threat Hunting</code> &nbsp;&nbsp; | &nbsp;&nbsp;  <code>SOC Investigation Reporting</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Defensive Security Mindset</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Email Analysis Tool Proficiency</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Wireshark Packet Capture</code> &nbsp;&nbsp; | &nbsp;&nbsp;  <code>Attack Simulation (Python Server)</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Artifact Documentation</code>  </p>

---

## 🔹 Lab Network Architecture  

| Component        | Role / Purpose | IP Address |
|------------------|----------------|------------|
| **pfSense Firewall** | DHCP management, lab network isolation, LAN gateway | 192.168.0.1 |
| **Attacker Machine (Ubuntu)** | Hosted phishing page with Python HTTP server, captured User-Agent strings and harvested credentials | 192.168.0.13 |
| **Victim Machine (Windows 10)** | Received phishing email, opened voicemail link, interacted with phishing login page | 192.168.0.12 |
| **SOC Analyst Workstation** | Performed email header analysis, packet review, and artifact collection using Wireshark, Sublime, MXToolbox, Google Admin Toolbox, REMnux | 192.168.0.11 |
| **Phishing Web Server (Python)** | Served fake voicemail login page and logged credential submissions | 192.168.0.13 (same as attacker) |
| **Wireshark Capture Point** | Captured SMTP, DNS, and HTTP/HTTPS traffic for analysis | Between Victim & Attacker |

**Tools Used:** Wireshark, Python (HTTP Server),Sublime Text, MXToolbox , REMnux, Mailtower, dnstwister, phishtool, Virtualization..
<img width="975" height="741" alt="image" src="https://github.com/user-attachments/assets/60c3e252-f997-4daa-a283-9e30877b9f9c" />



---
## 🔹 Attack Workflow  
1. `server01.py` → **Phishing Web Server** → **Hosts the fake login page**  → **Listens for victim requests on port 80**  → **Logs every time a victim visits the phishing site** → **Captures credentials**.
   
   <img width="621" height="297" alt="image" src="https://github.com/user-attachments/assets/872b2717-dc0a-4a67-8fce-2d74a362870c" />
   <img width="671" height="574" alt="image" src="https://github.com/user-attachments/assets/c8a99650-0a8d-4b10-9f6d-0c0b13da3762" />


   <img width="715" height="182" alt="image" src="https://github.com/user-attachments/assets/b6897286-6aa2-4aba-a242-1cb96d5c412c" />
   
---
   2. `getalert.py` → **Tracking Pixel Server** → **Hosts a tracking pixel (tracking_pixel.png) on port 8000**  → **Logs IP address, User-Agent (browser/email client), and timestamp**
      
       <img width="923" height="391" alt="image" src="https://github.com/user-attachments/assets/0c2d1eb2-d456-4e06-8290-fa6d40b83153" />
       <img width="1008" height="426" alt="image" src="https://github.com/user-attachments/assets/d872cc5f-4bd0-4c70-bc8d-a2ba19af1398" />
       <img width="1492" height="132" alt="image" src="https://github.com/user-attachments/assets/953cd05b-9469-42a3-8039-8c896ec6463c" />
       
---
## 🔹 Victim Workflow Simulation 
1. `Windows 10 Thunderbird inbox` → **Victim Receives the Email** → **Victim Opens the Email**  → **Victim Clicks the Link**  → **Victim Submits Credentials**  → **Awareness Outcome**
   
    <img width="654" height="532" alt="image" src="https://github.com/user-attachments/assets/021128e4-3e8c-4074-b9b8-cf19be2eabd1" />
    <img width="997" height="826" alt="image" src="https://github.com/user-attachments/assets/3234b915-945f-4152-ad1d-6f712aed824f" />
    <img width="765" height="418" alt="image" src="https://github.com/user-attachments/assets/22deabd8-b8b5-45f2-a8c5-5e0b4ee15166" />
    
 ---
 ## 🔹 Phishing Email Investigation  And Report (with Wireshark/ Sublime Txt/ REMnux/ phishtool)
1. `SOC analyst / incident responder` → **Collect the Phishing Email** → **Header Analysis**  → **Body & Link Analysis**  → **Indicator of Compromise (IOC) Extraction**  → **Packet Capture**  → **Open-Source Intel (Safe Investigation)**

---



# 📧 Phishing Email Investigation Report

**Project:** Phishing Analysis Lab  
**Date of Investigation:** 2025-08-30  
**Analyst:** [Dammie Ajewole]  

---

## 1. Email Overview

- **Subject:** 📩 New Voicemail Received (37 seconds)  
- **From:** Voicemail Service <voicemail@office365-support.com>  
- **Reply-To:** cyberlocal@proton.me  
- **To:** johndoe@secmode.com  
- **Return-Path:** <cyberlocal@proton.me>  
- **Message-ID:** <20250830164500.ABC123@office365-support.com>  
- **Date:** Sat, 30 Aug 2025 16:45:00 -0400  

---

## 2. Email Header Analysis

| Header Field            | Value |
|--------------------------|-------|
| **Return-Path**          | cyberlocal@proton.me |
| **Received From**        | mail.proton.me [192.0.2.55] |
| **X-Originating-IP**     | 192.0.2.1 |
| **SPF Result**           | Fail |
| **DKIM Result**          | None |
| **DMARC Result**         | Fail |


<img width="624" height="321" alt="image" src="https://github.com/user-attachments/assets/64c8d2d6-7268-4ac9-b1e5-3a8ab4719cef" />
<img width="549" height="348" alt="image" src="https://github.com/user-attachments/assets/f8aa9a54-7ad8-419e-867c-b4f10a1122c2" />



---

## 3. Body & Social Engineering Techniques

- Claims to be from **Microsoft Voicemail Service**.  
- Urgency tactic: "Message will be deleted after 24 hours."  
- Call-to-action: Click "Listen to Voicemail" button.  
- Spoofed branding (uses "Office365" in sender domain).  

<img width="491" height="560" alt="image" src="https://github.com/user-attachments/assets/1481db56-3728-414a-b488-1b18fbda1497" />


---

## 4. Indicators of Compromise (IOCs)

### URLs
- `http://192.168.0.13/index.html` → Malicious link disguised as voicemail button.  
- `http://192.168.0.13:8000/tracking_pixel.png?id=voicemail_lab_20250830` → Tracking pixel beacon.
- `http://192.168.0.13/login` → Phishing login page.
  <img width="873" height="781" alt="image" src="https://github.com/user-attachments/assets/d2028ea0-8a0b-4c13-ba7c-7926343847f2" />
  <img width="1052" height="568" alt="image" src="https://github.com/user-attachments/assets/edc207ba-0b9b-4800-b6ad-9cd0240e8603" />
  <img width="1905" height="942" alt="image" src="https://github.com/user-attachments/assets/1e412b42-f9af-4c0a-b01e-a6c2518be0c6" />



### Email Addresses
- **Sender:** voicemail@office365-support.com (spoofed)  
- **Reply-To:** cyberlocal@proton.me  

### Attachments
- `Voicemail_Transcription.txt` (Analyze with **Virustotal** and **phishtool**).  

<img width="1558" height="482" alt="image" src="https://github.com/user-attachments/assets/d4ce8916-56b6-4c79-a8a7-642b00602e8f" />
<img width="1365" height="534" alt="image" src="https://github.com/user-attachments/assets/e5f43a3a-1559-4ce0-bc7d-8be0917c12c6" />

--

## 4.1 Network Traffic Analysis (Wireshark)

- Wireshark on SOC workstation, filtered with: **ip.addr == 192.168.0.12 && ip.addr == 192.168.0.13** **http.request.method==POST** **http.request.uri contains "tracking_pixel"**  To **Observed victim → attacker traffic when the phishing link was clicked.**

- Captured **HTTP GET request** to `/index.html` (phishing page).  
- Captured **HTTP POST request** with submitted credentials.  
- Identified **tracking pixel request** to `/tracking_pixel.png`, confirming beaconing.  
<img width="1924" height="581" alt="image" src="https://github.com/user-attachments/assets/b60e2be8-9dfc-45d3-b980-7ba88e395952" />
<img width="1894" height="753" alt="image" src="https://github.com/user-attachments/assets/99cbe366-e3e0-4ded-bd6d-69d68a1e3621" />
<img width="1879" height="665" alt="image" src="https://github.com/user-attachments/assets/06fe3a3c-85a5-4a3b-8ef1-812af5c133f6" />
<img width="1522" height="628" alt="image" src="https://github.com/user-attachments/assets/c8749fef-e9e4-437a-9d71-f9ecebb86e4d" />




---

## 5. Tools Used

- **Header Analysis:** Thunderbird / Outlook / M365 Message Trace  
- **IOC Extraction:** `EIOC.py` (or `emldump` / `emlAnalyzer`)  
- **URL Analysis:** [urlscan.io](https://urlscan.io), [VirusTotal](https://www.virustotal.com)  
- **WHOIS / DNS:** `whois`, `nslookup`, `dig`  
- **Attachment Analysis:** [Hybrid Analysis](https://www.hybrid-analysis.com), Any.Run sandbox  
- **Traffic Capture (Lab):** Wireshark / tcpdump  

---

## 6. Analysis Notes

**Authentication Results:**
- **SPF:** SoftFail → sender not authorized (`proton.me`)
- **DKIM:** None → no cryptographic signature
- **DMARC:** None → no enforcement record

**Originating IP:** `192.0.2.1` (no reverse DNS, unusual for legitimate mail servers)

**Thematic Lure:** Voicemail notification creates urgency and encourages clicks

**Malicious Artifacts:**
- **Phishing link:** [http://192.168.0.13/index.html](http://192.168.0.13/index.html)
- **Tracking pixel:** [http://192.168.0.13:8000/tracking_pixel.png](http://192.168.0.13:8000/tracking_pixel.png)

<img width="1794" height="863" alt="image" src="https://github.com/user-attachments/assets/4d01e3c7-7f24-47e0-9616-125b4bceaaf9" />

<img width="588" height="779" alt="image" src="https://github.com/user-attachments/assets/8a2fe86f-3808-4a66-96e5-fcf271741c30" />


---

## 7. Verdict

**Result:** 🚨 Malicious (Phishing Attempt)  

- Social engineering (urgency + voicemail lure).  
- Failed authentication mechanisms (SPF, DKIM, DMARC).  
- Malicious embedded link and tracking pixel.  

---

## 8. Containment & Defense Actions

1. **Determine Scope**  
   - Review M365 message trace to check if similar emails were delivered.  
   - Search email security logs for sender/reply-to/subject IOCs.  

2. **Containment**  
   - Quarantine the email in Exchange Admin Center.  
   - Block sender domain (`office365-support.com`) and `proton.me` in mail flow rules.  

3. **Proactive Defense**  
   - Add phishing URLs to URL blocklist (Defender / proxy / firewall).  
   - Educate users: Awareness campaign on voicemail-themed phishing emails.  
   - Monitor for beaconing attempts from `tracking_pixel.png`.  

📸 *Screenshot Placeholder: Quarantined email in Exchange Admin Center*  

---

## 9. Lessons Learned

- Always verify SPF/DKIM/DMARC alignment.  
- Voicemail and missed call phishing themes remain highly effective.  
- Tracking pixels are often overlooked but provide adversaries with reconnaissance.  

---

✅ **Final Status:** Email confirmed as phishing. IOC list shared with SOC detection team.  

---


5. **SOC Report Creation**  
   - Findings documented into a structured SOC report with IOCs and mitigation recommendations.  

---

## 🔹 Indicators of Compromise (IOCs)  
| Indicator                        | Type          | Description                |  
|----------------------------------|--------------|----------------------------|  
| service@office-voicemail.com     | Email Address | Spoofed sender address     |  
| 192.168.0.13                     | IP Address    | Attacker server            |  
| http://192.168.0.13/login        | URL           | Phishing login page        |  
| “Office voicemail notification”  | Subject Line  | Phishing lure              |  

---

## 🔹 Key Skills Demonstrated  
- Phishing email analysis (headers, sender spoofing).  
- Network traffic analysis with **Wireshark**.  
- Credential harvesting simulation (attacker POV).  
- Extracting and validating IOCs.  
- Writing a professional SOC Investigation Report.  

---

## 🔹 Project Outcome  
This project highlights my ability to:  
- Understand phishing attack vectors.  
- Capture and analyze artifacts using Wireshark.  
- Investigate phishing emails as a SOC Analyst.  
- Document findings in a clear SOC report.  

It demonstrates **entry-level SOC Analyst skills** and readiness to investigate real-world phishing attacks.  

---

## 📸 Screenshots Included  
- Phishing email in victim inbox.  
- Email header analysis (Sublime + tools).  
- Python server with credential harvesting logs.  
- Fake voicemail/login phishing page.  
- Wireshark captures (DNS + HTTP traffic).  
- Extracted IOC list and SOC report summary.  

---

## 🔹 How to Use This Project  
- Clone this repo to review my artifacts and documentation.  
- Screenshots and SOC report are provided in `/screenshots` and `/report` folders.  
- This lab is for **educational and demonstration purposes only**.  

---



#  Phishing Email Analysis & Investigation Project  

## 🔹 Overview

This project simulates a **real-world phishing campaign** and documents the **SOC analyst investigation process** from email delivery to artifact collection and reporting.  
The phishing email was crafted to appear as a **voicemail notification from Office**, leading victims to a fake login page where credentials could be harvested.  

The project demonstrates both perspectives:  
- **Attacker:** Hosting a phishing page and logging credentials  
- **Defender:** Analyzing the phishing email, capturing traffic with Wireshark, and extracting IOCs



---

## 🔹 Skills & Tasks Demonstrated  
The lab covers a wide range of **Phishing Email Investigation and Analysis tasks**, including:

<p float="left">  
<code>Email Header Review</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Malicious Link Analysis</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>IOC Extraction & Threat Hunting</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>SOC Investigation Reporting</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Defensive Security Mindset</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Email Analysis Tool Proficiency</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Wireshark Packet Capture</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Attack Simulation (Python Server)</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Artifact Documentation</code>  
</p>


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


<img width="1875" height="617" alt="image" src="https://github.com/user-attachments/assets/af3051c1-0daf-4075-ba05-a9bb89fe8062" />
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
  <img width="968" height="412" alt="image" src="https://github.com/user-attachments/assets/d87a5c56-5ea8-46d5-b9a8-7edd72eb459c" />




### Email Addresses
- **Sender:** voicemail@office365-support.com (spoofed)  
- **Reply-To:** cyberlocal@proton.me  

## Attachments
| Attachment Name | MD5 | SHA1 | SHA256 |
|-----------------|-----|------|--------|
| Voicemail_Transcription.txt | 528d1ddc8a80d55e607eb6d15c4dbee2 | a6abcaff0eb79f491d7d8b8dbd9a376198261764 | b636c9cef547b1a18ce1dd2f998d2bee865a96f0e04958b4265ff75d7bfb764d


---
- `Voicemail_Transcription.txt` (Analyze with **Virustotal** and **phishtool**).  

<img width="1939" height="511" alt="image" src="https://github.com/user-attachments/assets/a0a5c6b4-9be3-49dd-8116-2ea365ecbe85" />
<img width="1365" height="534" alt="image" src="https://github.com/user-attachments/assets/e5f43a3a-1559-4ce0-bc7d-8be0917c12c6" />

--

## 5. Network Traffic Analysis (Wireshark)

- Wireshark on SOC workstation, filtered with: **ip.addr == 192.168.0.12 && ip.addr == 192.168.0.13** **http.request.method==POST** **http.request.uri contains "tracking_pixel"**  To **Observed victim → attacker traffic when the phishing link was clicked.**

- Captured **HTTP GET request** to `/index.html` (phishing page).  
- Captured **HTTP POST request** with submitted credentials.  
- Identified **tracking pixel request** to `/tracking_pixel.png`, confirming beaconing.  
<img width="1924" height="581" alt="image" src="https://github.com/user-attachments/assets/b60e2be8-9dfc-45d3-b980-7ba88e395952" />
<img width="1894" height="753" alt="image" src="https://github.com/user-attachments/assets/99cbe366-e3e0-4ded-bd6d-69d68a1e3621" />
<img width="1879" height="665" alt="image" src="https://github.com/user-attachments/assets/06fe3a3c-85a5-4a3b-8ef1-812af5c133f6" />
<img width="1522" height="628" alt="image" src="https://github.com/user-attachments/assets/c8749fef-e9e4-437a-9d71-f9ecebb86e4d" />




---

## 6. Tools Used

- **Header Analysis:** Thunderbird / Outlook / [Mailtower](https://mailheader.mailtower.app/#/),
- **IOC Extraction:** `EIOC.py` / [PhishToolAnalysis](https://app.phishtool.com)
- **URL Analysis:** [urlscan.io](https://urlscan.io), [VirusTotal](https://www.virustotal.com)  
- **WHOIS / DNS:** `whois`, `nslookup`, `dig`  
- **Attachment Analysis:** [PhishToolAnalysis](https://app.phishtool.com), Any.Run sandbox  
- **Traffic Capture (Lab):** Wireshark 

---

## 7.  Analysis Notes

**Authentication Results:**
- **SPF:** SoftFail → sender not authorized (`proton.me`)
- **DKIM:** None → no cryptographic signature
- **DMARC:** None → no enforcement record

**Originating IP:** `192.0.2.1` (no reverse DNS, unusual for legitimate mail servers)

**Thematic Lure:** Voicemail notification creates urgency and encourages clicks

**Malicious Artifacts:**
- **Phishing link:** [http://192.168.0.13/index.html](http://192.168.0.13/index.html)
- **Tracking pixel:** [http://192.168.0.13:8000/tracking_pixel.png](http://192.168.0.13:8000/tracking_pixel.png)

<img width="1858" height="859" alt="image" src="https://github.com/user-attachments/assets/a9fab7ed-523b-4908-b9b4-5d16b8891f23" />
<img width="588" height="779" alt="image" src="https://github.com/user-attachments/assets/8a2fe86f-3808-4a66-96e5-fcf271741c30" />


---

## 8.  Verdict

**Result:** 🚨 Malicious (Phishing Attempt)  

- Social engineering (urgency + voicemail lure).  
- Failed authentication mechanisms (SPF, DKIM, DMARC).  
- Malicious link and tracking pixel detected.  

---

## 9.  Containment & Defense Actions

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

##  Key Artifacts / IOCs

**URLs:**
- [http://192.168.0.13/index.html](http://192.168.0.13/index.html) → phishing page
- [http://192.168.0.13:8000/tracking_pixel.png](http://192.168.0.13:8000/tracking_pixel.png) → tracking beacon

**Email Addresses:**
- **Sender:** `voicemail@office365-support.com` (spoofed)
- **Reply-To:** `cyberlocal@proton.me`

**Attachments:**
- `Voicemail_Transcription.txt` → analyzed for malicious content

**IPs:**
- **X-Originating-IP:** `192.0.2.1`


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
- Understand phishing attack vectors  
- Capture and analyze artifacts using Wireshark  
- Investigate phishing emails as a SOC Analyst  
- Document findings in a clear SOC report  
- Verify SPF/DKIM/DMARC alignment  
- Recognize voicemail and missed call phishing themes as highly effective  
- Identify tracking pixels that provide adversaries with reconnaissance

---

✅ **Final Status:** Email confirmed as phishing. IOC list shared with SOC detection team.  

> **Note:** This project is Part One. All samples used were **created by me for safe testing purposes**.  
> Now that I am familiar with phishing analysis, I plan to download real-world samples from **PhishingPot on GitHub** to further improve my knowledge and skills.
 

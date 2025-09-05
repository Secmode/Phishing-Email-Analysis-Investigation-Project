
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

## 🔹 Attack & Investigation Workflow : Still working on the rest of the project: Thanks for viewing   

---
## 🔹 Attack Preparations Workflow  
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

    ## 🔹 Investigation Workflow (with Wireshark)
1. `SOC analyst / incident responder` → **Collect the Phishing Email** → **Header Analysis**  → **Body & Link Analysis**  → **Indicator of Compromise (IOC) Extraction**  → **Packet Capture**  → **Open-Source Intel (Safe Investigation)**



       

       


      





=============================================================================================================
1. **Setup Phishing Web Server Server.py and ** **Create Phishing Email** **Build the Phish login.html

## 🔹 Attack & Investigation Workflow  
1. **Phishing Email Sent**  
   - Spoofed sender with subject: *“You have a new voicemail”*.  
   - Embedded link leading to phishing login page.  

2. **Victim Interaction**  
   - Victim clicks link and is redirected to fake login page.  
   - Credentials submitted are harvested by attacker server.  

3. **Packet Capture with Wireshark**  
   - Captured traffic includes:  
     - SMTP email delivery.  
     - DNS requests for phishing domain.  
     - HTTP POST requests containing credentials.  

4. **Artifact Collection & Analysis**  
   - Extracted IOCs: sender domain, IPs, URLs, email headers.  
   - Analyzed with REMnux and open-source tools.  

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


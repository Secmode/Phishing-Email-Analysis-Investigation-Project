
#  Phishing Email Analysis & Investigation Project  

## 🔹 Overview  
This project simulates a **real-world phishing campaign** and documents the **SOC analyst investigation process** from email delivery to artifact collection and reporting. The phishing email was crafted to appear as a **voicemail notification from Office**, leading victims to a fake login page where credentials could be harvested.  

The project demonstrates both the **attacker’s perspective** (hosting a phishing page, logging credentials) and the **defender’s perspective** (analyzing the phishing email, capturing traffic with Wireshark, and extracting IOCs).  

---

## 🔹 Skills & Tasks Demonstrated  
The lab covers a wide range of **Phishing Email Investigation and Analysis tasks**, including:

<p float="left">  
<code>Email Header Review</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Threat Analysis</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Spoofing Detection</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Malicious Link Analysis</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Networking & Traffic Analysis</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Credential Harvesting Awareness</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Incident Response Workflows</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>IOC Extraction & Threat Hunting</code> &nbsp;&nbsp; | &nbsp;&nbsp;  <code>SOC Investigation Reporting</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Defensive Security Mindset</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Email Analysis Tool Proficiency</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Wireshark Packet Capture</code> &nbsp;&nbsp; | &nbsp;&nbsp;  <code>Attack Simulation (Python Server)</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Credential Harvest Logging</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Open-Source Intelligence (OSINT)</code> &nbsp;&nbsp; | &nbsp;&nbsp; <code>Artifact Documentation</code>  </p>

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

---
<img width="975" height="741" alt="image" src="https://github.com/user-attachments/assets/60c3e252-f997-4daa-a283-9e30877b9f9c" />


---

## 🔹 Attack & Investigation Workflow : Still working on the rest of the project: Thanks for viewing   



---

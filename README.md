# -Windows-Log-Forwarding-to-Splunk-via-Splunk-Universal-Forwarder
Author: Shaikh Salman 
Role: SOC Analyst Trainee | Cybersecurity Enthusiast

📌 Project Overview
This project outlines the process of forwarding Windows Security Event Logs using Splunk Universal Forwarder (UF) to a centralized Splunk Enterprise Server, enabling real-time threat detection and log analysis.

Developed as part of a hands-on SOC Analyst training task, the project emphasizes building a reliable pipeline to capture and monitor critical security events such as logon attempts, login failures, and privilege escalations (EventCodes 4624, 4625, 4672, etc.).

🚀 Key Features
✅ Real-time forwarding of Windows Security logs via Splunk UF
✅ Continuous monitoring of WinEventLog:Security
✅ Detection of successful/failed logins and administrative privilege use
✅ Custom configuration using inputs.conf and outputs.conf
✅ Verified setup through real-time Splunk search queries
✅ SEO-friendly formatting for visibility and learning exposure

🧰 Tools & Technologies
🟦 Splunk Universal Forwarder (Windows)
🟧 Splunk Enterprise Server (Indexer)
🪟 Windows 10 / 11
🔐 Log Source: WinEventLog:Security
⚙️ Network Port: TCP 9997
📁 Configuration Files: inputs.conf, outputs.conf

📖 Step-by-Step Implementation

1. Install Splunk Universal Forwarder on Windows
→ Download from the official Splunk Downloads page.

2. Configure inputs.conf

ini
Copy
Edit
[WinEventLog://Security]  
disabled = 0  
index = wineventlog  
3. Configure outputs.conf

ini
Copy
Edit
[tcpout]  
defaultGroup = default-autolb-group  

[tcpout:default-autolb-group]  
server = <Your_Indexer_IP>:9997  
4. Enable Receiving on Splunk Enterprise Server
→ Go to Settings > Forwarding and Receiving > Configure Receiving
→ Enable listening on Port 9997

5. Restart the Splunk Universal Forwarder

bash
Copy
Edit
splunk restart  
✅ Validation Search Query in Splunk

spl
Copy
Edit
host="DESKTOP-IRBHD8G" sourcetype="WinEventLog:Security"
📊 Results
Successfully indexed 20,000+ Windows Security Events, including:

🔓 EventCode 4624 – Successful Logon

❌ EventCode 4625 – Failed Logon Attempt

⚠️ EventCode 4672 – Privileged Account Logon

✍️ Author : Shaikh Salman 
384shaikhsalman@gmail.com
Cybersecurity Enthusiast & SOC Analyst Trainee

🧠 #Tags
splunk universal forwarder, windows event logs, eventcode 4624, soc analyst project, log forwarding, inputs.conf, outputs.conf, tcp port 9997, splunk enterprise, siem project, real-time log collection, log monitoring, security log forwarder, windows splunk configuration, cybersecurity internship project, splunk data ingestion

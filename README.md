# -Windows-Log-Forwarding-to-Splunk-via-Splunk-Universal-Forwarder
Author: Shaikh Salman 
Role: SOC Analyst Trainee | Cybersecurity Enthusiast

A step-by-step implementation to forward **Windows Security Logs** (e.g., logon attempts, privilege escalations) to a **centralized Splunk Enterprise server** using the **Splunk Universal Forwarder (UF)** — simulating a core SOC (Security Operations Center) workflow.

---

## 📌 Table of Contents

- [📌 Table of Contents](#-table-of-contents)
- [🎯 Objective](#-objective)
- [🧰 Tools & Technologies](#-tools--technologies)
- [🖥️ Architecture](#-architecture)
- [⚙️ Step-by-Step Configuration](#-step-by-step-configuration)
- [✅ Log Forwarding Validation](#-log-forwarding-validation)
- [📁 Project Structure](#-project-structure)
- [📚 References](#-references)
- [📸 Screenshots](#-screenshots)
- [📜 License](#-license)
- [🙋‍♂️ Connect](#-connect)

---

## 🎯 Objective

To configure a Windows client to collect and forward **Security Event Logs** to a **Splunk Enterprise** server in real-time for centralized monitoring, alerting, and threat analysis.

---

## 🧰 Tools & Technologies

| Tool                     | Purpose                                  |
|--------------------------|------------------------------------------|
| Windows 10/11            | Log-generating client machine            |
| Splunk Universal Forwarder | Log collector & forwarder              |
| Splunk Enterprise        | Central server for indexing & monitoring|
| TCP Port 9997            | Default Splunk forwarding port           |
| `inputs.conf`, `outputs.conf` | UF configuration files               |

---

## 🖥️ Architecture

```text
+----------------------------+          TCP:9997          +----------------------------+
|  Windows Client (UF)      |--------------------------->|   Splunk Enterprise Server |
|  Event Log Generator      |                            |   Receiver / Indexer       |
+----------------------------+                            +----------------------------+
⚙️ Step-by-Step Configuration
1️⃣ Install Splunk Universal Forwarder on Windows Client
Download from: https://www.splunk.com/en_us/download/universal-forwarder.html

Install as Local System User

2️⃣ Allow Outbound Port in Windows Firewall
Open Windows Defender Firewall

Go to Outbound Rules

Enable outbound rule for splunkd.exe on TCP Port 9997

3️⃣ Configure inputs.conf
📄 Path:
C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf

ini
Copy
Edit
[WinEventLog://Security]
disabled = 0
index = win_security

[WinEventLog://System]
disabled = 0
index = win_system

[WinEventLog://Application]
disabled = 0
index = win_app
4️⃣ Configure outputs.conf
📄 Path:
C:\Program Files\SplunkUniversalForwarder\etc\system\local\outputs.conf

ini
Copy
Edit
[tcpout]
defaultGroup = default-autolb-group

[tcpout:default-autolb-group]
server = <YOUR_SPLUNK_IP>:9997

[tcpout-server://<YOUR_SPLUNK_IP>:9997]
5️⃣ Enable Receiving on Splunk Enterprise
Go to Settings > Forwarding and receiving > Configure receiving

Click Add new

Add Port 9997

6️⃣ Restart Splunk Universal Forwarder
powershell
Copy
Edit
& "C:\Program Files\SplunkUniversalForwarder\bin\splunk.exe" restart
✅ Log Forwarding Validation
🔐 Simulate Security Events
Perform user login actions to generate:

4624: Successful Logon

4672: Privileged Account Logon

🔍 Search Query in Splunk Web
spl
Copy
Edit
index=* sourcetype="WinEventLog:*" host="<CLIENT-HOSTNAME>"
✔️ Expected Results:

Logs from Security, System, Application

EventCodes like 4624, 4672

Real-time updates on Splunk timeline

📁 Project Structure
arduino
Copy
Edit
.
├── config/
│   ├── inputs.conf
│   └── outputs.conf
├── screenshots/
│   ├── splunk_search_ui.png
│   └── firewall_rule.png
├── README.md
📚 References
Splunk Universal Forwarder Documentation

Windows Event ID Documentation

Splunk Enterprise Documentation

📸 Screenshots
Add these to a screenshots/ folder in your repo:

✅ Splunk Web UI showing logs

✅ Sample query output

✅ Firewall rule config

✅ UF inputs.conf and outputs.conf setup

📜 License
This project is licensed under the MIT License.

🙋‍♂️ Connect
Platform	Link
✍️ Author : Shaikh Salman 
📧 Email	: 384shaikhsalman@gmail.com
💼 LinkedIn	linkedin.com/in/shaikh-salman-60524b324
💻 GitHub	github.com//384ShaikhSalman

⭐ Star this repository if you found it useful — it helps others discover the project!

🧠 #Tags
splunk universal forwarder, windows event logs, eventcode 4624, soc analyst project, log forwarding, inputs.conf, outputs.conf, tcp port 9997, splunk enterprise, siem project, real-time log collection, log monitoring, security log forwarder, windows splunk configuration, cybersecurity internship project, splunk data ingestion

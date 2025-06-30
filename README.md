# -Windows-Log-Forwarding-to-Splunk-via-Splunk-Universal-Forwarder
This guide explains how to install and configure the Splunk Universal Forwarder on a Windows system to forward logs (Event Logs, Security Logs, Application Logs, etc.) to a Splunk Enterprise or Splunk Cloud instance.
________________________________________
📦 Prerequisites
•	Windows system (Windows 10/11, Server 2016+)
•	Splunk Enterprise or Splunk Cloud receiver ready (indexer IP/hostname and port)
•	Administrator privileges on the Windows machine
•	Splunk Universal Forwarder downloaded: Download Here
________________________________________
⚙️ Step-by-Step Setup
✅ Step 1: Install the Splunk Universal Forwarder
1.	Download the appropriate .msi installer for Windows.
2.	Run the installer as Administrator.
3.	Choose the installation path or keep the default.
4.	Configure:
o	Splunk Admin credentials
o	Forwarding receiver information (indexer IP & receiving port, typically 9997)
o	Select the logs you want to monitor (or skip to configure manually)
________________________________________
📁 Step 2: Add Windows Inputs for Log Forwarding
You can do this either via the GUI during install or by editing the inputs.conf file:
Location:
perl
CopyEdit
C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf
Sample Configuration:
ini
CopyEdit
[default]
host = YOUR-WINDOWS-HOSTNAME

[WinEventLog:Application]
disabled = 0

[WinEventLog:Security]
disabled = 0

[WinEventLog:System]
disabled = 0
________________________________________
🌐 Step 3: Configure Forwarding to Splunk Indexer
Location:
perl
CopyEdit
C:\Program Files\SplunkUniversalForwarder\etc\system\local\outputs.conf
Sample Configuration:
ini
CopyEdit
[tcpout]
defaultGroup = default-autolb-group

[tcpout:default-autolb-group]
server = YOUR-SPLUNK-INDEXER-IP:9997

[tcpout-server://YOUR-SPLUNK-INDEXER-IP:9997]
________________________________________
🔐 Step 4: Enable Splunk to Receive Logs
On your Splunk Indexer, go to:
Settings → Forwarding and receiving → Configure receiving → Add new
•	Enter port 9997
•	Save and restart Splunk if needed
________________________________________
🚀 Step 5: Start the Universal Forwarder
Open PowerShell as Administrator:
powershell
CopyEdit
& "C:\Program Files\SplunkUniversalForwarder\bin\splunk.exe" start
(Optional: set Splunk to start on boot)
powershell
CopyEdit
& "C:\Program Files\SplunkUniversalForwarder\bin\splunk.exe" enable boot-start
________________________________________
📊 Step 6: Verify in Splunk
In the Splunk search bar:
spl
CopyEdit
index=* host="YOUR-WINDOWS-HOSTNAME"
You should start seeing logs from your Windows machine.
________________________________________
📎 Useful References
•	📚 Splunk Docs: Universal Forwarder Manual
•	🔒 Best Practices: Always secure communication with TLS in production environments
•	📂 Logs Location (for troubleshooting):
o	Splunk UF logs: C:\Program Files\SplunkUniversalForwarder\var\log\splunk\
________________________________________
🛡️ Security Note
For production, it is recommended to:
•	Enable SSL on the forwarder and receiver
•	Restrict access via firewall
•	Monitor UF status regularly using Deployment Server or health dashboards
________________________________________

Author : Shaikh Salman Kaleem 
📧 384shaikhsalman@gmail.com
Cybersecurity & SOC Analyst Trainee

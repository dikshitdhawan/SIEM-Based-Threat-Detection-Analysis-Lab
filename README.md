🛡️ SIEM-Based Threat Detection & Analysis Lab 
________________________________________
📌 Overview
This project demonstrates a Security Operations Center (SOC) simulation lab designed to replicate real-world threat detection, monitoring, and incident analysis workflows.

The lab integrates endpoint telemetry, SIEM-based detection, and attack simulation to provide hands-on experience with practical cybersecurity operations.

🎯 Objective: Develop SOC analyst skills including log analysis, alert investigation, and event correlation.
________________________________________
🚨 Key Highlights

•	Analyzed 100000+ security events over a month

•	Successfully detected brute-force attack patterns (Hydra)

•	Identified detection gaps in reconnaissance & execution techniques

•	Demonstrated real-world SIEM limitations and tuning requirements
________________________________________
🏗️ Architecture
## 🔄 Attack & Monitoring Flow

```
Kali Linux (Attacker)
        ↓
Windows 11 (Victim + Sysmon + Wazuh Agent)
        ↓
Wazuh Manager (Amazon Linux 2023)
        ↓
 Wazuh Dashboard
        ↓
SOC Analysis & Visualization
```

<img width="750" height="750" alt="Architecture" src="https://github.com/dikshitdhawan/SIEM-Based-Threat-Detection-Analysis-Lab/blob/3097897423373be9ab8d4007c5549367244fa268/architecture/Architecture.png" />

________________________________________
⚙️ Tech Stack

Layer	Technology

SIEM	Wazuh

Endpoint Monitoring	Sysmon

Target System	Windows 11

Attacker System	Kali Linux

Server OS	Amazon Linux 2023

Virtualization	VMware
________________________________________
🚨 Attack Scenarios

🔐 Brute Force Attack (Hydra)

•	High-frequency authentication attempts

•	Windows Event ID 4625 (Failed Login)

•	Clear alert spikes observed in dashboard

Result:

✔ Successfully detected and visualized

________________________________________
🌐 Reconnaissance (Nmap)

•	Port scanning and service enumeration

•	Sequential probing behavior observed

Result:

⚠ Limited detection in default Wazuh configuration

Insight:

•	Highlights need for custom rule tuning

•	Demonstrates real-world SIEM detection limitations

________________________________________

⚡ Suspicious Execution (PowerShell)

•	Sysmon Event ID 1 (Process Creation)

•	System-level PowerShell execution observed

Result:

⚠ Low detection (5–7 events generated)

Insight:

•	Baseline detection present

•	Requires advanced rule customization for deeper visibility

________________________________________

📊 Dashboard Preview

screenshots/dashboard/alerts-over-time.png

screenshots/dashboard/alerts-by-severity.png

screenshots/dashboard/top-attack-types.png

________________________________________
🔍 Key Findings

•	Generated 100000+ logs during attack simulation over a month

•	Clear alert spike patterns during brute-force activity

•	Dominant alert:

Logon Failure – Unknown user or bad password

•	Detection highlights:

o	Repeated authentication failures

o	PowerShell execution activity

o	Service-level changes (BITS)

________________________________________

⚠️ Detection Limitations

During testing, certain attack techniques were not fully detected:

•	Nmap reconnaissance showed limited visibility

•	PowerShell execution generated minimal alerts

Analysis:

•	Default SIEM rules do not cover all attack vectors

•	Detection accuracy depends on:

o	Rule tuning

o	Log configuration

o	Detection engineering

SOC Insight:

This reflects real-world environments where continuous tuning is required to improve detection coverage.

________________________________________

🧠 Event Correlation

Multiple Failed Logins (Event ID 4625)
        +
High Alert Frequency
        +
Same Source IP
        ↓
Confirmed Brute Force Attack
________________________________________

🧬 MITRE ATT&CK Mapping

Technique	ID

Brute Force	T1110

Command Execution (PowerShell)	T1059

Network Discovery	T1046
________________________________________
## 📂 Project Structure

```
.
├── architecture/
├── setup/
├── attacks/
├── analysis/
├── screenshots/
├── report/
└── README.md
```
____________________
🛠️ Setup (High-Level)
1.	Deploy Wazuh OVA (Amazon Linux)
2.	Configure Wazuh Manager & Dashboard
3.	Install Wazuh Agent on Windows 11
4.	Configure Sysmon for telemetry
5.	Connect agent to Wazuh server
6.	Launch Kali attacker machine
7.	Execute attack simulations
8.	Monitor alerts in dashboard
________________________________________
🧩 Challenges
•	Limited detection for Nmap scans

•	Low PowerShell visibility

•	Sysmon configuration tuning

•	Wazuh dashboard filtering issues

•	VM networking inconsistencies
________________________________________
🚀 Key Learnings

•	SIEM effectiveness depends on log quality and rule configuration

•	Detection engineering is critical in SOC environments

•	Log analysis is more important than tool usage

•	Visualization enables faster threat identification
________________________________________
📄 Full Report

## 📄 Detailed SOC Incident Report

📥 [Download SOC Incident Report](https://github.com/dikshitdhawan/SIEM-Based-Threat-Detection-Analysis-Lab/blob/42f31b089761c9e37fba80a2bcd7aa674bd43af8/report/SOC_Report%201.docx)

________________________________________
🎯 Why This Project Matters

This project demonstrates real SOC analyst capabilities, including:

•	Threat detection using SIEM

•	Log correlation and investigation

•	Identification of detection gaps

•	Understanding of real-world monitoring limitations

Focused on practical cybersecurity skills — not just theoretical setup
________________________________________

📈 Future Improvements

•	Custom Wazuh rule development

•	Integration with Threat Intelligence (OTX / AbuseIPDB)

•	Automated alert response workflows

•	Network-level monitoring using Zeek

________________________________________

⭐ Final Note

This project reflects a practical SOC workflow, including detection, analysis, and identification of limitations.

👉 Built to demonstrate real-world cybersecurity and SOC skills


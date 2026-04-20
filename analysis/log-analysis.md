# 🧠 Log Analysis & Threat Correlation

## 📌 Overview

This section presents the analysis of logs collected in a SOC simulation lab using Wazuh SIEM.
The objective is to identify attack patterns, correlate events, and evaluate detection capability.

The analysis is based on data collected from:

* Windows 11 endpoint (Sysmon + Wazuh Agent)
* Wazuh Manager (Amazon Linux 2023)

---

## 📊 Log Volume & Activity

* Total logs generated: **100,000+ events**
* Observation period: **~1 month**
* Continuous log ingestion observed throughout the period

### 🧠 Insight:

* High log volume demonstrates stable SIEM ingestion pipeline
* Consistent logging reflects proper agent configuration
* Sudden spikes correspond to attack execution windows

---

## ⏱️ Temporal Analysis

* Normal activity shows steady log generation
* Attack periods show **sharp spikes in log volume**
* Brute-force attack windows exhibit the highest activity

### Interpretation:

* Baseline activity → predictable log flow
* Attack activity → anomalous spike pattern

This behavior is essential for identifying suspicious activity in real SOC environments.

---

## 🔐 Authentication Failure Analysis (Brute Force)

### Observations:

* High frequency of failed login attempts
* Event ID: **4625 (Failed Login)**
* Repeated attempts from the same source IP
* Rapid succession of authentication failures

### 🧠 Interpretation:

These indicators confirm a **brute-force attack pattern**, where automated tools attempt multiple credentials in a short period.

### Detection:

* Successfully detected in Wazuh
* Clear alert spikes visible in dashboard
* Dominant alert type:

  > *Logon Failure – Unknown user or bad password*

---

## ⚡ Process & PowerShell Activity

### Observations:

* Sysmon Event ID: **1 (Process Creation)**
* PowerShell execution detected
* Limited number of events (~5–7 hits)

### 🧠 Interpretation:

* Indicates baseline visibility into execution activity
* Low alert volume suggests:

  * Default rule limitations
  * Lack of advanced detection rules

### SOC Insight:

PowerShell is commonly used in:

* Fileless malware
* Post-exploitation
* Privilege escalation

Limited detection highlights the need for **enhanced rule tuning**.

---

## 🌐 Network Activity (Nmap Reconnaissance)

### Observations:

* Minimal or no alerts triggered during scan activity
* No clear detection of port scanning behavior

### 🧠 Interpretation:

* Default Wazuh rules do not fully detect reconnaissance techniques
* Indicates detection gap in SIEM configuration

### SOC Insight:

Reconnaissance is an early-stage attack phase and often requires:

* Custom rules
* Network-based monitoring tools (e.g., Zeek)

---

## 📊 Dashboard Correlation

Observed patterns in Wazuh Dashboard:

* Significant alert spikes during brute-force attack
* Authentication-related alerts dominate
* Clear separation between normal and attack activity

### 🧠 Insight:

Visualization enables quick identification of:

* Attack timelines
* Severity trends
* Alert distribution

---

## 🔗 Event Correlation

```text
Multiple Failed Logins (Event ID 4625)
        +
High Alert Frequency
        +
Same Source IP
        ↓
Confirmed Brute Force Attack
```

---

## 🧬 MITRE ATT&CK Mapping

| Activity             | Technique         | ID    |
| -------------------- | ----------------- | ----- |
| Brute Force          | Credential Access | T1110 |
| PowerShell Execution | Command Execution | T1059 |
| Nmap Scan            | Network Discovery | T1046 |

---

## ⚠️ Detection Limitations

During testing, certain attack techniques were not fully detected:

* Nmap reconnaissance showed limited or no detection
* PowerShell activity generated minimal alerts

### Root Cause:

* Default SIEM rules are not exhaustive
* Detection depends on:

  * Rule tuning
  * Log configuration
  * Detection engineering

### SOC Insight:

This reflects real-world SOC environments, where:

> Detection must be continuously improved through rule tuning and analysis

---

## 🎯 SOC Interpretation

* Brute-force attack successfully detected and analyzed
* No successful system compromise observed
* Detection gaps identified in:

  * Reconnaissance phase
  * Execution techniques

---

## 🧠 Analyst Verdict

The system experienced a simulated brute-force attack characterized by repeated authentication failures and clear spike patterns in log activity.

While detection of credential-based attacks was effective, limited visibility into reconnaissance and execution highlights the importance of **custom detection rules and continuous SIEM tuning**.

---

## 🚀 Key Takeaways

* SIEM effectiveness depends on **configuration and rule tuning**
* Log analysis is critical for threat detection
* Attack patterns can be identified through correlation and visualization
* Detection gaps are normal and must be addressed through continuous improvement

---

## 📸 Reference Logs

> Add your screenshots here:

```md
![Wazuh Logs](../screenshots/logs/wazuh-discover.png)
```

---


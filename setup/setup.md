# ⚙️ SOC Lab Setup Guide

## 📌 Overview

This document describes the setup of a **SOC simulation lab environment** using:

* Wazuh SIEM (Amazon Linux 2023)
* Windows 11 endpoint (Wazuh Agent + Sysmon)
* Kali Linux attacker machine

The objective is to create a working pipeline for:

* Log collection
* Threat detection
* Security monitoring

> 🎯 Focus: Practical SOC workflow — not just lab setup

---

## 🏗️ Lab Architecture

```
Kali Linux (Attacker)
        ↓
Windows 11 (Sysmon + Wazuh Agent)
        ↓
Wazuh Manager (Amazon Linux 2023)
        ↓
Wazuh Dashboard (SIEM)
```

---

## 🖥️ Environment Setup

| Machine      | Role            | OS                |
| ------------ | --------------- | ----------------- |
| Wazuh Server | SIEM            | Amazon Linux 2023 |
| Windows 11   | Victim Endpoint | Windows 11        |
| Kali Linux   | Attacker        | Kali Linux        |

---

## 🌐 Network Configuration

* All machines connected using **NAT network**
* Ensure connectivity:

```bash
ping <target-ip>
```

---

## ⚙️ Step 1: Wazuh Server Setup

### 1. Import Wazuh OVA

* Import into VMware
* Start the virtual machine

---

### 2. Access Dashboard

```
https://<WAZUH_SERVER_IP>
```

---

### 3. Verify Services

Ensure the following are running:

* Wazuh Manager
* Indexer
* Dashboard

---

## 🖥️ Step 2: Windows Agent Setup

### 1. Install Wazuh Agent

* Download agent from Wazuh dashboard
* Install on Windows 11 machine

---

### 2. Configure Agent

Edit:

```
C:\Program Files (x86)\ossec-agent\ossec.conf
```

Update server address:

```xml
<address><WAZUH_SERVER_IP></address>
```

---

### 3. 🔐 Agent Authentication (IMPORTANT)

```powershell
"C:\Program Files (x86)\ossec-agent\agent-auth.exe" -m <WAZUH_SERVER_IP>
```

> ⚠️ Without this step, the agent may not register in many setups

---

### 4. Start Agent

```powershell
net start wazuh-agent
```

---

## 🔍 Step 3: Sysmon Configuration

### 1. Download Sysmon

Download Sysmon from Microsoft official source.

---

### 2. Download Configuration

Use recommended configuration:

```
https://github.com/SwiftOnSecurity/sysmon-config
```

---

### 3. Install Sysmon

```powershell
Sysmon64.exe -i sysmonconfig.xml
```

---

### 4. Purpose

Sysmon provides:

* Process creation logs
* Network activity
* File & registry monitoring

---

## 🐉 Step 4: Kali Linux Setup

* Ensure Kali is on same network
* Verify connectivity to Windows machine

### Tools Used:

* Hydra
* Nmap

---

## 🧠 Step 5: Detection-Oriented Setup

A SOC lab should not only generate logs — it should **detect threats**.

---

### 🎯 Detection Goals

* Detect brute-force login attempts
* Detect suspicious PowerShell usage
* Detect abnormal process execution
* Monitor service-level changes

---

### 🔍 What to Verify

After setup:

* Logs visible in Wazuh **Discover**
* Key Event IDs:

  * 4625 → Failed login attempts
  * Sysmon Event ID 1 → Process creation

---

### 📊 Detection Check

Ensure:

* Alerts are generated
* Dashboards show activity
* Logs correlate with simulated attacks

---

## ⚠️ Common Issues & Fixes

### ❌ Agent not connecting

* Run `agent-auth.exe`
* Verify correct server IP

---

### ❌ No logs in dashboard

* Check Sysmon installation
* Restart Wazuh agent

---

### ❌ Detection missing

* Default rules may not detect all attacks
* Requires rule tuning

---

## ✅ Final Validation Checklist

* [ ] Wazuh dashboard accessible
* [ ] Agent connected and authenticated
* [ ] Sysmon logs visible
* [ ] Kali can reach Windows
* [ ] Alerts generated in dashboard

---

## 🎯 Outcome

After completing setup:

* Logs are successfully collected
* Endpoint visibility is established
* Detection pipeline is functional

---

## 🧠 Final Note

This lab demonstrates a key SOC principle:

> Detection is not automatic — it requires tuning, analysis, and understanding of logs.

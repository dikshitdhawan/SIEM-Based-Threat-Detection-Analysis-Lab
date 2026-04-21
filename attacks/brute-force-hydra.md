# 🔐 Brute Force Attack Analysis (Hydra)

## 📌 Objective

The purpose of this test was to simulate a **credential brute-force attack** against the Windows endpoint and evaluate how effectively the SIEM detects repeated authentication failures.

---

## ⚙️ Attack Setup

* **Attacker Machine:** Kali Linux
* **Target System:** Windows 11 (Wazuh Agent + Sysmon)
* **Protocol Used:** SSH / RDP (depending on configuration)
* **Tool:** Hydra

### Command Used

```bash
hydra -l administrator -P passwords.txt <target-ip> ssh
```

> A wordlist-based attack was executed to simulate repeated login attempts against the target system.

---

## 🧪 Attack Behavior

During execution:

* Continuous login attempts were made in rapid succession
* Requests were automated and high-frequency
* Same source system was used throughout

From a behavioral standpoint, this is clearly distinguishable from normal user activity.

---

## 🔍 Observed Logs
![Brute Force Detection](../screenshots/dashboard/SSH%20brute%20force.png)

### Key Indicators

* **Event ID:** 4625 (Failed Login)
* Repeated authentication failures
* High volume of events within short time intervals

### SIEM Observation

* Noticeable spike in alerts during attack window
* Authentication-related alerts dominated the dashboard
* Same source IP associated with repeated failures

---

## 📊 Detection Summary

| Parameter        | Observation             |
| ---------------- | ----------------------- |
| Detection Status | ✔ Successfully detected |
| Alert Volume     | High                    |
| Log Consistency  | Strong                  |
| Visibility       | Clear                   |

The attack was clearly visible in both **raw logs** and **dashboard visualizations**.

---

## 🧠 Analysis

The pattern of repeated failed logins, combined with high-frequency requests, confirms automated brute-force behavior.

Key indicators include:

* Multiple failed attempts from the same source
* Rapid execution with minimal delay
* No successful authentication observed

This type of activity is typically associated with password-guessing attacks rather than legitimate usage.

---

## 🔗 Event Correlation

```text id="corr1"
Multiple Failed Logins (Event ID 4625)
        +
High Frequency Attempts
        +
Same Source IP
        ↓
Confirmed Brute Force Attack
```

---

## 🎯 SOC Interpretation

From an analyst perspective:

* The attack was **clearly identifiable**
* The system successfully generated relevant alerts
* No evidence of account compromise was observed

This indicates that the detection pipeline is functioning correctly for authentication-based threats.

---

## ⚠️ Notes

* Detection relies heavily on authentication logs
* No advanced evasion techniques were used in this simulation
* Real-world attackers may attempt slower or distributed attacks

---

## 🧾 Conclusion

The brute-force attack simulation was successfully detected using Wazuh SIEM.

The combination of:

* Authentication failure logs
* Alert spikes
* Consistent source behavior

allowed for straightforward identification of the attack.

This scenario validates the effectiveness of the SIEM in detecting **credential-based attacks**, while also emphasizing the importance of continuous monitoring and alert analysis.

---


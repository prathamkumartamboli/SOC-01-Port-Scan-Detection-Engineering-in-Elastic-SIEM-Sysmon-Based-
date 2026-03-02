# 🛡 SOC-01: Port Scan Detection in Elastic SIEM (Sysmon-Based)

![Elastic](https://img.shields.io/badge/Elastic-SIEM-blue)
![Sysmon](https://img.shields.io/badge/Sysmon-EventID3-green)
![Detection
Engineering](https://img.shields.io/badge/Detection-Engineering-red)
![MITRE ATT&CK](https://img.shields.io/badge/MITRE-T1046-orange)

------------------------------------------------------------------------

## 📌 Project Overview

This project demonstrates the design, implementation, and validation of
a behavioral detection rule for identifying port scanning activity using
**Elastic Security** and **Sysmon Event ID 3 logs**.

The objective was to simulate reconnaissance activity in a controlled
lab environment and engineer a production-style detection rule capable
of identifying abnormal network behavior.

This repository includes:

-   Attack simulation using Nmap\
-   Log analysis using Sysmon\
-   Threshold-based detection rule creation\
-   Alert validation and timeline investigation\
-   Industry-style SOC incident report\
-   Defensive recommendations

------------------------------------------------------------------------

## 🏗 Lab Architecture

**Attacker:** Kali Linux\
**Target + SIEM Host:** Windows 11\
**SIEM Platform:** Elastic Stack (Main System deployment)\
**Log Forwarder:** Winlogbeat\
**Log Source:** Sysmon Event ID 3 (Network Connection)

### 🔄 Network Flow

    Kali Linux (Attacker)
            ↓
    Port Scanning (Nmap)
            ↓
    Windows 11 (Victim + Elastic Host)
            ↓
    Sysmon Event ID 3 Logs
            ↓
    Winlogbeat
            ↓
    Elasticsearch
            ↓
    Elastic Security Detection Rule

------------------------------------------------------------------------

## 🎯 Detection Objective

Detect abnormal port scanning behavior defined as:

-   Multiple network connection attempts\
-   Same source IP\
-   Rapid change in destination ports\
-   Threshold exceeded within defined time window

Detection is based on behavioral correlation, not static signatures.

------------------------------------------------------------------------

## 🔎 Detection Logic

**Log Source:** Sysmon Event ID 3

### KQL Query

event.code: 3

### Rule Configuration

-   Rule Type: Threshold Rule\
-   Group By: source.ip\
-   Threshold: ≥ 10 events\
-   Time Window: 1 minute\
-   Severity: Medium\
-   Risk Score: 50

### MITRE ATT&CK Mapping

-   Tactic: Reconnaissance\
-   Technique: T1046 -- Network Service Discovery

------------------------------------------------------------------------

## 🧪 Attack Simulation

The following Nmap scans were executed from Kali:

-   TCP SYN Scan (-sS)\
-   TCP Connect Scan (-sT)\
-   Service Version Detection (-sV)

These scans generated multiple network connection events across various
destination ports.

------------------------------------------------------------------------

## 🚨 Alert Investigation

After rule activation:

-   Alert triggered successfully\
-   Source IP identified\
-   Multiple destination ports confirmed\
-   Timeline analysis validated reconnaissance behavior

No exploitation or privilege escalation activity was observed.

------------------------------------------------------------------------

## 🕒 Incident Timeline

  Time       Event
  ---------- -------------------------------------
  12:17:45   First connection attempt observed
  12:18:17   Multiple port connections initiated
  12:25:01   Detection threshold met
  12:25:26   Alert generated in Elastic

Total Duration: \~7 minutes 41 seconds\
Threat Stage: Reconnaissance\
Severity: Medium

------------------------------------------------------------------------


## 🛠 Skills Demonstrated

-   Detection Engineering\
-   KQL Query Development\
-   Sysmon Log Analysis\
-   Behavioral Threat Detection\
-   MITRE ATT&CK Mapping\
-   SOC Alert Investigation Workflow\
-   Incident Documentation Standards

------------------------------------------------------------------------

## 🔐 Defensive Recommendations

-   Restrict unnecessary open ports\
-   Implement firewall hardening\
-   Monitor abnormal connection bursts\
-   Correlate reconnaissance with authentication activity\
-   Consider IDS/IPS integration

------------------------------------------------------------------------

## 📚 Learning Outcomes

This project reinforced:

-   Importance of proper log validation\
-   Behavioral detection over signature-based detection\
-   Threshold tuning considerations\
-   Structured SOC investigation methodology\
-   Professional incident reporting standards

------------------------------------------------------------------------

## 👤 Author

Pratham Tamboli\
SOC & Detection Engineering Enthusiast

------------------------------------------------------------------------

## 📌 Disclaimer

This project was conducted in a controlled lab environment for
educational and defensive cybersecurity research purposes only.

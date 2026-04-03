# 🛡️ SSH Brute-Force Detection Lab (Splunk)

## 📌 Overview

This project simulates an SSH brute-force attack and demonstrates detection using Splunk SIEM.

---

## 🧱 Lab Setup

* Attacker: Kali Linux
* Target: Ubuntu
* SIEM: Splunk
* Network: Host-only adapter

---

## ⚔️ Attack Simulation

### Nmap Scan

```
nmap 192.168.56.101
```

### Brute Force Attack

```
hydra -l vboxuser -P passwords.txt ssh://192.168.56.101
```

---

## 📊 Log Analysis

Logs monitored:

```
/var/log/auth.log
```

Example:

```
Failed password for vboxuser from 192.168.56.102
```

---

## 🔍 Detection in Splunk

```
"Failed password"
| rex "from (?<src>\d+\.\d+\.\d+\.\d+)"
| stats count by src
| where count > 5
```

---

## 🚨 Findings

* Attacker IP: 192.168.56.102
* Failed attempts: 49
* Successful login observed

---

## 🧠 Key Takeaways

* Brute-force attacks create detectable patterns
* SIEM enables centralized visibility
* Log analysis is essential for threat detection

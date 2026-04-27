# 🛡️ Web Server Compromise (JetBrains CVE)

## 🎯 Objective
Identify the attacker and analyze malicious activity on a compromised web server.

---

## 🧪 Environment
- OS: Linux
- Logs: HTTP
- Tools: Wireshark

---

## 🔍 Analysis

### 1. Initial Observation
- Suspicious IP: 23.158.56.196
- Brute force attempt detected on admin login

### 2. Exploitation
- Server running vulnerable JetBrains version
- Exploited CVE-2024-27199
- Code injection without authentication

### 3. Post-Exploitation
- Reverse shell deployed
- Malicious plugin created
- Credentials added for persistence

---

## ⚠️ Indicators of Compromise (IOC)
- IP: 23.158.56.196
- Malicious file: NSt8bHTg.zip
- Suspicious user accounts

---

## 🧠 Conclusion
Attacker exploited a critical vulnerability to gain remote access, establish persistence, and manipulate server data.

---

## 🛠️ Recommendations
- Patch the vulnerability
- Block attacker IP
- Monitor server logs

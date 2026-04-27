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

## 🧠 MITRE ATT&CK Mapping
- TA0001 : Initial Access
- TA0002 : Execution
- TA0011 : Command and Control
- T1110 : Brute Force
- T1565.001 : Stored Data Manipulation

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

## 📸 Evidence (Screenshots / Queries)
Credentials created by the attacker (c91oyemw:CL5vzdwLuK)
<img width="1281" height="835" alt="image" src="https://github.com/user-attachments/assets/044f22e6-9758-474b-8778-ad186de37508" />

Zip uploaded for the reverse shell (NSt8bHTg.zip)
<img width="1261" height="375" alt="image" src="https://github.com/user-attachments/assets/5687a10f-fbd5-4547-8e0e-472ea049dadf" />

Creation of the infected plugin
<img width="1290" height="47" alt="image" src="https://github.com/user-attachments/assets/46a10cfc-892d-47ed-a41b-05005ce968bc" />

Credentials added in the file Creds.txt (a1l4m:youarecompromised)
<img width="1357" height="541" alt="image" src="https://github.com/user-attachments/assets/026fa685-170c-416e-94f3-0165270a9016" />

The attacker tries to evade from the docker (docker run --rm -it -v /:/host ubuntu chroot /host)
<img width="1456" height="512" alt="image" src="https://github.com/user-attachments/assets/dc4b845b-9c54-490b-ba33-18ad60202f67" />






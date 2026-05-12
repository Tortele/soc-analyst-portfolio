# 🛡️ REvil Ransomware Investigation (GOLD SOUTHFIELD)

## 🎯 Objective
Investigate a ransomware infection and collect indicators of compromise (IOC) from an infected Windows machine.

---

## 🧪 Environment
- Platform: Windows
- Log Sources: Splunk / ELK
- Ransom Note: `5uizv5660t-readme.txt`
- Tools Used:
  - Splunk
  - VirusTotal
  - Triage
  - CyberChef

---

## 🔍 Analysis

### 1. Initial Observation
A ransom note named: **5uizv5660t-readme.txt** was discovered on the desktop of the Administrator user.

---

### 2. Investigation

- The ransom note was created by the executable:
  - **facebook assistant.exe**

- Process Information:
PID: **5348**
Path: **C:\Users\Administrator\Downloads\facebook assistant.exe**

- The ransomware opened a terminal session during execution.
Using Splunk, the following SHA256 hash was extracted:
  - **B8D7FB4488C0556385498271AB9FFFDF0EB38BB2A330265D9852E3A6288092AA**

 - VirusTotal analysis revealed:
    - **obfuscation techniques**
    - **suspicious PowerShell activity**
    - **ransomware behavior associated with backup destruction**

### 3. Post-Exploitation

- A suspicious Base64-encoded PowerShell command was identified:
    - **powershell -e RwBlAHQALQBXAG0AaQBPAGIAagBlAGMAdAAgAFcAaQBuADMAMgBfAFMAaABhAGQAbwB3AGMAbwBwAHkAIAB8ACAARgBvAHIARQBhAGMAaAAtAE8AYgBqAGUAYwB0ACAAewAk**

After decoding with CyberChef, the original command was recovered:
    - **Get-WmiObject Win32_Shadowcopy | ForEach-Object {$_.Delete();}**

This command deletes Windows Shadow Copies to prevent backup recovery.

- Using Triage, the ransomware note revealed the following onion domain:
    - **aplebzu47wgazapdqks6vrcv6zcnjppkbxbr6wketf56nf6aq2nmyoyd.onion**

This domain was used for ransom payment and victim communication.

---

## 🧠 MITRE ATT&CK Mapping

- **TA0002** – Execution
- **TA0003** – Persistence
- **TA0004** – Privilege Escalation
- **TA0005** – Defense Evasion
- **TA0007** – Discovery

- **T1059.001** – PowerShell
- **T1027** – Obfuscated Files or Information
- **T1055** – Process Injection

---

## ⚠️ Indicators of Compromise (IOC)

- Ransom note:`5uizv5660t-readme.txt`
- Original File:`facebook assistant.exe`
- Ransomware SHA256:`B8D7FB4488C0556385498271AB9FFFDF0EB38BB2A330265D9852E3A6288092AA`
- Onion Domain:`aplebzu47wgazapdqks6vrcv6zcnjppkbxbr6wketf56nf6aq2nmyoyd.onion`

---

## 🧠 Conclusion

The user Administrator downloaded and executed a malicious executable named: facebook assistant.exe

The malware deployed a REvil ransomware payload that:

- dropped a ransom note
- launched PowerShell commands
- deleted Shadow Copies
- attempted to prevent file recovery

The investigation also identified the attacker payment infrastructure hosted on a Tor onion service.

---

## 🛠️ Recommendations

Contact autorities

---

## 📸 Evidence

Ransom note 5uizv5660t-readme.txt on Administrator's Desktop (Splunk request : index=revil| rare limit=20 "winlog.event_data.TargetFilename”
<img width="737" height="628" alt="image" src="https://github.com/user-attachments/assets/fe93fe97-ef7c-48fb-9693-73c7771f321f" />

Creation of txt from the file facebook assistant.exe (Splunk request : index=revil "winlog.event_data.TargetFilename"="C:\\Users\\Administrator\\Desktop\\5uizv5660t-readme.txt” )
<img width="572" height="264" alt="image" src="https://github.com/user-attachments/assets/c91d3ac8-a3db-44e6-8fa5-e7d0af7c4f87" />

Terminal opening and SHA256 of the ransomware B8D7FB4488C0556385498271AB9FFFDF0EB38BB2A330265D9852E3A6288092AA (Splunk request : index=revil  | search "winlog.event_data.ProcessId"=5348 "winlog.event_data.TerminalSessionId"=1)
<img width="1460" height="702" alt="image" src="https://github.com/user-attachments/assets/96524182-e78d-4085-aabd-ef34685ba65e" />

Comments on obfuscation on Virus Total
<img width="1136" height="168" alt="image" src="https://github.com/user-attachments/assets/2670dd81-6b91-4d41-8e07-a438b70b8652" />

Powershell command obfuscated in base64 (Splunk request : * "winlog.event_data.CommandLine"="powershell -e RwBlAHQALQBXAG0AaQBPAGIAagBlAGMAdAAgAFcAaQBuADMAMgBfAFMAaABhAGQAbwB3AGMAbwBwAHkAIAB8ACAARgBvAHIARQBhAGMAaAAtAE8AYgBqAGUAYwB0ACAAewAkAF8ALgBEAGUAbABlAHQAZQAoACkAOwB9AA==” )
<img width="1579" height="412" alt="image" src="https://github.com/user-attachments/assets/34187ea0-23bd-4dac-8dbe-20fcdb8cae3c" />

<img width="1533" height="595" alt="image" src="https://github.com/user-attachments/assets/e7cfe610-1879-4154-91c9-020ce6a38b83" />

Body of the txt file
<img width="1555" height="657" alt="image" src="https://github.com/user-attachments/assets/65168b40-55b3-4d67-8cca-dac968a66dbd" />



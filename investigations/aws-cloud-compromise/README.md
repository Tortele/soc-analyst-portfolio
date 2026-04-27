# 🛡️ AWS Cloud Compromise Investigation

## 🎯 Objective
Identify a compromised account and analyze a potential data exfiltration within an AWS environment.

---

## 🧪 Environment
- Platform: AWS
- Logs: AWS CloudTrail
- Tool: Splunk

---

## 🔍 Analysis

### 1. Initial Observation
The account **helpdesk.luke** experienced multiple brute force attempts within a short period of time, followed by a successful login.

---

### 2. Investigation

- Shortly after the successful login, a listing of objects in an S3 bucket was performed to enumerate its contents.

- The attacker downloaded a sensitive file:
  - **Product2_CAD_Designs.dwg**
  - Bucket: `product-designs-repository31183937`

- The attacker modified the bucket:
  - `backup-and-restore98825501`
  - Changed its access settings to **public**

---

### 3. Post-Exploitation

- A new user was created:
  - **marketing.mark**

- The user was added to the **Admins group**, establishing persistence within the environment.

---

## 🧠 MITRE ATT&CK Mapping

- **TA0006** – Credential Access  
- **TA0004** – Privilege Escalation  
- **TA0003** – Persistence  

- **T1110** – Brute Force  
- **T1530** – Data from Cloud Storage  
- **T1098** – Account Manipulation  
- **T1556** – Modify Authentication Process  

---

## ⚠️ Indicators of Compromise (IOC)

- Suspicious IP: `185.192.70.78`  
- Compromised account: `helpdesk.luke`  
- Created account: `marketing.mark`  

---

## 🧠 Conclusion

The account **helpdesk.luke** was compromised through a brute force attack.  
After gaining access, the attacker:

- Accessed and enumerated S3 bucket contents  
- Downloaded sensitive design files  
- Modified a backup bucket to make it publicly accessible  
- Created a new administrative user (**marketing.mark**) to maintain persistence  

This indicates a full compromise involving data exfiltration and privilege escalation within the AWS environment.

---

## 🛠️ Recommendations

- Block the IP address: `185.192.70.78`  
- Enforce strong password policies  
- Enable Multi-Factor Authentication (MFA)  
- Implement account lockout after multiple failed attempts  
- Apply the principle of least privilege to user accounts  
- Monitor and restrict public access to S3 buckets  

---

## 📸 Evidence (Screenshots / Queries)

### Failed Authentication Attempts
Multiple failed login attempts observed on account **helpdesk.luke**
<img width="1915" height="538" alt="image" src="https://github.com/user-attachments/assets/107e2d71-f5dc-438b-88bc-4bb13d85c0a3" />

---

### Successful Login
Successful authentication at **09:54:04** following brute force attempts
<img width="1904" height="838" alt="image" src="https://github.com/user-attachments/assets/62e3fc4d-3289-4351-82ac-fee750e75b22" />

---

### S3 Bucket Enumeration
Listing of the bucket after connection (Splunk Query : index="aws_cloudtrail" "userIdentity.userName"="helpdesk.luke" eventCategory=Data)
<img width="1628" height="611" alt="image" src="https://github.com/user-attachments/assets/9834e215-88c8-46e3-8afe-878d8d64cca7" />

---

### Download of DWG File
Download of the file Product2_CAD_Designs.dwg on the bucket product-designs-repository31183937
<img width="1595" height="742" alt="image" src="https://github.com/user-attachments/assets/6ac4b9b7-35fa-4e90-8c9b-28925ec49202" />

---

### Bucket Permission Modified
Modification of the bucket (backup-and-restore98825501) access to public (Splunk Query : index="aws_cloudtrail" "userIdentity.userName"="helpdesk.luke" eventName="PutBucketPublicAccessBlock”)
<img width="1621" height="710" alt="image" src="https://github.com/user-attachments/assets/40d53856-eb21-45cc-a71c-3d5dff0c22cf" />

---

### Creation of marketing.mark user
Creation of the user marketing.mark to ensure persistence (Splunk Query : index="aws_cloudtrail" "userIdentity.userName"="helpdesk.luke" eventName=CreateUser)
<img width="1634" height="558" alt="image" src="https://github.com/user-attachments/assets/66aae73b-fbd2-41df-8191-d08f742bdddb" />

---

### Adding the user marketing.mark to the Admins Group
Add of the user marketing.mark to the Admins Group (Splunk Query : index="aws_cloudtrail" "userIdentity.userName"="helpdesk.luke" eventName=AddUserToGroup)
<img width="1634" height="565" alt="image" src="https://github.com/user-attachments/assets/8f5f117c-f541-4aab-9982-6657d696890f" />





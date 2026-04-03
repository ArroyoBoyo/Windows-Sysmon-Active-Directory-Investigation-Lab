# Windows-Sysmon-Active-Directory-Investigation-Lab
## 🚩 Problem Summary
- A Windows workstation triggered multiple failed authentication attempts against a user account, followed by an eventual successful logon
- Shortly after the successful authentication, elevated PowerShell activity was observed on the system
- This system normally would not have access to PowerShell or any administrative privileges 
- There is now concern that an internal user account may be compromised.
## 📋 Objective
- Investigate and document suspicious activity using Windows Event Logs, Sysmon telemetry, and Splunk in a simulated SOC-style workflow
- Determine whether the behavior is a false positive, suspicious, or indicative of compromise.
## 🔍 Investigation Overview
- Built a Windows VM environment with connected Windows 11 and Windows Server 2025 endpoints
- Installed and configured Sysmon for EDR processing
- Forwarded Windows and Sysmon logs to Splunk using Universal Forwarder
- Simulated failed authentication attempts followed by a successful attempt and suspicious PowerShell activity
- Reviewed relevant event data in Splunk to determine severity level
- Documented findings and response recommendations
## 🛠️ Tools Used
- ✅ Windows 11 VM
- ✅ Active Directory on Windows Server 2025
- ✅ Sysmon
- ✅ Splunk Enterprise and Universal Forwarder
- ✅ Windows Event Logs
## 🤝 Resolution Summary
- Confirmed that failed logon activity and PowerShell execution across Windows Event and Sysmon Logs
- Determined that the investigated behavior was suspicious and warranted further review and escalation
## ⏭️ Recommended Next Steps
- Review the affected user account activity for lateral movement, persistence, and C2 connection attempts
- Tighten monitoring and alerting for repeated failed authentication attempts within a short period of time
- Expand PowerShell logging and detection coverage
- Validate new endpoint hardening controls related to authentication and privileged command execution
# 📸 Screenshots
<img width="1894" height="646" alt="00-Sysmon-addon-proof" src="https://github.com/user-attachments/assets/5ab5f467-4733-4166-b0d6-d1fe7a32673f" />
<img width="945" height="766" alt="01-creating-victim-user-AD" src="https://github.com/user-attachments/assets/bf4717b6-4b45-495c-b14b-6dea0979c42a" />
<img width="951" height="766" alt="02-new-user-confirmation" src="https://github.com/user-attachments/assets/5c4163b0-6fb1-4571-a98e-297a111098af" />
<img width="1627" height="1148" alt="03-vitcim-login-attempts" src="https://github.com/user-attachments/assets/a371d127-6252-4416-87e5-5bd856a447ef" />
<img width="1273" height="1251" alt="04-victim-successful-login" src="https://github.com/user-attachments/assets/07d8e8f5-0af9-4ce5-b123-08e656609fd7" />
<img width="1278" height="746" alt="05-victim-powershell commands-1" src="https://github.com/user-attachments/assets/62481dfa-2fbb-4a10-b290-dc3060dad5b3" />
<img width="1277" height="778" alt="06-victim-powershell commands-2" src="https://github.com/user-attachments/assets/22f81481-23bf-4971-9de7-2cafee67f9cd" />
<img width="1633" height="1067" alt="07-Suspicous-logon-activity-detected" src="https://github.com/user-attachments/assets/dc22110e-1c98-48c4-bfd7-556d874c2b09" />
<img width="803" height="649" alt="08-victim-user-identification" src="https://github.com/user-attachments/assets/826aee11-0a16-4ecb-9744-4086086e5546" />
<img width="674" height="642" alt="09-first-failed-login-attempt" src="https://github.com/user-attachments/assets/ea30f8e2-3e9e-41bb-bf2b-4e3c3d835379" />
<img width="1136" height="474" alt="10-first-successful-login-attempt" src="https://github.com/user-attachments/assets/3faab265-f6a1-4a6d-8262-2c8d2906e114" />
<img width="1621" height="1080" alt="11-rapid-process-alerts-login-attempts" src="https://github.com/user-attachments/assets/4f2daeea-f6b0-4816-a5d4-890e9b338ec0" />
<img width="1201" height="732" alt="12-powershell-usage-proof" src="https://github.com/user-attachments/assets/3b187483-be2f-4a44-9cbc-66b537719662" />
<img width="1137" height="752" alt="13-more-powershell-process-proof" src="https://github.com/user-attachments/assets/060b2366-4e05-4bd0-8c0b-8b3f73998099" />
<img width="1267" height="985" alt="14-first-powershell-usage-attempt" src="https://github.com/user-attachments/assets/e13832e6-f3be-4b11-92da-ce88b56b262e" />
<img width="1133" height="919" alt="15-specific-commands-used-proof" src="https://github.com/user-attachments/assets/b0155a78-a734-4072-8ca8-05f3377884d2" />

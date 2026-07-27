# My write up BOTSV1.
This is my personal learning result on Botsv1 dataset.I did this on my own, there's also AI support but most of the work i did on my own. Check it out!

# [DFIR Report] Splunk Incident Investigation: Defacement & Cerber Ransomware (BOTSv1)

## 📌 Executive Summary
Báo cáo này trình bày quy trình điều tra chuyên sâu (Digital Forensics & Incident Response - DFIR) cho một chuỗi tấn công đa giai đoạn (Multi-stage Attack) xảy ra trong môi trường doanh nghiệp mô phỏng (Dataset **Boss of the SOC v1 - BOTSv1**). 

Cuộc tấn công bắt đầu bằng việc thăm dò lỗ hổng web, thực hiện Brute-force credentials, leo leo quyền bằng Web Shell, và cuối cùng phát tán mã độc mã hóa dữ liệu **Cerber Ransomware** sang các máy trạm và máy chủ quản lý tên miền (Domain Controller).

* **Target Scope:** 
  * Web Server (`192.168.250.70` - IIS/Joomla)
  * Workstation (`192.168.250.100` - User: `bob.smith`)
  * Domain Controller (`192.168.250.20` - `we9041srv`)
* **Attacker Infrastructure:** `40.80.148.42`, `23.22.63.114`
* **Primary SIEM Tool:** Splunk Enterprise (Log Sources: Sysmon, Suricata IDS, Fortigate UTM, Stream HTTP/SMB, WinRegistry).

---
Indicators of Compromise (IoCs)
1. Network IndicatorsAttacker IPs: 40.80.148.42, 23.22.63.114
2. Malicious Domains / C2:prankglassinebracket.jumpingcrab.com:1337
3. solidaritedeproximite.orgdedie73.olfsoft.net (37.187.37.150)
4. C2 IP: 92.222.104.182, 85.93.3.2512.


agent.php/joomla/media/ (Webshell)      HASH: N/A
3791.exe Web Server Trojan       HASH: ec78c938d8453739ca2a370b9c275971ec46caf6e479de2b2d04e97cc47fa45d (SHA256)
osk.exe%AppData%\Roaming\{GUID}\ HASH: C8F3F0A33EFE38E9296EF79552C4CADF6CF0BDE6 (SHA1)
System.dll%Temp%\nsaf2E7.tmp\    HASH: B6AC11DFB0D1FC75AD09C56BDE7830232395785 (SHA1)
CDrom.dll%AppData%\Roaming\      HASH: 171B499A512CDEEE8EE2553B2099D77B6799A427 (SHA1)

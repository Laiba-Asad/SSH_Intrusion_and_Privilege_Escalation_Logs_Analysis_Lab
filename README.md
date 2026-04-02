# SSH Intrusion & Privilege Escalation – Incident Analysis

This project documents a simulated **SSH brute force attack** followed by **privilege escalation and persistence techniques** on a Linux server.

---

## Overview

The objective of this lab was to analyze a full attack chain, including:

- Brute force authentication attempts  
- Initial system compromise  
- Privilege escalation to root  
- Persistence via cron jobs  
- System tampering and package manipulation  

---

## Environment

- **Target:** Server1 (Ubuntu)  
- **IP Address:** 192.168.1.156  
- **Attacker IP:** 192.168.1.166  
- **Service Targeted:** SSH (Port 22)  
- **Tool Used:** Wazuh SIEM  

---

## Attack Timeline

### Initial Access (23:10 – 23:35)
- Multiple failed SSH login attempts  
- Attempts using invalid and valid usernames  
- Clear brute-force pattern observed  

**MITRE:** T1110 – Brute Force  

---

### Successful Compromise (00:36)
- Successful login to user `server1`  
- Interactive session established  

---

### Persistence Activity (00:37 – 00:54)
- Multiple crontab modifications  
- Indicates scheduled task persistence  

**MITRE:** T1053 – Scheduled Task/Cron  

---

###  Privilege Escalation (01:08)
- Successful `sudo` access to root  
- Full system-level privileges obtained  

**MITRE:** T1548.003 – Sudo  

---

### System Tampering
- Removal and reinstallation of critical packages:
  - sudo  
  - ubuntu-minimal  
- Indicates attempt to weaken system defenses  

---

### Continued Activity
- Additional cron modifications  
- Failed and successful privilege escalation attempts  
- Repeated sudo usage  

---

### Potential Backdoor Installation (02:11)
- Multiple dpkg installation requests  
- Possible installation of malicious tools  

---

## Key Indicators

- High volume of failed SSH logins  
- Unauthorized successful login  
- Repeated cron job modifications  
- Sudo privilege escalation  
- Package management activity (dpkg logs)  

---

## Analysis

This attack demonstrates a complete intrusion lifecycle:

1. Initial access via brute force  
2. Establishing persistence via cron jobs  
3. Escalating privileges to root  
4. Manipulating system packages  
5. Attempting to maintain long-term access  

---

## Impact

- Partial root compromise  
- System-level modifications  
- Potential persistence mechanisms deployed  

---

## MITRE ATT&CK Mapping

| Technique | ID |
|----------|----|
| Brute Force | T1110 |
| Scheduled Task (Cron) | T1053 |
| Sudo Privilege Escalation | T1548.003 |

---

## Key Learnings

- Weak authentication enables brute force attacks  
- Cron jobs are commonly used for persistence  
- Privilege escalation is a critical detection point  
- Package tampering indicates deeper compromise  
- Continuous monitoring is essential for early detection  

---

## Recommendations

- Implement account lockout policies  
- Disable password-based SSH authentication  
- Monitor cron and package activity  
- Enable file integrity monitoring  
- Block suspicious IPs  

---

## Conclusion

This lab demonstrates how attackers move from initial access to full system compromise. It highlights the importance of monitoring authentication, privilege escalation, and persistence mechanisms in a SOC environment.

---

## Author

Laiba Asad

# SSH Bruteforce Investigation

## CASE DETAILS
Incident Type: SSH Bruteforce Activity   
Environment: Ubuntu (Wazuh Lab)  
Severity: HIGH  
Status: Closed  
Analyst: Niharika  

---

## EXECUTIVE SUMMARY:
A brute force attack was identified targeting the user phoebe on the endpoint. The attack involved multiple failed SSH login attempts from an external IP (10.0.2.30), followed by a successful authentication within a short timeframe. Shortly after gaining access, a sudo to root was executed, indicating privilege escalation. This sequence confirms unauthorized access and full system compromise.

**Outcome:** Brute force attack successful. Privilege escalation to root confirmed.

---

## WHO:
User: phoebe  
Host: phoebe-VirtualBox  
Attacker Source IP: 10.0.2.30  

---

## WHAT:
1. From 10.0.2.30 multiple failed login attempted
2. Successfull login to phoebe from 10.0.2.30
3. Privilege escalation was observed via execution of `/usr/bin/su`, indicating a switch to root privileges.

---

## WHEN:
1. Multiple failed login attempts - 18:16:43 to 18:16:45
2. Successfull login - 18:16:47
3. Successfull sudo to ROOT access - 18:22:33  
*Timeline observed via Wazuh alerts correlation*

---

## WHY:
**Attacker Goal:**
- Gain unauthorized access via password brute force
- Escalate privileges to root level

---

## HOW:
1. Attacker initiated multiple SSH login attempts from external IP
2. High-frequency failed attempts indicate automated brute force
3. Successful authentication achieved using valid credentials
4. `sudo` access gained by attacker indicating privilege escalation

---

## IMPACT
**Observed Impact:**
- Unauthorized system access confirmed
- Root-level privileges obtained

**Potential Impact:**
- Full system control by attacker
- Ability to execute further malicious actions

---

## ATTACK FLOW 
Brute Force → Successful Authentication → Privilege Escalation

--- 

## MITRE ATT&CK MAPPING
| Tactic      | Technique                                | ID        |
| ----------- | ---------------------------------------- | --------- |
| Credential Access | Password Guessing | T1110.001 |
| Privilege Escalation | Valid Accounts / Sudo Abuse | T1078 |

---

## INDICATORS OF COMPROMISE (IOCs)
IP : 10.0.2.30  
Commands: ssh, sudo / su

---

## VALIDATION CHECKS
- Verified whether IP 10.0.2.30 is trusted or known  
- Reviewed login history for abnormal access patterns
- Checked if user phoebe typically performs sudo operations
- Investigated for additional suspicious activity post-login

---

## FINAL ASSESSMENT:
Confirmed brute-force attack resulting in successful authentication and privilege escalation to root.

---

## RECCOMENDATIONS:
- Block or investigate source IP (10.0.2.30)
- Reset credentials for affected user
- Enable account lockout policies
- Implement MFA for SSH access
- Restrict and monitor sudo privileges
- Conduct further review for post-compromise activity
- Escalate to Incident Response (L2)

---

## EVIDENCE

Wazuh detected:

- Multiple failed SSH login attempts

  ![failedlogins](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/failed-loginattempts.png)
  
- Successfull login to phoebe from 10.0.2.30

   ![successfullogin](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/successful%20login%20.png)
  
- Successfull sudo to ROOT access

   ![rootaccess](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/successful%20root%20access.png)
  
Logs were analyzed from:
`/var/log/auth.log` (collected via the Wazuh agent)

---

## What I Learned

- How to analyze Wazuh alerts and authentication logs to understand suspicious login activity.
- How to correlate multiple failed SSH login attempts followed by a successful login to recognize a possible brute-force attack.
- How privilege escalation using sudo appears in Linux logs during an investigation.
- How to write my first security incident investigation report based on the findings.
- The importance of mitigation strategies such as strong password policies and account lockout after multiple failed login attempts.

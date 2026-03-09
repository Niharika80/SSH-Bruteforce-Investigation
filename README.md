# Linux Threat Detection with Wazuh

## Project Overview
This SOC lab simulates a Linux attack chain involving SSH brute force and privilege escalation, analyzes Wazuh alerts, and documents the investigation in a security incident report.

## Lab Environment

![SOC Lab Architecture](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/linux%20.drawio.png)

Attacker Machine: Kali Linux (10.0.2.30)  
Target Machine: Ubuntu Linux (10.0.2.20) with Wazuh Agent installed    
Monitoring Tool: Wazuh  

## Attack Simulation

1. SSH brute force using Hydra
   
   ![attack](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/attack.png)
   
2. Successful login with compromised credentials
   
   ![login](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/ssh%20login.png)
   
3. Privilege escalation using `sudo su`
   
   ![rootaccess](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/root%20access%202.png)
   
## Detection

Wazuh detected:

- Multiple failed SSH login attempts

  ![failedlogins](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/failed-loginattempts.png)
  
- Successful login after brute force

   ![successfullogin](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/successful%20login%20.png)
  
- Privilege escalation using sudo

   ![rootaccess](https://github.com/Niharika80/Linux-Threat-Detection-with-Wazuh/blob/0530ad3bf809f5c9d24a82840b93c7deefc49f0b/screenshots/successful%20root%20access.png)
  
Logs were analyzed from:
`/var/log/auth.log` (collected via the Wazuh agent)

## Incident Report

Full report available in:
report/incident-report.md

## What I Learned

- How to analyze Wazuh alerts and authentication logs to understand suspicious login activity.
- How to correlate multiple failed SSH login attempts followed by a successful login to recognize a possible brute-force attack.
- How privilege escalation using sudo appears in Linux logs during an investigation.
- How to write my first security incident investigation report based on the findings.
- The importance of mitigation strategies such as strong password policies and account lockout after multiple failed login attempts.

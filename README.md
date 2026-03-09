# Linux Threat Detection with Wazuh

## Project Overview
This SOC lab simulates a Linux attack chain involving SSH brute force and privilege escalation, analyzes Wazuh alerts, and documents the investigation in a security incident report.

## Lab Environment

Attacker Machine: Kali Linux (10.0.2.30)
Target Machine: Ubuntu Linux (10.0.2.20) with Wazuh Agent installed  
Monitoring Tool: Wazuh

## Attack Simulation

1. SSH brute force using Hydra
2. Successful login with compromised credentials
3. Privilege escalation using sudo

## Detection

Wazuh detected:

- Multiple failed SSH login attempts
- Successful login after brute force
- Privilege escalation using sudo

Logs were analyzed from:
`/var/log/auth.log` (collected via the Wazuh agent)

## Incident Report

Full report available in:
report/incident-report.md



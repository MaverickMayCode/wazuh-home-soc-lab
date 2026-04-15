# Event Simulations
See ["incident-reports.md"](https://github.com/MaverickMayCode/wazuh-home-soc-lab/blob/main/docs/incident-reports.md) for incident reports.

## 🔑 Simulation Index

- [Simulation 1: Failed Authentication Attempts](#simulation-1-failed-authentication-attempts)
- [Simulation 2: Successful Account Creation](#simulation-2-successful-account-creation)
- [Simulation 3: Successful Privilege Escalation](#simulation-3-successful-privilege-escalation)
- [Simulation 4: Baisc Low-Level Nmap Scan - Kali ATTACKER](#simulation-4-basic-low-level-nmap-scan---kali-attacker)
- [Simulation 5: Network Login Attempt (SMB) - Kali ATTACKER](#simulation-5-network-login-attempt-smb---kali-attacker)

## Objective
Simulate security events to test SIEM detection capabilities.

## 💻 Simulation 1: Failed Authentication Attempts
- Incident Report: https://github.com/MaverickMayCode/wazuh-home-soc-lab/blob/main/docs/incident-reports.md

### Command Used: net use \127.0.0.1\fake /user:fakeuser wrongpassword

### Description

- Generated multiple failed login attempts
- Simulates credential abuse / brute force behavior

<img width="974" height="504" alt="70645b3c-3f2f-44a6-a3af-b1076873f5f5" src="https://github.com/user-attachments/assets/20d60959-f692-4569-91f7-f51de71192f9" />
<img width="1870" height="924" alt="04055a2a-553b-4248-97db-48d2f8747eb9" src="https://github.com/user-attachments/assets/4ed352e2-962b-41b7-9e55-0ea8fdc01d5f" />

## 💻 Simulation 2: Successful Account Creation
- Incident Report: https://github.com/MaverickMayCode/wazuh-home-soc-lab/blob/main/docs/incident-reports.md

### Commands Used

Create user: net user testuser Password123! /add

### Description

- Simulates successful authorized account creation

<img width="855" height="169" alt="561cf6ed-2bf5-4c06-9c13-1c7f867e6bc9" src="https://github.com/user-attachments/assets/aaf08687-1adf-42d8-bf45-60c01a274690" />
<img width="1859" height="369" alt="0975720f-5449-4d6b-854b-3640bf6e774a" src="https://github.com/user-attachments/assets/7bdcb7b6-72d2-4795-b7bf-4f3cc291bf4d" />

## Outcome

- Wazuh generated alerts for:
  - Account creation

## 💻 Simulation 3: Successful Privilege Escalation
- Incident Report: https://github.com/MaverickMayCode/wazuh-home-soc-lab/blob/main/docs/incident-reports.md

### Commands Used

Add to admin group: net localgroup administrators testuser /add

### Description

- Simulates successful privilege escalation

<img width="857" height="220" alt="3f97d454-4c0e-4b04-85e4-d621cff7525c" src="https://github.com/user-attachments/assets/bb19a822-3abb-4692-9716-337f8d487a29" />
<img width="1860" height="67" alt="39baac69-e4a1-4bae-b8c4-3d582ab1191c" src="https://github.com/user-attachments/assets/22c9370a-6099-4686-90db-27e418be13e3" />
<img width="1778" height="857" alt="b8349931-deb4-47d0-9120-0d0588f48691" src="https://github.com/user-attachments/assets/66e238c6-bdf0-4904-b102-51ed265b768d" />

## Outcome

- Wazuh generated alerts for:
  - Successful privilege escalation activity

## 💻 Simulation 4: Baisc Low-Level Nmap Scan - Kali ATTACKER
- Incident Report: https://github.com/MaverickMayCode/wazuh-home-soc-lab/blob/main/docs/incident-reports.md

### Commands Used

Nmap Scan from Kali ATTACKER: nmap -sS 192.168.4.22

### Description

- Ran a basic network scan that searches for exposed services/ports on a Windows endpoint

<img width="1100" height="697" alt="ab8fe2eb-1d69-430c-96db-f06157489c85" src="https://github.com/user-attachments/assets/bab8aecb-977c-4e9d-a2c7-81f26cce9ca7" />

## Outcome

- Wazuh generated alerts for:
  - None of the processes executed by the Kali ATTACKER during the Nmap scan showing the gap in log generation certain endpoint operating systems can have - like our Windows endpoint
- ATTACKER gained:
  - Insight into the vunerable ports on our Windows endpoint
 
## 💻 Simulation 5: Network Login Attempt (SMB) - Kali ATTACKER
- Incident Report: https://github.com/MaverickMayCode/wazuh-home-soc-lab/blob/main/docs/incident-reports.md

### Commands Used

Network Login attempt from Kali ATTACKER: smbclient -L //192.168.4.22 -U fakeuser

### Description

- Kali ATTACKER used the command listed to attempt to log in to the SMB service on our windows endpoint

### Single Attempt from Kali ATTACKER

<img width="703" height="547" alt="firstkali" src="https://github.com/user-attachments/assets/7ab2b0b4-37d3-4ad6-86dc-42a5b4f5c27f" />

### Alert from Wazuh

<img width="1874" height="169" alt="firstalert" src="https://github.com/user-attachments/assets/8cb43a22-919d-4a52-9a38-fef8dc953b90" />

### Multiple Attempts from Kali ATTACKER

<img width="778" height="619" alt="multikali" src="https://github.com/user-attachments/assets/f377ad99-b654-436b-b863-db1e30179666" />

### Alerts from Wazuh

<img width="1880" height="546" alt="88f9e44a-cb22-41fa-ab28-187e4159a449" src="https://github.com/user-attachments/assets/66bad29f-c119-4716-8658-4e1908c7c2b8" />

### Wazuh Escalates the Issue - Escalation Log

<img width="1857" height="61" alt="esca" src="https://github.com/user-attachments/assets/00237f40-d760-4a74-8203-69b949259309" />

### Wazuh Escalates the Issue -  Log Details

<img width="1875" height="897" alt="esca1" src="https://github.com/user-attachments/assets/d837dee0-2612-4711-a740-da35c8f3c54a" />

## Outcome

- Wazuh generated alerts for:
  - Single/Multiple failed login attempts using a fake user account to attempt to gain SMB access
- ATTACKER gained:
  - Confirmed the target endpoint is reachable and accepting SMB authentication requests
  - Identified that SMB (port 445) is active and responding
  - Determined the attempted username was invalid or incorrect




# Event Simulations
See "incident-reports.md" for reports.

## Objective
Simulate security events to test SIEM detection capabilities.

## Simulation 1: Failed Authentication Attempts - Incident Report: https://github.com/MaverickMayCode/wazuh-home-soc-lab/blob/main/docs/incident-reports.md

### Command Used: net use \127.0.0.1\fake /user:fakeuser wrongpassword

### Description

- Generated multiple failed login attempts
- Simulates credential abuse / brute force behavior

<img width="974" height="504" alt="70645b3c-3f2f-44a6-a3af-b1076873f5f5" src="https://github.com/user-attachments/assets/20d60959-f692-4569-91f7-f51de71192f9" />
<img width="1870" height="924" alt="04055a2a-553b-4248-97db-48d2f8747eb9" src="https://github.com/user-attachments/assets/4ed352e2-962b-41b7-9e55-0ea8fdc01d5f" />

## Simulation 2: Successful Account Creation

### Commands Used

Create user: net user testuser Password123! /add

### Description

- Simulates successful authorized account creation

<img width="855" height="169" alt="561cf6ed-2bf5-4c06-9c13-1c7f867e6bc9" src="https://github.com/user-attachments/assets/aaf08687-1adf-42d8-bf45-60c01a274690" />
<img width="1859" height="369" alt="0975720f-5449-4d6b-854b-3640bf6e774a" src="https://github.com/user-attachments/assets/7bdcb7b6-72d2-4795-b7bf-4f3cc291bf4d" />

## Outcome

- Wazuh generated alerts for:
  - Account creation

## Simulation 3: Successful Privilege Escalation

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


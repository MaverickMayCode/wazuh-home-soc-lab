# Attack Simulations

## Objective
Simulate malicious behavior to test SIEM detection capabilities.

## Simulation 1: Failed Authentication Attempts

### Command Used: net use \127.0.0.1\fake /user:fakeuser wrongpassword

### Description

- Generated multiple failed login attempts
- Simulates credential abuse / brute force behavior

<img width="974" height="504" alt="70645b3c-3f2f-44a6-a3af-b1076873f5f5" src="https://github.com/user-attachments/assets/20d60959-f692-4569-91f7-f51de71192f9" />
<img width="1870" height="924" alt="04055a2a-553b-4248-97db-48d2f8747eb9" src="https://github.com/user-attachments/assets/4ed352e2-962b-41b7-9e55-0ea8fdc01d5f" />

## Simulation 2: Privilege Escalation

### Commands Used

Create user: net user testuser Password123! /add

Add to admin group: net localgroup administrators testuser /add

### Description

- Simulates unauthorized account creation
- Simulates privilege escalation

## Outcome

- Wazuh generated alerts for:
  - Failed logins
  - Multiple login failures (brute force)
  - Account creation
  - Privilege escalation activity


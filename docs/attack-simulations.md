# Attack Simulations

## Objective
Simulate malicious behavior to test SIEM detection capabilities.

## Simulation 1: Failed Authentication Attempts

### Command Used: net use \127.0.0.1\fake /user:fakeuser wrongpassword

### Description

- Generated multiple failed login attempts
- Simulates credential abuse / brute force behavior

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


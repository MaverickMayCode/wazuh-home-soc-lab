# Incident Reports

## 🔑 Incident Report Index

- [💻 Simulation 1: Failed Authentication Attempts](#-simulation-1-failed-authentication-attempts)
- [💻 Simulation 2: Successful User Creation](#-simulation-2-successful-user-creation)
- [💻 Simulation 3: Successful Privilege Escalation](#-simulation-3-successful-privilege-escalation)
- [💻 Simulation 4: Basic Low-Level Nmap Scan - Kali ATTACKER](#-simulation-4-basic-low-level-nmap-scan---kali-attacker)
- [💻 Simulation 5: Network Login Attempt (SMB) - Kali ATTACKER](#-simulation-5-network-login-attempt-smb---kali-attacker)

---

# 💻 Simulation 1: Failed Authentication Attempts

## Summary
Simulated multiple failed login attempts on a Windows endpoint to test SIEM detection.

## Observations

- Multiple "logon failure" events detected  
- Wazuh escalated alert severity after repeated attempts  
  - Alerts escalated from "Logon failure - Unknown user or bad password." (Level 5) to "Multiple Windows logon failures." (Level 10)

## Key Alert - where the issue became escalated

Rule ID: 60204  
Level: 10  
Description: Multiple Windows logon failures  
MITRE Technique: T1110 (Brute Force)

## Timeline

- Initial failed login attempts recorded  
- Repeated attempts triggered a correlation rule  
- High severity alert generated - Multiple Windows logon failures  

## Analysis

Wazuh identified a clear pattern of repeated failed authentication attempts, indicating potential brute-force activity.

## Conclusion

Wazuh successfully detected and escalated suspicious authentication behavior, showing strong log correlation and threat detection capabilities.

---

# 💻 Simulation 2: Successful User Creation

## Summary
Executed user creation commands on a Windows endpoint to test SIEM detection.

## Observations

- Multiple logs detailing the command execution, including:
  - Domain users group changed | ID: 60160 | Level: 5  
  - User account enabled or created | ID: 60109 | Level: 8  
  - User account changed | ID: 60110 | Level: 8  
  - Users group changed | ID: 60170 | Level: 5  

## Timeline

- Initial user creation with no group assigned  
- User account created under the name: testuser  
- testuser was assigned attributes, including a "Password Last Set" timestamp  
- testuser added to the "Users" group  

## Analysis

Wazuh tracked the full lifecycle of the account creation process, including attribute assignment and group membership.

## Conclusion

Wazuh successfully detected the user account creation process on the Windows endpoint. Logs like these are important for identifying suspicious activity and catching potential privilege escalation early. They act as a strong first line of defense.

---

# 💻 Simulation 3: Successful Privilege Escalation

## Summary
Executed privilege escalation commands on a Windows endpoint to test SIEM detection.

## Observations

- A single high-level alert detected:
  - Administrators group changed | ID: 60154 | Level: 12 | MITRE Technique: T1484  
- Highest severity alert observed so far  
- Wazuh dashboard reflected "Level 12 or above" alerts, highlighting the risk of this action  

## Timeline

- User (testuser) successfully added to the "Administrators" group  

## Analysis

Wazuh identified a user account escalating its privileges to an administrative level.

## Conclusion

Wazuh successfully detected the privilege escalation event on the Windows endpoint. Alerts at this level are critical due to the level of access gained. If this were a real attack, the damage potential would be significantly higher once admin privileges are obtained.

---

# 💻 Simulation 4: Basic Low-Level Nmap Scan - Kali ATTACKER

## Summary
Used my Kali ATTACKER VM to run a basic Nmap scan against a Windows endpoint to test SIEM detection.

## Observations

- The endpoint did not generate logs for this activity  
- As a result, no relevant events were visible in Wazuh  
- The scan still successfully gathered useful information for the attacker, including open ports on the endpoint  

## Timeline

- Ran the scan from the Kali ATTACKER VM  
- Monitored Wazuh for generated logs  
- No logs were created for this activity  

## Analysis

Wazuh did not detect this event because it relies on endpoint-generated logs. Since the Windows endpoint did not log this type of network activity, the SIEM had no visibility into the scan.

- This highlights a detection gap in endpoint-based monitoring  
- Attackers can gather valuable reconnaissance data without triggering alerts  

## Conclusion

Basic Nmap scans can allow attackers to gather insight into a system while remaining undetected by endpoint-based logging systems. This reinforces the importance of layered security, where network monitoring tools (IDS/IPS) are used alongside SIEM solutions to improve visibility.

---

# 💻 Simulation 5: Network Login Attempt (SMB) - Kali ATTACKER

## Summary
Simulated multiple failed login attempts from the Kali ATTACKER to the Windows endpoint’s SMB service to test SIEM detection.

## Observations

- Multiple "logon failure" events detected  
- Wazuh escalated alert severity after repeated login attempts  
  - Alerts escalated from "Logon failure - Unknown user or bad password." (Level 5) to "Multiple Windows logon failures." (Level 10)

## Key Alert - where the issue became escalated

Rule ID: 60204  
Level: 10  
Description: Multiple Windows logon failures  
MITRE Technique: T1110 (Brute Force)

## Timeline

- Initial failed login attempt  
- Wazuh generated an alert tied to the attempt  
- Repeated attempts triggered additional alerts and a correlation rule  
- High severity alert generated due to multiple failed logon attempts  

## Analysis

Wazuh identified a pattern of repeated failed authentication attempts targeting the SMB service on the Windows endpoint, indicating potential brute-force activity.

## Conclusion

Wazuh successfully detected and escalated suspicious authentication behavior, again showing strong log correlation. It also captured the username used during the attack attempts, which helps narrow down potential threat activity.

This kind of visibility becomes even more useful when paired with strategies like honeytokens. If fake credentials were planted and an attacker attempted to use them, it would provide a high-confidence indicator of malicious activity, allowing security teams to quickly identify and respond to threats.
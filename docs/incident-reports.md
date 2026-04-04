# Simulation 1: Failed Authentication Attempts

## Summary
Simulated multiple failed login attempts on a Windows endpoint to test SIEM detection.

## Observations

- Multiple "logon failure" events detected
- Wazuh escalated alert severity after repeated attempts
  - Alerts escalated from "Logon failure - Unknown user or bad password." with a score of 5 to: "Multiple Windows logon failures." with a score of 10.

## Key Alert - where the issue became escalated

Rule ID: 60204  
Level: 10  
Description: Multiple Windows logon failures  
MITRE Technique: T1110 (Brute Force)

## Timeline

- Initial failed login attempts recorded
- Repeated attempts triggered correlation rule 
- High severity alert generated - Multiple Windows logon failures.

## Analysis

The SIEM identified a pattern of repeated failed authentication attempts, indicating potential brute-force activity.

## Conclusion

Wazuh successfully detected and escalated suspicious authentication behavior demonstrating log correlation and threat detection.

# Simulation 2: Successful User Creation

## Summary
Ran successful user creation commands being executed on a Windows endpoint to test SIEM detection.

## Observations

- Multiple logs detailing the command run including
  - Domain users group changed. | ID: 60160 | Level: 5
  - User account enabled or created. | ID: 60109 | Level: 8
  - User account changed. | ID: 60110 | Level: 8
  - Users group changed. | ID: 60170 | Level: 5

## Timeline

- Initial user creation with no group assigned
- User account assigned to account name: testuser 
- testuser was assigned a list of attributes
- testuser was assigned a "Password Last Set" time in attributes
- testuser added to group name: Users

## Analysis

The SIEM identified a user account and it's process of being created.

## Conclusion

Wazuh successfully detected the user account creation process from the Windows endpoint. Logs like these are crucial in detecting malicious activity and further privledge escalation down the line and are important as a "first line of defence" for proactive cybersecurity practices.

# Simulation 3: Successful Privledge Escalation

## Summary
Executed successful privledge escalation commands on a Windows endpoint to test SIEM detection.

## Observations

- A single log detailing: Administrators group changed. | ID: 60154 | Level: 12 | MITRE Technique: T1484
- A new high score! Our highest leveled threat yet.
- Wazuh dashboard updated to mark "1 - Level 12 or above alerts" signifying the potenial security hazards an incident like this can bring

## Timeline

- A member (our user) was added to Group Name: Administrators with success

## Analysis

The SIEM identified a user account escalating its privledges to admin.

## Conclusion

Wazuh successfully detected the priveledge escalation from the Windows endpoint. These logs are so important and are leveled so high because of the potential damage a malicious threat can do with escalated privledges.

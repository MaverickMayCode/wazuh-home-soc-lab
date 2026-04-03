# Incident Report: Brute Force Detection

## Summary
Simulated multiple failed login attempts on a Windows endpoint to test SIEM detection capabilities.

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

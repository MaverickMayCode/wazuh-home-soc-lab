# Incident Report: Brute Force Detection

## Summary
Simulated multiple failed login attempts on a Windows endpoint to test SIEM detection capabilities.

## Observations

- Multiple "logon failure" events detected
- Wazuh escalated alert severity after repeated attempts

## Key Alert

Rule ID: 60204  
Level: 10  
Description: Multiple Windows logon failures  
MITRE Technique: T1110 (Brute Force)

## Timeline

- Initial failed login attempts recorded
- Repeated attempts triggered correlation rule
- High severity alert generated

## Analysis

The SIEM identified a pattern of repeated failed authentication attempts, indicating potential brute-force activity.

## Conclusion

Wazuh successfully detected and escalated suspicious authentication behavior demonstrating log correlation and threat detection.

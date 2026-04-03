# Log Ingestion

## Overview
Log ingestion is the process of collecting logs from endpoints and sending them to the SIEM.

## Process

1. Installed Wazuh agent on Windows host
2. Configured agent to communicate with Wazuh server (192.168.4.82)
3. Started Wazuh agent service

## Result

- Logs from Windows system successfully sent to Wazuh server
- Endpoint appeared as "Active" in dashboard

## Types of Logs Collected

- Windows Security Logs
- Authentication events
- System activity

## Key Insight

The SIEM cannot detect threats without log ingestion. This step is critical for enabling visibility into endpoint behavior.

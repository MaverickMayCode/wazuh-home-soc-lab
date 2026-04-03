# Lab Architecture

## Overview
This lab simulates a basic Security Operations Center (SOC) environment using Wazuh SIEM.

## Components

### 1. Wazuh Server (SIEM)
- Hosted on an Ubuntu Server virtual machine using VirtualBox
- IP Address: 192.168.4.82
- Role:
  - Collect logs from endpoints
  - Analyze and correlate events
  - Generate security alerts

### 2. Endpoint (Agent)
- Windows 10 host machine
- Wazuh agent installed
- Role:
  - Generate system and security logs
  - Send logs to Wazuh server

### 3. Network Configuration
- VirtualBox configured using Bridged Adapter
- Allows communication between host and virtual machines

## Data Flow

Endpoint (Windows PC) -> logs -> Wazuh Agent -> Wazuh Server (SIEM) -> Wazuh Dashboard

## Key Concept

The agent acts as the data source, while the SIEM acts as the analysis engine that detects suspicious behavior.

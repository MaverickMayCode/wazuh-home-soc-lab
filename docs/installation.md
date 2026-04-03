# Installation Process

## Step 1: Environment Setup
- Installed Oracle VirtualBox
- Allocated 8GB RAM, 4 CPU cores, and 60GB storage for Wazuh server VM
- Installed Ubuntu Server 22.04

## Step 2: System Preparation

- Updated system: sudo apt update && sudo apt upgrade -y
- Installed dependencies: sudo apt install curl unzip apt-transport-https lsb-release gnupg -y

## Step 3: Wazuh Installation

Downloaded installer: curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh

Installed Wazuh: sudo bash wazuh-install.sh -a -i

## Step 4: Network Configuration

- Initially used NAT (could not access dashboard)
- Switched to Bridged Adapter
- Assigned IP: 192.168.4.82

## Step 5: Dashboard Access

Accessed via:
https://192.168.4.82

## Step 6: Agent Installation (Windows)

Installed agent using PowerShell: Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.7.5-1.msi
 -OutFile ${env.tmp}\wazuh-agent;
msiexec.exe /i ${env.tmp}\wazuh-agent /q WAZUH_MANAGER='192.168.4.82' WAZUH_AGENT_NAME='windows-host' WAZUH_REGISTRATION_SERVER='192.168.4.82'

Started service: NET START WazuhSvc

Agent online...

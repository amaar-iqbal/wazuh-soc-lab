# Wazuh SOC Lab – Commands Reference

This document contains all major commands used during the deployment, configuration, and testing of the Wazuh SIEM lab.

---

# 1. Wazuh Manager (Ubuntu Server)

## System Update
sudo apt update
sudo apt upgrade -y

## Install Required Dependencies
sudo apt install curl unzip wget apt-transport-https -y

## Configure vm.max_map_count (Required for OpenSearch)
sudo nano /etc/sysctl.conf

Add:
vm.max_map_count=262144

Apply changes:
sudo sysctl -p

## Install Wazuh All-in-One Stack
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a

## Verify Services
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard

---

# 2. Kali Linux – Agent Installation

## Add Wazuh GPG Key
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | sudo gpg --dearmor -o /usr/share/keyrings/wazuh.gpg

## Add Wazuh Repository
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | sudo tee /etc/apt/sources.list.d/wazuh.list

## Update Repository List
sudo apt update

## Install Agent
sudo apt install wazuh-agent -y

## Configure Manager IP
sudo nano /var/ossec/etc/ossec.conf

Set manager IP:
192.168.153.138

## Register Agent
sudo /var/ossec/bin/agent-auth -m 192.168.153.138

## Start Agent
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

## Check Agent Status
sudo systemctl status wazuh-agent

---

# 3. Linux Mint – Agent Installation

## Install Agent
sudo apt update
sudo apt install wazuh-agent -y

## Configure Manager IP
sudo nano /var/ossec/etc/ossec.conf

## Register Agent
sudo /var/ossec/bin/agent-auth -m 192.168.153.138

## Start Agent
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

---

# 4. Lubuntu – Agent Installation

## Install Agent
sudo apt update
sudo apt install wazuh-agent -y

## Configure Manager IP
sudo nano /var/ossec/etc/ossec.conf

## Register Agent
sudo /var/ossec/bin/agent-auth -m 192.168.153.138

## Start Agent
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

---

# 5. Enable SSH on Mint (Victim Setup)

sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl status ssh

---

# 6. Attack Simulation – Kali → Mint

## Basic Port Scan
nmap 192.168.153.139

## Advanced Scan
nmap -sS -A 192.168.153.139

## SSH Brute Force Simulation
for i in {1..6}; do ssh fakeuser@192.168.153.139; done

---

# 7. Privilege Escalation Test (Mint)

sudo su

---

# 8. File Integrity Monitoring Test

## Modify System File
echo "intrusion_test" >> /etc/passwd

## Generate Syslog Event
logger intrusion_test

---

# 9. Custom Rule Creation (Wazuh Server)

## Edit Local Rules
sudo nano /var/ossec/etc/rules/local_rules.xml

## Restart Manager
sudo systemctl restart wazuh-manager

---

# 10. Troubleshooting Commands

## View Agent Logs
sudo tail -f /var/ossec/logs/ossec.log

## Check Agent Connectivity
ping 192.168.153.138

## List Registered Agents (Server)
sudo /var/ossec/bin/agent_control -l

---

# Summary

This lab involved:

- Wazuh SIEM deployment
- Multi-agent configuration
- SSH service configuration
- Network scanning and brute-force simulation
- Privilege escalation testing
- File integrity monitoring
- Custom rule implementation
- Alert analysis via dashboard

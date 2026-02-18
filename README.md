# wazuh-soc-lab
Wazuh SIEM deployment with multi-agent monitoring and attack simulation in a Linux-based SOC lab.
Overview

This project demonstrates deployment of Wazuh SIEM in a multi-VM Linux environment including:

Ubuntu Server (Wazuh Manager)

Kali Linux (Attacker + Agent)

Linux Mint (Primary Victim)

Lubuntu (Secondary Endpoint)

Architecture
Component	   Role	                  IP
Ubuntu   Server	Wazuh Manager	192.168.153.138
Kali	   Attacker + Agent	      192.168.153.130
Mint	   Victim + Agent	        192.168.153.139
Lubuntu	    Agent	              192.168.153.141

Deployment Steps:
Wazuh Server Installation
Ubuntu Server setup
Wazuh stack installation
Service verification

Agent Installation:
Repository setup
Agent installation
Manager IP configuration
Agent registration
Service startup

Attack Simulations:
Nmap scanning
SSH brute force attempts
Privilege escalation (sudo)
Authentication monitoring
Detection Results

Wazuh successfully detected:
SSH login failures (Rule 5710)
PAM login failures (Rule 5503)
Successful sudo execution (Rule 5402)
MITRE ATT&CK mappings:
  Credential Access
  Lateral Movement
  Privilege Escalation

Skills Demonstrated:
SIEM deployment
Log analysis
MITRE ATT&CK mapping
Threat detection
Multi-host monitoring
Linux system administration

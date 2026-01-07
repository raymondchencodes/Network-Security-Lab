# Network Security Lab

## Overview
This project demonstrates a virtualized network security lab designed to simulate real-world firewall configuration, traffic control, and security monitoring. The goal is to understand how firewalls enforce policy, log traffic, and mitigate common network threats.

## Network Architecture
- Windows host system running VirtualBox
- Firewall VM acting as the network gateway
- Victim VM located on the internal network
- Attacker VM used to simulate malicious activity
- Segmented WAN and LAN networks with all traffic routed through the firewall

## Firewall Configuration
The firewall was configured using a default-deny mindset with explicitly defined rules:
- Baseline rule allowing outbound LAN traffic
- ICMP traffic blocked to restrict network probing
- Outbound SSH traffic blocked and logged to prevent unauthorized remote access

## Validation
Firewall rules were validated through controlled testing:
- ICMP traffic successfully blocked after rule deployment
- SSH connection attempts denied and recorded in firewall logs
- Allowed traffic continues to function as expected

## Current Status
- Firewall configuration complete
- Traffic validation complete
- Logging confirmed

## Next Steps
- Capture and analyze traffic using packet inspection tools
- Establish a baseline of normal network behavior
- Deploy an intrusion detection system
- Perform controlled scanning and attack simulations

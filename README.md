# Network Security Lab

## Overview
This project demonstrates a virtualized network security lab designed to simulate real-world firewall configuration, traffic control, and security monitoring. The goal is to understand how firewalls enforce policy, log traffic, and mitigate common network threats.

## Network Architecture
- Windows 10 host system running VirtualBox
- pfSense firewall VM acting as the gateway between networks
- Victim VM located on the internal LAN
- Attacker VM (Kali Linux) used to generate controlled attack traffic
- Segmented WAN and LAN networks with all traffic routed through pfSense

## Firewall Configuration
The firewall was configured using a default-deny mindset with explicitly defined rules:
- Baseline rule allowing normal outbound LAN traffic
- ICMP traffic blocked to restrict network probing
- Outbound SSH traffic blocked and logged to prevent unauthorized remote access

## Traffic Analysis and Validation
Firewall rules were validated through controlled testing and packet capture:
- TCP SYN scans were generated from the attacker VM using Nmap
- SYN packets were captured on the pfSense WAN interface
- No SYN-ACK responses were observed, confirming that the traffic was blocked by the firewall rules applied 

Captured traffic was analyzed in Wireshark to distinguish baseline traffic (ARP, normal TCP behavior) from abnormal traffic (repeated SYN packets)

## Findings
- pfSense Firewall rules successfully intercepted and blocked unauthorized connection attempts
- Packet captures confirmed that malicious scanning traffic reached the firewall but was not forwarded to the internal host

## Next Steps
- Deploy an intrusion detection system
- Perform controlled scanning and attack simulations

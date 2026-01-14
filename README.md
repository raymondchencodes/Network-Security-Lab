# Network Security Lab

## Overview
This project demonstrates a virtualized network security lab designed to simulate real-world firewall configuration, traffic control, and security monitoring. The goal is to understand how firewalls enforce policy, log traffic, and mitigate common network threats through testing and analysis of real network traffic.

## Network Architecture
- Windows 10 host system running VirtualBox
- pfSense firewall VM acting as the gateway between networks
- Suricata IDS enabled on pfSense to monitor network traffic
- Victim VM (Metasploitable) located on the internal LAN
- Attacker VM (Kali Linux) used to generate controlled attack traffic
- Segmented WAN and LAN networks with all traffic routed through pfSense

This architecture enforces clear trust boundaries between internal and external networks, allowing security controls to be tested in isolation. 

## Firewall Configuration
The firewall was configured using a default-deny mindset with explicitly defined rules:
- Baseline rule allowing normal outbound LAN traffic
- ICMP traffic blocked to restrict network probing
- Outbound SSH traffic blocked and logged to prevent unauthorized remote access

## Traffic Analysis and Validation
Firewall rules were validated through controlled testing and packet capture:
- Three scans were executed from the Kali Attacker VM against the victim VM to evaluate exposed services and defensive responses
- Traffic was captured on the pfSense WAN interface to observe how scanning activity was handled
- Packet captures confirmed that scanning traffic reached the firewall but was not forwarded to the internal host
- Captured traffic was analyzed in Wireshark to distinguish baseline traffic (ARP, normal TCP behavior) from abnormal activity (repeated TCP SYN packets)

## Intrustion Detection System (IDS) Deployment and Monitoring
Suricata was deployed on the pfSense firewall to monitor traffic traversing the network boundary. Suricata was configured using the Emerging Threats Open (ET Open) rule set to inspect network traffic and generate alerts for suspicious or malicious patterns, providing detection capabilities beyond basic firewall packet filtering.

## IDS Detection Tests
To evaluate the effectiveness of Suricata in this environment, two targeted detection scenarios were executed:

1) Scan Detection Test
- A network scanning test was performed to simulate reconnaissance activity from the attacker VM. IDS monitoring was used to evaluate whether scanning behavior would be visible if traffic reached the detection layer.
2) Service Attack Pattern Test
- A service-focused attack pattern was generated to simulate attempts to interact with or abuse a network service. IDS visibility and firewall behavior were reviewed to assess how layered defenses handled application-level attack patterns.

## Key Findings
- Configured firewall rules successfully intercepted and blocked unauthorized connection attempts
- Packet captures confirmed that malicious scanning traffic reached the firewall but did not reach the internal host
- No IDS alerts were generated because traffic was blocked by the firewall before reaching IDS inspection

## Tech Stack:
- VirtualBox
- pfSense
- Kali Linux
- Metasploitable
- Wireshark
- Suricata

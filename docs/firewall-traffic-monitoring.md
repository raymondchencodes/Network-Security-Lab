# Firewall and Traffic Analysis

## Objective
The objective of this analysis is to evaluate firewall rule enforcement by observing how unauthorized traffic was handled at the firewall layer.

## Tests
Traffic was generated from the Kali Linux attacker VM targeting the internal victim host (Metasploitable). The following tests were performed:
1) TCP SYN scan targeting port 80 - tests whether HTTP-related traffic was permitted through the firewall:
   
   `sudo nmap -sS -p 80 192.168.56.194`
   
2) ICMP echo requests - tests basic network reachability:

   `ping 192.168.56.194`
   
3) SSH connection attempts targeting port 22 - tests whether remote access to the internal host was allowed:

   `sudo nmap -p 22 192.168.56.194`

## Observations
1) Packet captures taken on the pfSense WAN interface showed repeated TCP SYN packets originating from the attacker IP and destined for the internal host. No SYN-ACK responses were observed. This behavior confirms that the firewall intercepted and blocked the connection attempts at the firewall, preventing the scan traffic from reaching the internal network. 

<p align="center">
<img width="650" height="375" alt="image" src="https://github.com/user-attachments/assets/34db62d7-a821-49e2-be22-0654473fb500" />
</p>

2) ICMP echo requests were sent from the attacker VM to the internal host to test network reachability. Packet captures showed ICMP echo request packets arriving at the pfSense WAN interface with no corresponding echo replies. This behavior confirms that ICMP traffic was blocked by the configured firewall rule.

<p align="center">
<img width="650" height="375" alt="image" src="https://github.com/user-attachments/assets/ee7d8c3e-38dc-49f7-bedf-a151e04f9434" />
</p>

3) An SSH connection attempt was simulated by probing port 22 from the attacker VM. Scanning results showed that the host was unreachable and no SSH service was accessible. This behavior is consistent with firewall rules blocking SSH traffic and preventing connection attempts from reaching the internal host.

<p align="center">
<img width="1136" height="282" alt="image" src="https://github.com/user-attachments/assets/c05b16cb-8174-44f6-baff-9bc45d18e7d7" />
</p>

## Summary
The results confirmed that the firewall rules were enforced as intended, preventing unauthorized scanning and connection attempts from being forwarded to the internal host. Packet captures provide evidence of effective network segmentation and traffic control at the firewall stage. 

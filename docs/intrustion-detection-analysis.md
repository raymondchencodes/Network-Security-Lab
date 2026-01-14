# Suricata IDS Analysis

## Objective
The objective of this analysis is to evaluate the behavior of the intrusion detection system (Suricata) when malicious traffic is generated against the network and determine whether such activity reaches the IDS for inspection.

## Tests
Traffic was generated from the Kali Linux attacker VM targeting the internal victim host (Metasploitable). The following tests were performed:
1) Scan Detection Test - a TCP SYN scan was executed using Nmap to simulate reconnaissance activity:

   `sudo nmap -sS -Pn --reason --max-retries 1 --min-rate 500 -p 1-1000 192.168.56.104`

2) Service Attack Pattern Test - service-level requests were attempted using to simulate interaction with internal services:

   `curl http://192.168.56.104`

## Observations
1) All 1,000 scanned ports were reported as filtered with no responses received. This indicates that SYN packets reached the firewall but were dropped before reaching the internal host. Because the traffic was blocked at the firewall, Suricata did not observe the scan and no IDS alerts were generated.

<p align="center">
<img width="743" height="271" alt="image" src="https://github.com/user-attachments/assets/31419bc4-d440-40e9-8e82-e636006fd319" />
</p>

2) Service-level requests did not appear in LAN packet captures, and no HTTP traffic reached the internal host. The Suricata Alerts dashboard showed no entries associated with this activity, confirming that the firewall blocked the requests before they could be inspected by the IDS.

<p align="center">
<img width="671" height="426" alt="image" src="https://github.com/user-attachments/assets/8f679312-0c10-4e32-9fd5-2288e44c223f" />
</p>
   
## Summary
The results confirmed that Suricata was correctly positioned behind the firewall and inspected only traffic that was allowed through. In both tests, malicious traffic was blocked at the firewall and did not reach the IDS, resulting in no alerts. This confirms that firewall rules were enforced as intended and prevented unauthorized traffic from entering the internal network.

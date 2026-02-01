<h1>Exploring-pivoting-with-Dual-NIC-Lab</h1>
A hands-on lab project demonstrating pivoting concepts using a dual-NIC configuration to analyze network segmentation and lateral movement in a controlled environment.

## Disclaimer
This project was conducted strictly in a controlled lab environment for educational purposes only.

## Lab Environment
- Attacker Machine: Kali Linux
- Target Machine: Metasploitable2
- Tool: Nmap
- Network Type: Isolated / Host-only Network
  
## Analysis flow
<b>1. Host discovery with Nmap ARP Scan</b>
<br>
The image descibe the results of the ARP-Based host discovery scan performmed by the attacker machine (Kali Linux) on the network 192.168.56.0/24 network. The highlighted IP add corresponds to the Metasploitable2 host Confirmed with its MAC address

<b>2. Network interface enumeration with on a dual-homed host</b><br>
The screenshot show the network interface configuration of the Metasploitable2 machine using the ip a command. The first interface (eth0) is connected to the hpst-only network with IP Add 192.168.56.103/24. Meanwhile, the second interface (eth1) is connected to an internal network and assigned static IP add 10.10.10.5/24.

<b>3. Internal network discovery</b><br>
This screenshot show the the execution of an ARP-based host discovery scan (nmap -sn -PR) againts host 10.10.10.5/24.

<b>4. Internal network scan from attacker perspective</b><br>
The screenshot describe an attempt to perform an ARP-based host discovery scan (nmap -sn -PR) against the internal network segment (10.10.10.0/24) from the attacker machine (Kali Linux). The scan fails with routing errors indicates that the attacker does not have valid route to internal network. This confirms that the internal network is not directly reachable from the attacker’s position and highlights the difference in network visibility between the attacker and the dual-homed compromised host.

## Findings
This lab demonstrates that pivoting is possible when a compromised server has direct connectivity to other hosts within the local network, even if the attacker machine does not. Once the initial server is compromised, it can be used as a pivot point to access internal systems, enabling lateral movement across the network.

## Mitigation
To mitigate this risk, internal network segmentation should be properly enforced, and servers should only be allowed to communicate with necessary systems. Applying strict firewall rules, limiting trust relationships between internal hosts, and monitoring internal traffic can reduce the impact of pivoting and lateral movement if a server is compromised.

5 –      IPSG Attacks
5.1.   Introduction
IP Source Guard (IPSG) is a defense mechanism that is designed to prevent IP spoofing attacks. For instance, when someone wants to spoof the address of another host, this feature will prevent this spoofing because this IP address is not assigned by DHCP. IPSG works by relying on DHCP snooping and IP source bindings to match the IP address on untrusted Layer 2 networks.   

5.2.   Topology

5.3.   IP Attacks:
5.3.1.           IP Spoofing
IP spoofing is an attack performed to achieve one of two goals: a DOS (Denial of Services) or unauthorized access to a network. We perform this attack by using Scapy. As shown below we build an IP header with a spoofed IP address and the destination of our target IP address.


Scapy Configuration
Also it worth noting that in my topology the actual IP address of our Kali is 10.150.100.12, the reason this is working is there is no validation that maps the IP address to the mac address of the host that is sending the spoofed IP as we will see, this is how the mitigation works.  Now if we look at Wireshark capture below, we see that the ICMP packet was sent to the target and the replay came back to the spoofed IP address.


Wireshark IP spoofing ﻿
5.3.2.           IP Source Guard Mitigation
This mitigation relies on the DHCP database so we need to make sure we enable that as we discussed in previous mitigations. After this we include the IP source guard configuration to the switch as show below


IP Source Guard
Now if we try to spoof an IP from scapy on Kali, the victim should not successfully respond back to that packet.  If we take a look at the DHCP snooping database it show that the Kali mac address is associated with that IP address, and if tried to send a packet with different IP address other than that IP it should just get dropped.
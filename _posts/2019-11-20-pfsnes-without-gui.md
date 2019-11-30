---
layout: post
title:  "PfSense without GUI"
categories: Network_Security
---
# **Introduction**
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;"> 
PfSense is FreeBsd based.</span>


# **Topology**
<img src="https://raw.githubusercontent.com/t1g3rpwn/layer0/gh-pages/_posts/img/ARP/Arp_Topology.png"/>

#   **ARP Attacks**:

###  **ARP Spoofing**
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;"> 
Using the 
</span>


## **Dynamic ARP Inspection Mitigation**
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;"> When we want to avoid invalid and malicious ARP packets, we can use Dynamic ARP Inspection (DAI). This feature work similarly to DHCP snooping, in that if a client sends a message that is recognized as malicious it will drop these illegitimate packets. We start the switch configuration by applying DAI on the switch in </span>




# **Conclusoin**
<span style="color: #f2cf4a; font-family: Babas; font-size: 0.9em;"> 
TODO
</span>

# **References**

[Man Page FreeBSD firewall](https://www.freebsd.org/doc/handbook/firewalls.html)

[ARP Spoofing](https://networklessons.com/cisco/ccnp-switch/vlan-hopping/)




* Notes
  * FreeBSD has three firewalls built into the base system: 
  * PF
    * packet filter
    * Enabling PF
      * adding pf_enable=yes to /etc/rc.conf
        * sysrc pf_enable=yes
        * pf_flags=""                     # additional flags for pfctl startup
      * reeBSD does not ship with a ruleset and there is no /etc/pf.conf. Example rulesets can be found in /usr/share/examples/pf/.
      * add a line to /etc/rc.conf
        * pf_rules="/path/to/pf.conf"
      * To enable logging support, add pflog_enable=yes to /etc/rc.conf:
        *  sysrc pflog_enable=yes
     *  
  
  * IPFW, and IPFILTER, also known as IPF.
  * To lookup unknown port numbers, refer to /etc/services. Alternatively, visit http://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers and do a port number lookup to find the purpose of a particular port number.
  * A firewall ruleset can be either “exclusive” or “inclusive”. 
    * An exclusive firewall allows all traffic through except for the traffic matching the ruleset. 
    * An inclusive firewall does the reverse as it only allows traffic matching the rules through and blocks everything else.
    *  Inclusive firewalls are generally safer than exclusive firewalls because they significantly reduce the risk of allowing unwanted traffic.
    *  
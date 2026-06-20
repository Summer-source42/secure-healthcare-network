# 09 - Interview Talking Points

## 30-Second Project Pitch

I designed and implemented a secure healthcare enterprise network in Cisco Packet Tracer. The network includes segmented LAN, WLAN, Voice, and DMZ zones; redundant multilayer switches using HSRP; EtherChannel for resilient inter-switch links; OSPF routing; Cisco ASA firewall policies; NAT; centralized DHCP/DNS; WLC-managed wireless; and VoIP services. I also documented verification commands, test cases, security controls, and troubleshooting steps to show that the design works operationally, not just visually.

## 2-Minute Technical Explanation

The network uses a hierarchical design with a firewall at the perimeter, an enterprise edge router, two multilayer switches, and access switches for each department. I separated traffic using VLAN 10 for LAN, VLAN 50 for WLAN, and VLAN 99 for voice. The multilayer switches provide inter-VLAN routing and default gateway redundancy using HSRP. I used LACP EtherChannel between the multilayer switches to increase bandwidth and provide link resiliency. OSPF advertises internal routes between the routing devices and firewall. The ASA firewall separates inside, outside, and DMZ networks, applies NAT for internet access, and uses ACLs to control traffic between zones. DHCP and DNS are centralized in the server farm, while wireless access is managed through a WLC and lightweight APs. I validated the design with show commands, DHCP testing, ping/traceroute, ACL counters, NAT translation checks, HSRP failover, and wireless/VoIP tests.

## Questions You May Be Asked

### Why did you use VLANs?

To separate traffic types, reduce broadcast scope, improve performance, and apply security policy per segment.

### Why did you use HSRP?

To provide a virtual default gateway so users can continue communicating if one multilayer switch fails.

### Why use a DMZ?

To isolate servers from both internal clients and the outside network, allowing firewall rules to control exact access.

### What would you improve in production?

I would add AAA with TACACS+/RADIUS, dedicated management VLAN, SNMPv3, syslog/SIEM, NetFlow, DHCP Snooping, Dynamic ARP Inspection, IP Source Guard, guest isolation, and stricter least-privilege firewall rules.

### How did you verify the project?

I used commands like `show vlan brief`, `show interfaces trunk`, `show etherchannel summary`, `show standby brief`, `show ip ospf neighbor`, `show ip route`, `show access-list`, `show nat`, and client connectivity tests.

### What was the hardest part?

The hardest part was making security and redundancy work together: VLAN segmentation, HSRP, OSPF, NAT, and ACLs all had to align for traffic to flow correctly while still being controlled by security policy.

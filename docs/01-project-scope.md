# 01 Project Scope

## Objective

Design and implement a secure enterprise network for a healthcare organization with multiple departments, floors, user groups, internal services, wireless access, VoIP, DMZ resources, ISP access, and cloud connectivity.

## Business Requirements

- Support multiple departments across several office floors.
- Separate wired users, wireless users, voice traffic, and server resources.
- Provide secure internet access through an enterprise firewall.
- Provide controlled access to DMZ hosted services.
- Support centralized DHCP and DNS services.
- Provide wireless access for employees, corporate users, auditors, and guests.
- Provide VoIP services for department communication.
- Support high availability and future growth.


## Technical Requirements

- Cisco Packet Tracer 
- Cisco ASA firewall
- Multilayer switching
- Access switching
- VLANs and trunks
- HSRP redundancy
- LACP EtherChannel
- OSPF routing
- DHCP relay
- DNS/DHCP server in server farm
- WLC and lightweight APs
- Voice VLAN and VoIP router
- SSH management access restricted by ACL
- Static IPs for infrastructure and DMZ servers
- NAT/PAT for internet access
- Testing and validation documentation

## Scope

These items are included

- Real SIEM integration
- Real TACACS+/RADIUS AAA server integration
- Production IDS/IPS
- Real AWS VPN or Direct Connect
- Real VMware ESXi deployment
- Real endpoint EDR/antivirus
- Real healthcare compliance audit

## Success Criteria

The project is considered complete when:

- VLANs are created and assigned correctly.
- LAN, WLAN, and Voice segments use separate addressing.
- Inter-VLAN routing works through multilayer switches.
- HSRP virtual gateways are operational.
- EtherChannel forms successfully.
- OSPF neighbors form and routes are learned.
- Internal users receive DHCP addresses.
- DMZ servers use static IP addresses.
- Firewall zones, NAT, and ACLs are applied.
- Wireless clients can connect through WLC-managed APs.
- IP phones register and can call each other.
- Verification evidence is captured and documented.

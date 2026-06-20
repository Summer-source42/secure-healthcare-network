# Presentation Outline

## Slide 1 - Title

**Secure Healthcare Enterprise Network Design**

Subtitle: Enterprise network engineering portfolio project using Cisco Packet Tracer

## Slide 2 - Business Problem

- Healthcare company with multiple departments and floors
- Needs secure access to internal services, internet, wireless, voice, and cloud resources
- Sensitive data requires segmentation, firewall control, and high availability

## Slide 3 - Network Architecture

- Hierarchical design
- ASA firewall at perimeter
- Redundant multilayer switches
- Access switches per department
- DMZ server farm
- WLC/AP wireless design
- VoIP gateway

## Slide 4 - Segmentation and IP Plan

- VLAN 10: LAN
- VLAN 50: WLAN
- VLAN 99: Voice
- DMZ subnet for servers
- Transit/public subnets for routing and firewall links

## Slide 5 - Redundancy and Routing

- HSRP for default gateway redundancy
- LACP EtherChannel between multilayer switches
- OSPF dynamic routing
- Static/default route to ISP

## Slide 6 - Security Controls

- ASA zones: inside, DMZ, outside
- NAT/PAT
- ACL traffic filtering
- SSH restricted to admin PC
- PortFast/BPDU Guard
- Recommended hardening: DHCP Snooping, DAI, SNMPv3, syslog, AAA

## Slide 7 - Validation Evidence

Show screenshots:

- HSRP active/standby
- OSPF neighbor
- EtherChannel summary
- DHCP client address
- ASA NAT/ACL
- Wireless client
- VoIP call

## Slide 8 - Troubleshooting and Lessons Learned

- DHCP relay issue
- HSRP priority/preempt issue
- NAT/ACL issue
- What I would improve in production

## Slide 9 - Closing

- Skills demonstrated
- Business value
- Security and availability improvements
- GitHub repository link

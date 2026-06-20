# Secure Healthcare Enterprise Network 

![Status](https://img.shields.io/badge/status-portfolio%20ready-brightgreen)
![Platform](https://img.shields.io/badge/platform-Cisco%20Packet%20Tracer-blue)
![Focus](https://img.shields.io/badge/focus-enterprise%20networking%20%7C%20security%20%7C%20high%20availability-orange)
![Role](https://img.shields.io/badge/role-network%20engineer-informational)

## Executive Overview

This repository documents a realistic enterprise network design for a multi-floor healthcare services organization. The environment supports clinical departments, reception and guest access, doctors and consultancy teams, procurement, HR, finance, internal audit, corporate users, IT operations, wireless users, VoIP phones, internal servers, DMZ services, ISP connectivity, and simulated cloud connectivity.

The design focuses on the responsibilities expected from a Network Engineer: building a scalable topology, segmenting users and services, protecting traffic with a firewall and access controls, providing routing and gateway redundancy, supporting centralized DHCP/DNS, enabling wireless and voice services, and validating the implementation with operational commands.


## At a Glance

| Item | Summary |
|---|---|
| Organization type | Healthcare diagnostics and services provider |
| Environment | Multi-floor enterprise campus with clinical, business, guest, IT, server, wireless, voice, and cloud-facing segments |
| Primary goal | Build a secure, scalable, redundant network that supports business operations and protects sensitive healthcare services |
| Engineering role demonstrated | Network design, switching, routing, firewall policy, wireless, voice, documentation, validation, and troubleshooting |
| Main platform | Cisco Packet Tracer |
| Key controls | VLAN segmentation, Cisco ASA zones, ACLs, NAT/PAT, OSPF, HSRP, EtherChannel, SSH-restricted management, DMZ isolation |

## Architecture and Lab Files

| Asset | Link | 
|---|---|
| Full topology diagram | [View topology diagram](assets/topology/packet-tracer-full-topology.png) |
|  File | [Download Packet Tracer lab](packet-tracer/secure-healthcare-enterprise-network.pkt) | 
| Architecture reference | [View architecture reference](assets/topology/healthcare-enterprise-architecture.svg) |

Topology

![Secure Healthcare Enterprise Network Topology](assets/topology/packet-tracer-full-topology.png)


## Business Requirements

The organization requires a secure and scalable network across multiple floors and departments. The design must support wired access, wireless access, VoIP, internal application servers, DMZ-hosted services, centralized DHCP/DNS, secure internet access, and cloud resource reachability.

Key design requirements:

| Requirement | Design Response |
|---|---|
| Multi-floor department support | Access-layer switches grouped by department/floor |
| Secure segmentation | Separate LAN, WLAN, Voice, and DMZ networks |
| High availability | HSRP gateway redundancy and LACP EtherChannel |
| Internal routing | Inter-VLAN routing using multilayer switch SVIs |
| Dynamic routing | OSPF between firewall, routers, and multilayer switches |
| Internet and cloud access | ISP edge and AWS cloud simulation |
| Server protection | DMZ zone behind Cisco ASA firewall |
| Centralized services | DHCP, DNS, directory, email, file, and healthcare information system servers |
| Wireless access | WLC-managed access points and SSID segmentation concept |
| Voice support | Voice VLAN and VoIP router/CME concept |
| Secure administration | SSH management restricted to an authorized admin workstation |

## Network Scope

| Area | Scope |
|---|---|
| Users | Wired employees, wireless employees, guests, auditors, corporate users |
| Departments | Pharmacy, medical labs, reception, doctors, consultancy, procurement, HR, finance, audit, corporate, IT |
| Infrastructure | ASA firewall, enterprise edge router, multilayer switches, access switches, WLC, APs, VoIP router |
| Services | DHCP, DNS, directory services, email, file storage, healthcare information system |
| External connectivity | ISP/internet simulation and AWS cloud simulation |
| Security zones | Inside, outside, DMZ, LAN, WLAN, Voice |

## VLAN and Segmentation Plan

| VLAN | Name | Purpose | Example Gateway Role |
|---:|---|---|---|
| 10 | LAN | Wired users and printers | HSRP virtual gateway on multilayer switches |
| 50 | WLAN | Access points and wireless users | HSRP virtual gateway on multilayer switches |
| 99 | Voice | Cisco IP phones and VoIP services | HSRP virtual gateway on multilayer switches |
| DMZ | Server zone | Public-facing/internal shared services | Cisco ASA DMZ interface |

Segmentation is used to reduce broadcast domains, separate user groups, isolate voice traffic, control wireless access, and protect server resources through firewall policy.

## Technologies Implemented

| Category | Technologies / Controls |
|---|---|
| Switching | VLANs, trunks, access ports, PortFast, BPDU Guard, LACP EtherChannel |
| Routing | SVIs, inter-VLAN routing, OSPF, static/default routes |
| High Availability | HSRP gateway redundancy, redundant uplinks, server failover concept |
| Firewall Security | Cisco ASA interfaces, security levels, inside/outside/DMZ zones, ACLs, NAT/PAT |
| Wireless | Wireless LAN Controller, lightweight APs, employee/guest/corporate SSID design concept |
| Voice | Voice VLAN, IP phones, VoIP router/CME concept |
| Services | DHCP, DNS, directory services, email, file, healthcare information system |
| Administration | SSH access control, management workstation restriction, encrypted passwords |
| Operations | Verification commands, connectivity matrix, troubleshooting notes, evidence collection |

## Security Design Summary

The security model uses layered controls rather than relying on a single device.

| Layer | Security Control |
|---|---|
| Perimeter | ASA firewall zones, NAT, ACL based traffic filtering |
| DMZ | Server isolation from internal users and internet facing traffic |
| Access layer | VLAN separation, PortFast, BPDU Guard, unused port shutdown checklist |
| Management plane | SSH only administration from an authorized security engineer workstation |
| Wireless | SSID separation for employees, corporate users, auditors, and guests |
| Voice | Dedicated voice VLAN for IP phones |
| Routing | OSPF route advertisement with controlled edge/default routing |
| Availability | HSRP and EtherChannel to reduce single points of failure |

Recommended hardening items included in the documentation:

- Disable unused switch ports
- Disable DTP on access ports
- Restrict allowed VLANs on trunks
- Use a non-default native VLAN
- Apply DHCP snooping, Dynamic ARP Inspection, and IP Source Guard where supported
- Prefer SNMPv3, NTP, syslog, AAA/TACACS+/RADIUS in production environments
- Use least-privilege firewall rules instead of broad permit statements

## IP Addressing and Documentation

The detailed addressing plan is documented in [`docs/03-ip-addressing-plan.md`](docs/03-ip-addressing-plan.md)

Summary:

| Network Area | Purpose |
|---|---|
| LAN subnet | Wired users and printers |
| WLAN subnet | Wireless users and AP-related access |
| Voice subnet | IP phones and telephony services |
| DMZ subnet | Internal servers and shared services |
| Point-to-point subnets | Firewall, router, ISP, cloud, and multilayer switch links |

## Repository Structure

```text
secure-healthcare-network-portfolio/
├── README.md
├── docs/
│   ├── 01-project-scope.md
│   ├── 02-network-design.md
│   ├── 03-ip-addressing-plan.md
│   ├── 04-security-design.md
│   ├── 05-validation-and-testing.md
│   ├── 06-troubleshooting.md
├── configs/
│   ├── switches/
│   ├── routers/
│   ├── firewall/
│   └── wireless/
├── evidence/
│   ├── command-outputs/
│   └── test-results/
├── assets/
│   ├── topology/
│   └── screenshots/
└── packet-tracer/
    └── secure-healthcare-enterprise-network.pkt

```


## Verification 


| Evidence | Links |
|---|---|
| Cisco Packet Tracer lab file | `packet-tracer/secure-healthcare-enterprise-network.pkt` |
| Full Packet Tracer topology screenshot | `assets/topology/packet-tracer-full-topology.png` |
| VLAN verification | `evidence/command-outputs/show-vlan-brief.txt` |
| Trunk verification | `evidence/command-outputs/show-interfaces-trunk.txt` |
| EtherChannel verification | `evidence/command-outputs/show-etherchannel-summary.txt` |
| HSRP verification | `evidence/command-outputs/show-standby-brief.txt` |
| OSPF neighbor verification | `evidence/command-outputs/show-ip-ospf-neighbor.txt` |
| Routing table verification | `evidence/command-outputs/show-ip-route.txt` |
| ASA ACL verification | `evidence/command-outputs/asa-show-access-lists.txt` |
| ASA NAT verification | `evidence/command-outputs/asa-show-nat.txt` |
| DHCP client screenshot | `assets/screenshots/dhcp-client-success.png` |
| Inter-VLAN ping test | `assets/screenshots/inter-vlan-connectivity.png` |
| DMZ access test | `assets/screenshots/dmz-access-test.png` |
| Wireless client association | `assets/screenshots/wireless-client-associated.png` |
| VoIP call test | `assets/screenshots/voip-call-success.png` |
| HSRP failover test | `assets/screenshots/hsrp-failover-test.png` |

## Core Verification Commands

```bash
show vlan brief
show interfaces trunk
show etherchannel summary
show standby brief
show ip interface brief
show ip route
show ip ospf neighbor
show running-config
```

Cisco ASA verification:

```bash
show interface ip brief
show route
show access-lists
show nat
show xlate
show running-config
```

## Implementation Outcome

The final design demonstrates the ability to:

- Translate business requirements into a scalable enterprise network design
- Build a segmented network using VLANs and routed SVIs
- Implement redundant gateway services using HSRP
- Use EtherChannel to improve uplink resiliency and bandwidth
- Advertise internal and edge routes using OSPF
- Protect internal and DMZ resources with Cisco ASA firewall policies
- Provide centralized IP services using DHCP/DNS
- Support wireless access through a WLC-managed architecture
- Support enterprise voice services using a dedicated voice VLAN
- Validate network behavior using real operational commands and test cases

## Limitations


Production improvements would include:

- 802.1X authentication with RADIUS
- TACACS+/AAA for device administration
- SNMPv3, centralized syslog, and NetFlow
- Real IDS/IPS or next-generation firewall inspection
- Stronger wireless security with WPA2/WPA3-Enterprise
- Automated configuration backup
- Formal change control and rollback plan


## License

This repository is provided for educational and portfolio demonstration purposes.

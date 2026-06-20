# 03 IP Addressing Plan

> Note: Adjust this table if your final Packet Tracer topology uses different masks or device IP addresses. The plan below is written to match the project design and the values visible in the implementation transcript where available.

## VLAN Summary

| VLAN ID | Name | Purpose | Example Subnet | Gateway / HSRP VIP |
|---:|---|---|---|---|
| 10 | LAN | Wired users and printers | 10.10.0.0/16 or lab-defined LAN subnet | 10.10.0.1 |
| 50 | WLAN | Wireless users and AP management | 192.168.0.0/20 | 192.168.0.1 |
| 99 | VOICE | IP phones | 172.16.0.0/20 | 172.16.0.1 |
| N/A | DMZ | Server farm | 10.20.10.0/26 | 10.20.10.1 |
| N/A | Transit | Firewall/router/switch links | 10.30.10.0/30 blocks | Per link |
| N/A | Outside | ISP/public link | 197.200.100.0/30 | ISP/firewall link |

## Infrastructure Addressing

| Device / Interface | Example IP | Notes |
|---|---:|---|
| ASA Inside | 10.30.10.1/30 | Toward enterprise edge/core routing domain |
| ASA DMZ | 10.20.10.1/26 | Default gateway for DMZ servers |
| ASA Outside | 197.200.100.2/30 | Toward ISP |
| ISP Router | 197.200.100.1/30 | ISP-facing next hop |
| Primary Server / DHCP-DNS | 10.20.10.10/26 | Central services |
| WLC Management | 10.10.0.50 | Wireless controller management |
| MLS1 VLAN 10 SVI | 10.10.0.3/16 | HSRP active example |
| MLS2 VLAN 10 SVI | 10.10.0.2/16 | HSRP standby example |
| VLAN 10 HSRP VIP | 10.10.0.1 | Client default gateway |
| VLAN 50 HSRP VIP | 192.168.0.1 | WLAN default gateway |
| VLAN 99 HSRP VIP | 172.16.0.1 | Voice default gateway / or voice router gateway depending final design |

## DHCP Pools

| Pool | Scope | Gateway | DNS | Notes |
|---|---|---|---|---|
| LAN_POOL | LAN subnet | VLAN 10 VIP | 10.20.10.10 | Wired clients and printers |
| WLAN_POOL | WLAN subnet | VLAN 50 VIP | 10.20.10.10 | Wireless clients |
| VOICE_POOL | Voice subnet | Voice gateway / VLAN 99 VIP | 10.20.10.10 | IP phones; may be served by VoIP router in Packet Tracer |

## Static Addressing

Use static addresses for:

- ASA interfaces
- Edge router interfaces
- Multilayer switch routed links and SVIs
- WLC management interface
- DMZ servers
- Directory/DNS/DHCP servers
- Storage devices
- Cloud simulation resources

## IP Planning Notes for Hiring Manager Discussion

- User subnets are sized for current users and future growth.
- Infrastructure links use small point-to-point subnets to conserve address space.
- Server and management IPs are static to support predictable firewall rules, monitoring, and troubleshooting.
- DHCP relay is used on SVIs so centralized DHCP can serve multiple VLANs.

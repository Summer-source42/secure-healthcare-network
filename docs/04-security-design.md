# 04 - Security Design

## Security Objectives

The design is built around the CIA model:

- **Confidentiality:** Separate sensitive systems from general users and guests.
- **Integrity:** Restrict who can manage infrastructure devices and reach servers.
- **Availability:** Use redundancy, failover, and resilient design.

## Network Segmentation

| Zone / Segment | Security Purpose |
|---|---|
| LAN | Normal wired business users |
| WLAN | Wireless users; should be controlled separately from wired users |
| Voice | IP phone traffic separated from data traffic |
| DMZ | Server resources isolated from internal clients and outside users |
| Outside | Untrusted ISP/internet/cloud side |
| Management | Admin-only access to network devices |

## Cisco ASA Firewall Policy

### Firewall Zones

| ASA Zone | Trust Level | Purpose |
|---|---:|---|
| Inside | High | Internal enterprise network |
| DMZ | Medium | Server farm with controlled access |
| Outside | Low | ISP/internet/cloud |

### NAT/PAT

NAT/PAT is used so inside users can access outside networks while hiding internal private IP addresses.

Recommended objects:

```cisco
object network LAN_TO_INTERNET
 subnet <LAN_SUBNET> <MASK>
 nat (inside,outside) dynamic interface

object network WLAN_TO_INTERNET
 subnet <WLAN_SUBNET> <MASK>
 nat (inside,outside) dynamic interface

object network DMZ_TO_INTERNET
 subnet <DMZ_SUBNET> <MASK>
 nat (dmz,outside) dynamic interface
```

### Least-Privilege ACL Design

Avoid broad rules such as `permit ip any any`. Prefer specific policies:

| Source | Destination | Ports | Reason |
|---|---|---|---|
| LAN users | DNS/DHCP server | DNS, DHCP | Name resolution and addressing |
| LAN users | File server | SMB/required app ports | Business file access |
| Doctors/Consultancy | Healthcare system server | HTTPS/app port | Healthcare application access |
| IT admin PC | Network devices | SSH | Device management |
| WLAN guest | Internet only | HTTP/HTTPS/DNS | Guest browsing only |
| Outside | Public DMZ services | HTTPS only | Public-facing service access |
| DMZ servers | Inside | Deny by default | Prevent DMZ-to-inside lateral movement |

## Management Plane Security

Recommended controls:

```cisco
ip domain-name example.local
crypto key generate rsa modulus 2048
ip ssh version 2
username netadmin privilege 15 secret <STRONG_SECRET>

ip access-list standard MGMT_SSH_ONLY
 permit <ADMIN_PC_IP>
 deny any log

line vty 0 4
 login local
 transport input ssh
 access-class MGMT_SSH_ONLY in
```

## Layer 2 Security Hardening

Add these controls to make the project stronger for interviews:

| Control | Purpose |
|---|---|
| Disable unused ports | Reduce attack surface |
| Port security | Limit MAC addresses per access port |
| BPDU Guard | Protect access ports from rogue switches |
| PortFast | Fast convergence for endpoint ports |
| DHCP Snooping | Stop rogue DHCP servers |
| Dynamic ARP Inspection | Reduce ARP spoofing risk |
| IP Source Guard | Prevent IP spoofing on access ports |
| Storm Control | Reduce broadcast/multicast flood impact |
| Disable DTP | Prevent unwanted trunk negotiation |
| Restrict trunk VLANs | Prevent VLAN leakage |
| Change native VLAN | Reduce VLAN hopping risk |

Example access port hardening:

```cisco
interface range fa0/3 - 20
 switchport mode access
 switchport access vlan 10
 switchport voice vlan 99
 spanning-tree portfast
 spanning-tree bpduguard enable
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
 storm-control broadcast level 5.00
```

Example unused port shutdown:

```cisco
interface range fa0/25 - 48
 description UNUSED_PORT_DISABLED
 switchport mode access
 switchport access vlan 999
 shutdown
```

## Wireless Security Recommendations

| SSID | VLAN | Security | Access Policy |
|---|---:|---|---|
| EMPLOYEE | 50 | WPA2/WPA3-Enterprise concept | Internal resources based on role |
| CORPORATE | 50 or dedicated VLAN | WPA2/WPA3-Enterprise concept | Restricted corporate access |
| AUDITOR | Dedicated auditor VLAN recommended | Time-limited credentials | Audit-only systems |
| GUEST | Dedicated guest VLAN recommended | Captive portal / WPA2-PSK in lab | Internet-only |

Packet Tracer may not fully support production WPA3/RADIUS workflows, so document these as production recommendations.

## Logging and Monitoring

Recommended production controls:

```cisco
service timestamps log datetime msec
logging host <SYSLOG_SERVER_IP>
logging trap warnings
ntp server <NTP_SERVER_IP>
snmp-server group NETOPS v3 priv
```

For the portfolio, include screenshots or command outputs showing:

- Successful SSH restriction
- Firewall ACL counters
- NAT translations
- HSRP failover
- OSPF routes
- DHCP assignment
- Wireless client association

## Threat Model

| Threat | Mitigation |
|---|---|
| Unauthorized admin login | SSH-only management, ACL restriction, local user/AAA concept |
| Rogue DHCP server | DHCP snooping |
| Rogue switch connection | BPDU Guard, PortFast on access ports |
| VLAN hopping | Disable DTP, restrict trunk VLANs, change native VLAN |
| Guest lateral movement | Guest SSID/VLAN isolation and firewall ACLs |
| DMZ compromise | Deny DMZ-to-inside by default; allow only required flows |
| Internet exposure | NAT, firewall inspection, least-privilege inbound ACLs |
| Single gateway failure | HSRP |
| Link failure | EtherChannel and redundant uplinks |

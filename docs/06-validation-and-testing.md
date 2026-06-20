# 06 - Validation and Testing

## Required Evidence for GitHub

For a professional portfolio, do not only upload the Packet Tracer file. Add screenshots and command outputs proving that the design works.

## Command Output Checklist

Save command outputs in `evidence/command-outputs/`.

| Test Area | Device | Command | Expected Result |
|---|---|---|---|
| VLANs | Access switch | `show vlan brief` | VLANs 10, 50, 99 present and ports assigned |
| Trunks | Access/Core switches | `show interfaces trunk` | Uplink ports trunking expected VLANs |
| EtherChannel | Multilayer switches | `show etherchannel summary` | Port-channel is bundled/up |
| HSRP | Multilayer switches | `show standby brief` | MLS1 active, MLS2 standby, VIPs visible |
| Routing | Routers/switches | `show ip route` | OSPF and connected routes visible |
| OSPF | Routers/switches | `show ip ospf neighbor` | Neighbors in FULL state |
| DHCP | Client | `ipconfig /all` | Client receives correct IP, gateway, DNS |
| Firewall NAT | ASA | `show xlate` / `show nat` | Dynamic translations appear |
| Firewall ACLs | ASA | `show access-list` | ACL hit counters increase |
| Wireless | WLC/AP/client | WLC client/AP screens | APs joined and clients associated |
| Voice | VoIP router | `show ephone registered` | Phones registered |
| SSH security | Admin PC | SSH test | Admin PC succeeds; other PCs fail |

## Functional Test Matrix

| Test ID | Source | Destination | Expected Result | Status |
|---|---|---|---|---|
| T01 | LAN PC | LAN gateway | Success | Pending screenshot |
| T02 | WLAN client | WLAN gateway | Success | Pending screenshot |
| T03 | LAN PC | DMZ DNS/DHCP server | Success for required services | Pending screenshot |
| T04 | Guest WLAN client | Internal server | Denied | Pending screenshot |
| T05 | LAN PC | Internet/cloud resource | Success through NAT | Pending screenshot |
| T06 | Outside host | Inside client | Denied | Pending screenshot |
| T07 | Outside host | Public DMZ service | Allowed only for approved port | Pending screenshot |
| T08 | IP phone 1 | IP phone 2 | Successful call | Pending screenshot |
| T09 | MLS1 failure simulation | Client default gateway | Traffic continues through MLS2 | Pending screenshot |
| T10 | One EtherChannel link down | Core connectivity | Port-channel remains operational | Pending screenshot |

## Screenshot Checklist

Store screenshots in `assets/screenshots/`.

Recommended screenshot names:

```text
01-full-topology.png
02-vlan-brief-access-switch.png
03-trunk-status.png
04-etherchannel-summary.png
05-hsrp-standby-brief.png
06-ospf-neighbor.png
07-dhcp-client-ipconfig.png
08-asa-nat-translations.png
09-asa-access-list-counters.png
10-wlc-ap-joined.png
11-wireless-client-connected.png
12-voip-phone-call.png
13-ssh-admin-success.png
14-ssh-unauthorized-denied.png
15-hsrp-failover-test.png
```

## Example Evidence Format

Use this format inside each command output file:

```text
Device: MLS1
Command: show standby brief
Purpose: Verify HSRP active/standby gateway redundancy
Expected: MLS1 active for VLAN 10/50/99, MLS2 standby
Result: PASS

<PASTE COMMAND OUTPUT HERE>
```

## Final Acceptance Criteria

The project is ready for GitHub and resume review when:

- Topology screenshot is included.
- VLAN, trunk, EtherChannel, HSRP, OSPF, DHCP, NAT, ACL, wireless, and VoIP evidence is included.
- Failed/denied security tests are documented, not only successful pings.
- Troubleshooting notes explain at least two real issues and fixes.

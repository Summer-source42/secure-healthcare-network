# 05 Validation and Testing


## Command Output Checklist

| Test Area | Device | Command | Results |
|---|---|---|---|
| VLANs | Access switch | `show vlan brief` | VLANs 10, 50, 99 present and ports assigned |
| Trunks | Access/Core switches | `show interfaces trunk` | Uplink ports trunking expected VLANs |
| EtherChannel | Multilayer switches | `show etherchannel summary` | Port-channel is bundled up |
| HSRP | Multilayer switches | `show standby brief` | MLS1 active, MLS2 standby, VIPs visible |
| Routing | Routers/switches | `show ip route` | OSPF and connected routes visible |
| OSPF | Routers/switches | `show ip ospf neighbor` | Neighbors in FULL state |
| DHCP | Client | `ipconfig /all` | Client receives correct IP, gateway, DNS |
| Firewall NAT | ASA | `show xlate` / `show nat` | Dynamic translations appear |
| Firewall ACLs | ASA | `show access-list` | ACL hit counters increase |
| Wireless | WLC/AP/client | WLC client/AP screens | APs joined and clients associated |
| Voice | VoIP router | `show ephone registered` | Phones registered |
| SSH security | Admin PC | SSH test | Admin PC succeeds; other PCs fail |



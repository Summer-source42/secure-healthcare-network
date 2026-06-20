# Connectivity Test Matrix

| Test ID | Source | Destination | Protocol | Expected | Actual | Pass/Fail | Evidence |
|---|---|---|---|---|---|---|---|
| T01 | LAN PC | VLAN 10 Gateway | ICMP | Allowed | Pending | Pending | Screenshot needed |
| T02 | WLAN Client | VLAN 50 Gateway | ICMP | Allowed | Pending | Pending | Screenshot needed |
| T03 | LAN PC | DNS Server | DNS/ICMP | Allowed | Pending | Pending | Screenshot needed |
| T04 | Guest WLAN | Internal Server | ICMP/TCP | Denied | Pending | Pending | Screenshot needed |
| T05 | LAN PC | Cloud Resource | ICMP/HTTP | Allowed through NAT | Pending | Pending | Screenshot needed |
| T06 | Outside Host | Inside Client | Any | Denied | Pending | Pending | Screenshot needed |
| T07 | Outside Host | DMZ Web Service | HTTPS | Allowed | Pending | Pending | Screenshot needed |
| T08 | IP Phone 3001 | IP Phone 3002 | SCCP/Voice | Call successful | Pending | Pending | Screenshot needed |
| T09 | MLS1 Down | LAN Gateway | ICMP | Failover to MLS2 | Pending | Pending | Screenshot needed |
| T10 | EtherChannel Link Down | Core Link | LACP | Port-channel remains up | Pending | Pending | Screenshot needed |

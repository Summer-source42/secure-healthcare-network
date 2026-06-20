# 08 - Limitations and Improvements

## Lab Limitations

Cisco Packet Tracer is useful for demonstrating CCNA-level and some enterprise concepts, but it does not fully simulate every production feature.

| Limitation | How It Is Handled |
|---|---|
| Limited ASA feature support | Use supported NAT/ACL/zone features and document production recommendations |
| Limited AAA/RADIUS/TACACS+ realism | Include design recommendation and placeholder configs |
| Limited enterprise WLC security features | Document WPA2/WPA3-Enterprise and RADIUS as production improvements |
| No real ESXi/NetApp failover | Represent as architecture concept and document expected role |
| No real cloud VPN/Direct Connect | Simulate cloud reachability and document production option |
| Limited logging/SIEM | Include syslog/SNMPv3/NTP recommendations |

## Recommended Improvements

### 1. Dedicated Management VLAN

Add a dedicated management VLAN for switch/router/WLC management instead of managing devices from user networks.

### 2. Separate Guest Wireless VLAN

Create a guest VLAN with internet-only access and deny access to internal subnets.

### 3. AAA Authentication

Use centralized TACACS+ or RADIUS for network device admin login.

### 4. Stronger Firewall Policy

Replace broad ACLs with least-privilege rules by source VLAN, destination IP, and destination port.

### 5. Layer 2 Protection

Add DHCP Snooping, Dynamic ARP Inspection, IP Source Guard, storm control, unused port shutdown, and trunk hardening.

### 6. Monitoring and Logging

Add syslog, SNMPv3, NTP, NetFlow, and alerting documentation.

### 7. Site-to-Cloud Security

For a production design, connect to AWS using site-to-site VPN, private subnets, security groups, and route table controls.

### 8. Documentation Enhancements

Add:

- Network topology screenshot
- IP address plan spreadsheet/table
- Config backups
- Test results
- Troubleshooting notes
- Short presentation deck
- 2-minute demo video

## How to Explain Limitations in an Interview

> Packet Tracer does not fully support every production security control, so I implemented the supported parts and documented the production-grade controls I would add in a real environment, including AAA, SNMPv3, syslog, DHCP Snooping, Dynamic ARP Inspection, guest VLAN isolation, and more specific firewall ACLs.

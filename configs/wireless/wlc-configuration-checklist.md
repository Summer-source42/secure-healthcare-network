# WLC Configuration Checklist

## Management

- [ ] Set WLC system name: `HQ-WLC`
- [ ] Set management IP address
- [ ] Set default gateway
- [ ] Set DNS server
- [ ] Use a lab-only admin password, never a real password

## AP Join

- [ ] Lightweight APs receive IP address
- [ ] APs can reach WLC management IP
- [ ] AP status shows joined/registered

## SSIDs

| SSID | Recommended VLAN | Security | Notes |
|---|---:|---|---|
| EMPLOYEE | 50 | WPA2/WPA3 Enterprise concept | Normal employees |
| CORPORATE | 50 or dedicated VLAN | WPA2/WPA3 Enterprise concept | Corporate users |
| AUDITOR | Dedicated auditor VLAN recommended | Time-limited access | External auditors |
| GUEST | Dedicated guest VLAN recommended | Guest/captive portal concept | Internet-only |

## GitHub Evidence

Add screenshots for:

- WLC management page
- AP joined page
- WLAN/SSID configuration
- Wireless client associated
- Wireless client DHCP address

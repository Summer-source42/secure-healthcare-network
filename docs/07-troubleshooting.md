# 07 - Troubleshooting Documentation

## Issue 1 - Wireless Client Did Not Receive DHCP Address

**Symptom:** Wireless client associated to SSID but received no valid IP address.

**Checks:**

```bash
show vlan brief
show interfaces trunk
show ip interface brief
show running-config interface vlan 50
```

**Root Cause:** VLAN 50 was not allowed on one trunk or DHCP relay was missing on the VLAN 50 SVI.

**Fix:**

```cisco
interface vlan 50
 ip helper-address 10.20.10.10

interface <TRUNK_INTERFACE>
 switchport trunk allowed vlan add 50
```

**Result:** Client received WLAN subnet address and could ping the VLAN 50 gateway.

## Issue 2 - HSRP Did Not Elect Expected Active Switch

**Symptom:** MLS2 became active when MLS1 was expected to be active.

**Checks:**

```bash
show standby brief
show running-config interface vlan 10
show running-config interface vlan 50
show running-config interface vlan 99
```

**Root Cause:** HSRP priority was not configured correctly or `preempt` was missing.

**Fix:**

```cisco
interface vlan 10
 standby 10 priority 150
 standby 10 preempt
```

**Result:** MLS1 became active after HSRP convergence.

## Issue 3 - LAN Users Could Not Access Internet

**Symptom:** LAN clients could ping internal gateways but not outside/cloud resources.

**Checks:**

```bash
show ip route
show ip ospf neighbor
show access-list
show nat
show xlate
packet-tracer input inside icmp <SRC_IP> 8 0 <DST_IP>
```

**Root Cause:** Missing NAT object or missing default route on ASA.

**Fix:**

```cisco
object network LAN_TO_INTERNET
 subnet <LAN_SUBNET> <MASK>
 nat (inside,outside) dynamic interface

route outside 0.0.0.0 0.0.0.0 <ISP_NEXT_HOP>
```

**Result:** ASA created translations and outside pings/web tests succeeded.

## Issue 4 - Unauthorized PC Could SSH to a Switch

**Symptom:** Non-admin client could reach device VTY lines.

**Checks:**

```bash
show running-config | section line vty
show access-lists
```

**Root Cause:** VTY ACL missing or applied in wrong direction.

**Fix:**

```cisco
ip access-list standard MGMT_SSH_ONLY
 permit <ADMIN_PC_IP>
 deny any log

line vty 0 4
 access-class MGMT_SSH_ONLY in
 transport input ssh
```

**Result:** Admin PC can SSH; unauthorized PC is denied.

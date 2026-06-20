# 05 - Implementation Guide

## Phase 1 - Build the Topology

1. Add Cisco ASA firewall.
2. Add enterprise edge router.
3. Add two multilayer switches.
4. Add access switches for departments/floors.
5. Add DMZ/server farm switch and servers.
6. Add WLC and lightweight APs.
7. Add VoIP router and IP phones.
8. Add ISP and cloud simulation routers/resources.
9. Connect devices using redundant uplinks where possible.

## Phase 2 - Basic Device Hardening

Apply to routers and switches:

```cisco
enable
configure terminal
hostname <DEVICE_NAME>
no ip domain-lookup
service password-encryption
banner motd # Unauthorized access is prohibited #
enable secret <STRONG_SECRET>
username netadmin privilege 15 secret <STRONG_SECRET>
ip domain-name healthcare.local
crypto key generate rsa modulus 2048
ip ssh version 2
line console 0
 password <CONSOLE_SECRET>
 login
line vty 0 4
 login local
 transport input ssh
end
write memory
```

## Phase 3 - VLAN Creation

```cisco
vlan 10
 name LAN
vlan 50
 name WLAN
vlan 99
 name VOICE
vlan 999
 name BLACKHOLE_UNUSED
```

## Phase 4 - Access Switch Port Assignment

Example departmental switch:

```cisco
interface range fa0/1 - 2
 description UPLINK_TO_MULTILAYER_SWITCHES
 switchport mode trunk
 switchport trunk allowed vlan 10,50,99
 switchport nonegotiate

interface range fa0/3 - 20
 description WIRED_USER_PORTS
 switchport mode access
 switchport access vlan 10
 switchport voice vlan 99
 spanning-tree portfast
 spanning-tree bpduguard enable

interface range fa0/21 - 24
 description ACCESS_POINT_PORTS
 switchport mode access
 switchport access vlan 50
 spanning-tree portfast
 spanning-tree bpduguard enable
```

## Phase 5 - EtherChannel

On both multilayer switches:

```cisco
interface range gig1/0/21 - 24
 description LACP_TO_PEER_MULTILAYER_SWITCH
 switchport mode trunk
 switchport trunk allowed vlan 10,50,99
 channel-group 1 mode active

interface port-channel 1
 description LACP_PORT_CHANNEL_TO_PEER
 switchport mode trunk
 switchport trunk allowed vlan 10,50,99
```

## Phase 6 - Inter-VLAN Routing and HSRP

Example on MLS1:

```cisco
ip routing

interface vlan 10
 description LAN_GATEWAY
 ip address 10.10.0.3 255.255.0.0
 ip helper-address 10.20.10.10
 standby 10 ip 10.10.0.1
 standby 10 priority 150
 standby 10 preempt

interface vlan 50
 description WLAN_GATEWAY
 ip address 192.168.0.3 255.255.240.0
 ip helper-address 10.20.10.10
 standby 50 ip 192.168.0.1
 standby 50 priority 150
 standby 50 preempt

interface vlan 99
 description VOICE_GATEWAY
 ip address 172.16.0.3 255.255.240.0
 standby 99 ip 172.16.0.1
 standby 99 priority 150
 standby 99 preempt
```

Example on MLS2:

```cisco
ip routing

interface vlan 10
 ip address 10.10.0.2 255.255.0.0
 ip helper-address 10.20.10.10
 standby 10 ip 10.10.0.1
 standby 10 priority 110
 standby 10 preempt

interface vlan 50
 ip address 192.168.0.2 255.255.240.0
 ip helper-address 10.20.10.10
 standby 50 ip 192.168.0.1
 standby 50 priority 110
 standby 50 preempt

interface vlan 99
 ip address 172.16.0.2 255.255.240.0
 standby 99 ip 172.16.0.1
 standby 99 priority 110
 standby 99 preempt
```

## Phase 7 - OSPF Routing

Example:

```cisco
router ospf 25
 router-id <UNIQUE_ROUTER_ID>
 network 10.10.0.0 0.0.255.255 area 0
 network 192.168.0.0 0.0.15.255 area 0
 network 172.16.0.0 0.0.15.255 area 0
 network 10.30.10.0 0.0.0.255 area 0
```

## Phase 8 - ASA Firewall

1. Configure interfaces and security levels.
2. Add static/default route to ISP.
3. Add OSPF where supported.
4. Configure NAT objects.
5. Configure ACLs.
6. Apply ACLs to interfaces.
7. Verify translations and allowed/blocked flows.

## Phase 9 - DHCP/DNS Services

Configure DHCP pools on the server or router according to the lab design.

For centralized server DHCP:

- LAN pool
- WLAN pool
- DNS server IP
- Default gateway = HSRP virtual IP

For voice DHCP in Packet Tracer, use the VoIP router if required by the simulation.

## Phase 10 - Wireless LAN Controller

1. Assign WLC management IP.
2. Configure admin account using a lab-only secret.
3. Create SSIDs.
4. Map SSIDs to VLANs.
5. Join APs to the controller.
6. Connect wireless clients and verify DHCP.

## Phase 11 - VoIP

1. Configure voice VLAN.
2. Configure router subinterface or CME gateway.
3. Configure DHCP option 150 if supported.
4. Register phones.
5. Assign extensions.
6. Test phone-to-phone calls.

## Phase 12 - Validation

Use the validation plan in `docs/06-validation-and-testing.md` and save results under `evidence/`.

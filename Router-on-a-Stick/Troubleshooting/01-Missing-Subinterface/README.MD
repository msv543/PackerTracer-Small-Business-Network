## Problem

A user in the HR department (VLAN 30) reports they cannot communicate with devices in other VLANs or reach their default gateway. Users in the Sales, IT and Management VLANs continue to have normal network connectivity.

## Symptoms

- PC3 cannot ping its default gateway (192.168.30.1).
- PC3 cannot communicate with devices in VLAN 10 or VLAN 20.
- PC3 cannot reach the simulated ISP router.
- DHCP may still function if the lease was already obtained, but inter-VLAN routing fails.
- Users in VLANs 10, 20 and 99 are unaffected.

## Investigation

The issue appeared to affect only VLAN 30, indicating the switch trunk and other VLANs were operating correctly.

1. Verified PC3's IP configuration.
2. Confirmed the switch port was assigned to VLAN 30.
3. Verified the trunk link was operational.
4. Examined the router's interfaces.
5. Discovered that the VLAN 30 router subinterface was missing.

## Commands Used
- On PC3
```
ipconfig
ping 192.168.30.1
ping 192.168.10.10
```
- On Switch
```
show vlan brief
show interfaces trunk
```
- On Router
```
show ip interface brief
show running-config
show ip route
```

## Root Cause

The router subinterface responsible for VLAN 30 had been removed. Since Router-on-a-Stick uses router subinterfaces as the default gateways for each VLAN, devices in VLAN 30 had no Layer 3 gateway and could not communicate outside their local network.

## Resolution

Recreated the VLAN 30 subinterface.
```
interface GigabitEthernet 0/1.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
no shutdown
```

## Verification

After restoring the router subinterface:
- PC3 successfully pinged its default gateway.
- PC3 successfully communicated with devices in VLAN 10, VLAN 20, and VLAN 99.
- PC3 successfully reached the simulated ISP router.
- show ip interface brief confirmed that GigabitEthernet 0/1.30 was operational.
- show ip route displayed the connected route for 192.168.30.0/24.

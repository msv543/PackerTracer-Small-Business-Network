# Incorrect Next-Hop Address

## Problem

Traffic between the two LANs failed becasue a static route on R1 pointed to an incorrect next-hop IP address.

## Symptoms
- PC1 cannot reach PC2.
- All router interfaces are operational.
- The static route appears in the routing table.
- Pings to directly connected networks succeed.
- Traceroute fails after reaching R1.

## Investigation

1. Verified phyiscal connectivity between routers.
2. Confirmed interface status using show ip interface brief.
3. Reviewed the routing table.
4. Examined the running configuration.
5. Compared the configured next-hop address with the neighboring router's interface IP.

## Commands Used

```
show ip route
show running-config
show ip interface brief
ping
traceroute
```

## Root Cause

The static route on R1 referenced an incorrect next-hop address (10.0.12.11) instead of the correct neighboring router (10.0.12.2)

## Resolution

Removed the incorrect static route and configured the correct next-hop address.
```
no ip route 192.168.30.0 255.255.255.0 10.0.12.11
ip route 192.168.30.0 255.255.255.0 10.0.12.2
```

## Verification

- Confirmed the correct route in the routing table.
- Successfully pinged PC2 from PC1.
- Verified end-to-end connectivity between both LANs.
- Confirmed traceroute completed successfully.


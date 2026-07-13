# Incorrect Next-Hop Address

## Problem

PC1 is unable to communicate with PC2 because one of the required static routes on R2 has been accidentally removed.

## Symptoms

- PC1 unsuccessful ping to PC2.
- PC2 cannot reach PC1.
- Ping fails at R2 during a traceroute.

![Static-Routing](screenshots/NHA-Ping.png)

## Investigation

1. Verified that all router interfaces were up and operational.
2. Confirmed IP addressing on routers and PCs.
3. Reviewed the routing table on R2 using show ip route.
4. Compared the running configuration against the expected static routes.
5. Identified that the route to the remote network is missing.

![Static-Routing](screenshots/NHA-Routes.png)

## Commands Used
```
show ip route
show running-config
show ip interface brief
ping
tracert
```

## Root Cause

The static route to the 192.168.10.0/24 network had been removed from R2, preventing traffic from being forwarded to the remote LAN.

## Resolution

Reconfigured the missing static route.
ip route 192.168.10.0 255.255.255.0 10.0.12.1

![Static-Routing](screenshots/NHA-Fix.png)

## Verification

- Verified the static route appeared in the routing table.
- Successfully pinged PC2 from PC1.
- Successfully pinged PC1 from PC2.
- Confirmed traceroute completed through all three routers.

![Static-Routing](screenshots/NHA-Verify.png)


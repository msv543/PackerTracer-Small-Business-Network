# Incorrect Default Route

## Problem

Users report that communication within the local network is funcitoning normally, but external destinations connected through the simulated ISP cannot be reached.

## Symptoms

- Devices can successfully communicate within the local network.
- Inter-VLAN routing functions properly.
- Clients can reach their default gatways.
- Clients cannot ping the simulated ISP router.
- Traffic destined for unknown networks is dropped.
- End-to-end connectivity to external networks fails.

## Investigation

1. Verified client IP addressing and default gateway configuration.
2. Confirmed successful communication between VLANs.
3. Verified the WAN interface between the branch router and ISP router was operational.
4. Attempted to ping the ISP router from the branch router.
5. Examined the routing table using Cisco IOS verification commands.
6. Identified that the default route referenced an incorrect next-hop IP address.

## Commands Used

Client Verification
```
ping <default-gateway>
ping <ISP Router IP>
tracert <ISP Router IP>
```
Router
```
show ip interface brief
show ip route
show running-config
ping 209.165.200.1
```
ISP
```
show ip route
ping 209.165.200.1
```

## Root Cause

The branch router's default route pointed to an incorrect next-hop IP address. The router did not have a valid route for unknown destinations and traffic intended for the simulated ISP was discarded instead of being forwarded through the WAN link.

# Resolution

Removed the incorrect default route and configured the correct next-hop address.
```
no ip route 0.0.0.0 0.0.0.0 209.165.200.254
ip route 0.0.0.0 0.0.0.0 209.165.200.1
```

## Verification

- The routing table displayed the correct Gateway of Last Resort.
- The branch router successfully reached the simulated ISP router.
- Client devices successfully communicated with the simulated ISP.
- Traceroute confirmed packets were forwarded through the branch router to the ISP router.
- End-to-end WAN connectivity was fully restored.


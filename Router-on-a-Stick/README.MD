# Router-on-a-Stick

## Overview

This project demonstrates the deployment of Router-on-a-Stick configuration in Cisco Packet Tracer. The lab simulates a small multi-department environemnt using VLANs, Inter-VLAN Routing, DHCP, Router-on-a-Stick, and simulated ISP router.

## Network Topology
- 2 Cisco Routers
- 1 Cisco Switch
- 4 Client PCs
- Four departmental VLANs
![Router-on-a-Stick](screenshots/1-Topology.png)

## IP Addressing

```
Device        Interface        IP Address            Subnet Mask            Purpose
--- 
ISP           G0/0             209.165.200.1         255.255.255.252        WAN Link
R1            G0/0             209.165.200.2         255.255.255.252        WAN Link to ISP
R1            G0/1.10          192.168.10.1          255.255.255.0          VLAN 10 Gateway
R1            G0/1.20          192.168.20.1          255.255.255.0          VLAN 20 Gateway
R1            G0/1.30          192.168.30.1          255.255.255.0          VLAN 30 Gateway
R1            G0/1.99          192.168.99.1          255.255.255.0          VLAN 99 Gateway
PC1           DHCP             192.168.10.21         255.255.255.0          SALES
PC2           DHCP             192.168.20.21         255.255.255.0          IT
PC3           DHCP             192.168.30.21         255.255.255.0          HR
PC4           DHCP             192.168.99.21         255.255.255.0          Management
```
## Steps Performed

1. 

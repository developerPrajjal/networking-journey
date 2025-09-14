📘 Day 13 – Inter-VLAN Routing (Router-on-a-Stick with 2 VLANs)
🔹 Theory Notes

Why VLANs?
VLANs logically segment a switch into multiple broadcast domains.

VLAN 10 → e.g., Sales

VLAN 20 → e.g., HR

The Problem: By default, devices in different VLANs cannot communicate.

Solution – Router-on-a-Stick

Use one router interface connected to the switch.

Configure it as a trunk link.

Create subinterfaces (one per VLAN) on the router.

Each subinterface handles traffic for its VLAN using 802.1Q encapsulation.

Workflow:

Create VLANs on switch.

Assign switch ports to VLANs.

Configure trunk between switch & router.

On router → create subinterfaces for each VLAN.

Assign IPs → these act as default gateways for PCs.

Test ping across VLANs.

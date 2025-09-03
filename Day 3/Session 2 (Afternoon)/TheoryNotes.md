📘 Day 3 Afternoon – Inter-VLAN Routing (Router-on-a-Stick)

🔹 Theory Notes

1. Problem with VLANs

VLANs provide segmentation and isolate traffic.

Devices in different VLANs cannot communicate directly.

Example: HR VLAN cannot reach Finance VLAN.

2. Why Inter-VLAN Routing?

In real networks, departments need to communicate (e.g., HR ↔ Finance).

This requires Layer 3 (Routing).

3. Methods of Inter-VLAN Routing

Router-on-a-Stick (Legacy)

Single router interface used.

Multiple sub-interfaces created (1 per VLAN).

Switch port connected to router is a Trunk port.

Common in labs and CCNA syllabus.

Layer 3 Switch (Modern)

Routing done directly by switch.

Faster, used in enterprises.

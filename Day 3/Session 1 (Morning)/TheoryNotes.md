📖 Day 3 – VLAN Basics (Handwritten Notes)
1. Definition of VLAN

VLAN stands for Virtual Local Area Network.

It is used to logically divide a single physical switch into multiple smaller networks.

Even though devices may be physically connected to the same switch, VLANs make them behave as if they are on separate switches.

👉 Example:
Imagine a company has only one switch.

All HR computers can be put into VLAN 10.

All Finance computers can be put into VLAN 20.
Now HR and Finance cannot talk directly, even though they are on the same switch.

2. Why VLANs are Important?

Segmentation → Divides a big network into smaller, manageable parts.

Security → Sensitive departments (like Finance) are isolated from others.

Performance → Reduces unnecessary broadcast traffic, because broadcasts remain inside their VLAN.

Flexibility → Users can be grouped by function (e.g., HR, Sales, IT), not by their physical location.

3. Default VLAN

Every Cisco switch comes with a Default VLAN 1.

By default → all switch ports belong to VLAN 1.

That’s why when you connect 2 PCs to a fresh switch, they can immediately ping each other.

But if you move them to different VLANs → they will no longer communicate directly.

4. Communication Rules

Same VLAN → Devices can communicate normally.

Different VLANs → Devices cannot communicate (blocked) unless a Router or Layer 3 Switch is added for Inter-VLAN routing.

👉 Diagram for Notebook:

Draw one Switch in the middle.

Left side: PC-A (VLAN 10 – HR)

Right side: PC-B (VLAN 20 – Finance)

Write below the diagram:
“PC-A and PC-B are on the same physical switch, but since they are in different VLANs, they cannot ping each other.”

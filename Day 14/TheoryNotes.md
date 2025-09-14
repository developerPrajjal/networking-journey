📘 Day 14 – Multi-VLAN Router-on-a-Stick (4 VLANs)
🔹 Theory Notes

Scaling Day 13’s setup to multiple VLANs.

Each VLAN still requires:

VLAN creation on switch.

Port assignment.

Router subinterface with dot1Q encapsulation + IP.

The concept remains same, but now router handles multiple VLANs.

Useful in medium networks where multiple departments exist:

VLAN 10 → Sales

VLAN 20 → HR

VLAN 30 → IT

VLAN 40 → Management

🔹 Lab Work
🖥️ Topology:

PC0 ---- Switch ---- PC1

🔹 IP Addressing
Device	Interface	IP Address	Subnet Mask	Gateway
PC0	NIC	192.168.1.2	255.255.255.0	192.168.1.1
PC1	NIC	192.168.1.3	255.255.255.0	192.168.1.1
Switch	VLAN 1	192.168.1.1	255.255.255.0	---
🔹 Steps

Connect PC0 → Switch (Fa0/1), PC1 → Switch (Fa0/2).

Assign IP addresses to PCs.

On Switch, run:

Switch> enable
Switch# show spanning-tree


Output showed:

Switch elected as Root Bridge (lowest BID).

Ports Fa0/1 and Fa0/2 → Designated Forwarding state.

Verified STP timers (Hello, Max Age, Forward Delay).

Ping Test: PC0 → PC1 successful.

🔹 Verification

STP ensured no loops even if more redundant links were added.

Verified Root Bridge & Port Roles using:

Switch# show spanning-tree


Successful ping confirmed end-to-end connectivity.

✅ Conclusion

STP is critical for preventing Layer 2 loops in redundant topologies.

Learned Root Bridge election, Port Roles, and Port States.

Verified through Packet Tracer lab.

This forms the foundation for RSTP (Rapid STP) and MSTP (Multiple STP) in future labs.

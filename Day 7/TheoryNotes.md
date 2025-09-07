📘 Day 7 – Spanning Tree Protocol (STP)
🔹 Theory Notes
1. What is STP?

Spanning Tree Protocol (STP) is a Layer 2 protocol used in Ethernet networks to prevent loops.
Redundant links are necessary for fault tolerance, but they can create broadcast storms if frames loop endlessly.
STP solves this by blocking certain ports and keeping one logical path active.

2. How STP Works
Bridge ID (BID): Each switch has a unique BID = priority (default 32768) + MAC address.
The switch with the lowest BID becomes the Root Bridge.

Steps in STP Process:

Root Bridge Election → Lowest BID wins.

Root Port Selection (RP): On each switch, the port with the shortest path to the Root Bridge is chosen.

Designated Port (DP): For each network segment, the port closest to the Root becomes DP (it forwards traffic).

Blocked Port: Any extra redundant port is placed in Blocking state to prevent loops.

3. Port Roles

Root Port (RP): Path towards Root Bridge.

Designated Port (DP): Forwards traffic for its LAN segment.

Non-Designated Port (Blocked): Prevents loops by staying inactive.

4. Port States

Ports transition through states:

Blocking → Receives BPDU, doesn’t forward traffic.

Listening → Prepares to participate in STP.

Learning → Builds MAC table but doesn’t forward yet.

Forwarding → Actively forwards frames.

Disabled → Manually shut down.

Timers:

Hello Time = 2s

Max Age = 20s

Forward Delay = 15s

5. Commands Used

Check STP status:

Switch# show spanning-tree


Manually set priority (optional):

Switch(config)# spanning-tree vlan 1 priority 24576

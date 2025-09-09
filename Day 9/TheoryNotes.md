Day 9 – EtherChannel (PAgP)
🔹 Theory Notes
What is EtherChannel?

EtherChannel is a link aggregation technology that allows multiple physical Ethernet links to be combined into a single logical link.

Provides increased bandwidth and fault tolerance.

If one physical link fails, traffic automatically shifts to remaining links.

Benefits:

Increased Bandwidth – Multiple links act as one (e.g., 4 × 100 Mbps = 400 Mbps).

Redundancy – If one link fails, traffic keeps flowing.

STP Efficiency – Spanning Tree Protocol treats the entire bundle as a single link, avoiding blocked redundant paths.

Load Balancing – Distributes traffic across available links.

Protocols:

PAgP (Port Aggregation Protocol) → Cisco proprietary.

LACP (Link Aggregation Control Protocol) → IEEE standard (802.3ad).

On Mode → Forces bundling without negotiation (manual).

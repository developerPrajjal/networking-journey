Day 12 – EtherChannel Redundancy & Failover Testing
📖 Theory
🔹 What is EtherChannel?

EtherChannel is a technology that allows you to bundle multiple physical links between switches into a single logical link.

Provides higher bandwidth (sum of member links).

Provides redundancy (if one link fails, traffic moves to the others).

Managed as a single interface (Port-Channel).

🔹 Benefits of EtherChannel

Increased Bandwidth – Multiple links work as one logical link.

Redundancy/Fault Tolerance – If one link goes down, others carry traffic.

Load Balancing – Traffic distribution across links using different methods (src-mac, dst-mac, src-ip, etc.).

Simplified Management – Multiple links are managed under one Port-Channel interface.

🔹 Protocols Used

PAgP (Port Aggregation Protocol) – Cisco proprietary.

LACP (Link Aggregation Control Protocol) – IEEE standard (802.3ad).

On Mode – No negotiation, forces EtherChannel.

🔹 Failover Concept

If one physical link in the EtherChannel fails, the traffic is automatically rerouted through remaining links.

Ensures zero downtime for communication between switches.

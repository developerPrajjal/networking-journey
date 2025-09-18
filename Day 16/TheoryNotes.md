📘 Theory Notes – OSPF (Day X)
🔹 What is OSPF?

OSPF (Open Shortest Path First) is a link-state routing protocol.

Uses Dijkstra’s Shortest Path First (SPF) algorithm.

Interior Gateway Protocol (IGP) → works inside an Autonomous System (AS).

Protocol type: Dynamic Routing.

🔹 OSPF Features

Classless (supports VLSM & CIDR).

Metric: Cost (calculated based on interface bandwidth).

Fast convergence compared to RIP.

Supports areas for scalability:

Backbone Area (Area 0).

Non-backbone areas (must connect to Area 0).

Administrative Distance (AD): 110.

Supports authentication (clear text & MD5).

🔹 OSPF Packet Types

Hello Packet (for neighbor discovery).

DBD – Database Description.

LSR – Link State Request.

LSU – Link State Update.

LSAck – Link State Acknowledgement.

🔹 OSPF States (Neighbor Formation)

Down → Init → 2-Way → ExStart → Exchange → Loading → Full.

🔹 Verification Commands

show ip route → Check OSPF learned routes (marked with O).

show ip ospf neighbor → OSPF adjacency status.

show ip protocols → Networks advertised.

show ip ospf interface brief → Interfaces running OSPF.

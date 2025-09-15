📘 Day 15 – OSPF (Open Shortest Path First) – Theory Notes
🔹 Introduction to OSPF

OSPF (Open Shortest Path First) is a link-state routing protocol.

It is an IGP (Interior Gateway Protocol) designed for use within an Autonomous System (AS).

Uses Dijkstra’s SPF (Shortest Path First) algorithm to compute the best path.

Works with Areas to reduce complexity and improve scalability.

Runs directly on IP, protocol number 89 (not TCP/UDP).

🔹 Key Features

Classless Protocol → Supports VLSM & CIDR.

Convergence Speed → Much faster than Distance Vector protocols like RIP.

Metric → Cost, which is based on bandwidth (Cost = 100 / Bandwidth).

Supports Load Balancing over equal-cost paths.

Hello Protocol → Used to discover and maintain neighbor relationships.

Areas:

Area 0 = Backbone area (all others must connect to it).

Large networks are divided into areas for scalability.

🔹 OSPF Packet Types

Hello Packet → Discover neighbors, maintain adjacencies.

DBD (Database Description) → Summarized LSDB exchange.

LSR (Link State Request) → Ask neighbor for missing LSAs.

LSU (Link State Update) → Send LSAs to neighbors.

LSAck (Link State Acknowledgement) → Acknowledge LSUs.

🔹 OSPF Router Types

Internal Router → All interfaces in one area.

Backbone Router → Has interfaces in Area 0.

ABR (Area Border Router) → Connects multiple areas.

ASBR (Autonomous System Boundary Router) → Redistributes routes between OSPF and other protocols.

🔹 OSPF States (Neighbor Adjacency)

Down

Init

2-Way

ExStart

Exchange

Loading

Full (neighbors fully synchronized)

🔹 OSPF Configuration Basics

Enable OSPF process:
router ospf <process-id>

Set Router-ID (manually or via loopback).

Advertise networks:
network <ip> <wildcard> area <id>

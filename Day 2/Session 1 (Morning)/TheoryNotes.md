📘 Day 2 – Routers & IP Addressing (Theory)
🔹 What is a Router?

A Router is a Layer 3 device (Network Layer of OSI model).

Main role: connects multiple networks together.

Uses IP addresses to forward packets.

Think of it as traffic police – deciding the best path for data.

Each Router interface belongs to a different network.

🔹 Router vs Switch
Feature	Switch (Layer 2)	Router (Layer 3)
Works on	MAC Address (physical)	IP Address (logical)
OSI Layer	Layer 2 (Data Link)	Layer 3 (Network)
Purpose	Connects devices in same LAN	Connects different networks
Example	PC ↔ Switch ↔ PC (same LAN)	PC ↔ Router ↔ PC (different LANs)
🔹 IP Address Basics

IPv4 address = 32 bits, written in 4 octets (e.g., 192.168.1.10).

Consists of:

Network ID → identifies the network.

Host ID → identifies the device within the network.

Example:
192.168.1.10 /24

Network = 192.168.1.0

Host = .10

🔹 Subnet Mask

Subnet mask determines which part of IP = Network, which part = Host.

Example: 255.255.255.0 →

First 3 octets (192.168.1) = Network

Last octet = Host

👉 So all addresses from 192.168.1.1 to 192.168.1.254 are valid hosts in that network.

Why 254?

1 octet = 8 bits = 2⁸ = 256 values (0–255).

First address (192.168.1.0) = Network Address (reserved).

Last address (192.168.1.255) = Broadcast Address (reserved).

Remaining usable = 256 – 2 = 254 hosts.

🔹 Default Gateway

A Default Gateway is the Router’s IP inside the network.

Acts like a Post Office → forwards packets outside the local network.

Example:

PC1: 192.168.1.10 /24, Gateway: 192.168.1.1

PC2: 192.168.2.20 /24, Gateway: 192.168.2.1
👉 Since these two are on different networks, they need a Router (Gateway) to communicate.

🔹 Static Routing

By default, Routers only know networks directly connected to them.

To reach other networks, we configure Static Routes.

Static Route = manual entry in routing table.

Command Syntax (Cisco):

Router(config)# ip route <destination_network> <subnet_mask> <next_hop_ip>

Sample Example: 

Router(config)# ip route 192.168.2.0 255.255.255.0 192.168.1.2

Day 4 – Static Routing (Theory Notes)
🔹 What is Static Routing?

Static routing is a process where the network administrator manually configures the routes to reach remote networks.

Each route must be entered individually on every router.

🔹 Advantages:

Simple to configure for small networks

More secure (no automatic route exchange)

Uses less CPU and memory compared to dynamic routing

🔹 Disadvantages:

Not scalable for large networks (manual updates required)

High chance of human error while configuring

No automatic failover (if a link fails, admin must update routes)

🔹 Example Topology:

2 Routers connected via a serial/Gigabit link (10.0.0.0/30 network)

Router0 LAN: 192.168.1.0/24

Router1 LAN: 192.168.2.0/24

🔹 Command Syntax:
    Router(config)# ip route [destination_network] [subnet_mask] [next_hop_IP]

Example (Router0 → Router1):

Router(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2


Example (Router1 → Router0):

Router(config)# ip route 192.168.1.0 255.255.255.0 10.0.0.1

🔹 Troubleshooting Commands:

ping [ip] → To test connectivity

show ip interface brief → To check interface status and IPs

show running-config → To verify configuration

show ip route → To view routing table

📘 Day 5 – Static Routing (Theory Notes)
🔹 What is Static Routing?

Static Routing is a manual method of configuring network routes by the administrator.

Each route must be explicitly defined on the router.

Unlike dynamic routing protocols, static routing does not adapt automatically to network changes.

🔹 Key Command
ip route <destination-network> <subnet-mask> <next-hop-IP>


Example:

ip route 192.168.2.0 255.255.255.0 10.0.0.2


This means: “To reach network 192.168.2.0/24, forward packets to next-hop 10.0.0.2”.

🔹 Advantages

Simple to configure.

Predictable, full control of routing decisions.

Useful for small networks or default routes.

🔹 Disadvantages

Not scalable for large networks.

Does not auto-update if topology changes.

Requires manual changes if network grows.

🔹 When to Use

Small networks with limited routers.

As a backup route in enterprise networks.

For stub networks (single exit path).

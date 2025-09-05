🧪 Day 5 – Static Routing (Lab Notes)
🔹 Topology

2 Routers (Router0 & Router1)

2 PCs (PC0 & PC1)

Connections:

PC0 ↔ Router0 (G0/0) — Straight-through

PC1 ↔ Router1 (G0/0) — Straight-through

Router0 (G0/1) ↔ Router1 (G0/1) — Cross-over

🔹 IP Addressing Scheme

PC0 → 192.168.1.2 /24, Gateway: 192.168.1.1

Router0 G0/0 → 192.168.1.1 /24

Router0 G0/1 → 10.0.0.1 /30

Router1 G0/0 → 192.168.2.1 /24

Router1 G0/1 → 10.0.0.2 /30

PC1 → 192.168.2.2 /24, Gateway: 192.168.2.1

🔹 Router0 Configuration
enable
configure terminal
interface g0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
exit

interface g0/1
 ip address 10.0.0.1 255.255.255.252
 no shutdown
exit

ip route 192.168.2.0 255.255.255.0 10.0.0.2
end
write memory

🔹 Router1 Configuration
enable
configure terminal
interface g0/0
 ip address 192.168.2.1 255.255.255.0
 no shutdown
exit

interface g0/1
 ip address 10.0.0.2 255.255.255.252
 no shutdown
exit

ip route 192.168.1.0 255.255.255.0 10.0.0.1
end
write memory

🔹 Verification

Check interfaces:

show ip interface brief


→ All should be “up/up”.

Check routing table:

show ip route


→ Should display connected networks + static route.

Ping tests:

From Router0 → ping 10.0.0.2 ✅

From Router1 → ping 10.0.0.1 ✅

From PC0 → ping 192.168.1.1 ✅

From PC1 → ping 192.168.2.1 ✅

From PC0 → ping 192.168.2.2 ✅ (final success)

🔹 Result

✅ Static Routing configured successfully → End-to-End connectivity established between PC0 & PC1.

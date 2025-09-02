=============================
Day 2 - Router Configuration & Inter-VLAN Communication
=============================

🔹 Objective:
Understand how routers connect different networks and configure basic routing in Cisco Packet Tracer.

🔹 Topology:
PC0 --- Router0 --- PC1

🔹 IP Addressing:
PC0:
  IPv4: 192.168.1.2
  Subnet Mask: 255.255.255.0
  Default Gateway: 192.168.1.1

PC1:
  IPv4: 192.168.2.2
  Subnet Mask: 255.255.255.0
  Default Gateway: 192.168.2.1

Router0:
  Interface g0/0 → 192.168.1.1 255.255.255.0
  Interface g0/1 → 192.168.2.1 255.255.255.0

🔹 Router Configuration (CLI Commands):
Router> enable
Router# configure terminal
Router(config)# interface g0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface g0/1
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# end

🔹 Testing:
From PC0:
  ping 192.168.2.2  ✅ Successful
From PC1:
  ping 192.168.1.2  ✅ Successful

🔹 Key Takeaways:
- Routers operate at **Layer 3 (Network Layer)**.
- Each router interface must be in a **different network**.
- Default Gateway is required for PCs to reach other networks.
- First ping may fail due to ARP resolution, subsequent pings succeed.



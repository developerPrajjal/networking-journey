🧪 Day 15 – OSPF Lab Notes
🔹 Topology

 [PC-A] ---192.168.1.0/24--- [R1] ---10.0.12.0/30--- [R2] ---10.0.23.0/30--- [R3] ---192.168.3.0/24--- [PC-B]

 Loopback R1 = 1.1.1.1/32
 Loopback R2 = 2.2.2.2/32
 Loopback R3 = 3.3.3.3/32

🔹 IP Addressing Table

| Device | Interface | IP Address  | Subnet Mask     |
| ------ | --------- | ----------- | --------------- |
| PC-A   | NIC       | 192.168.1.2 | 255.255.255.0   |
| R1     | G0/0      | 192.168.1.1 | 255.255.255.0   |
| R1     | G0/1      | 10.0.12.1   | 255.255.255.252 |
| R1     | Loopback0 | 1.1.1.1     | 255.255.255.255 |
| R2     | G0/0      | 10.0.12.2   | 255.255.255.252 |
| R2     | G0/1      | 10.0.23.1   | 255.255.255.252 |
| R2     | Loopback0 | 2.2.2.2     | 255.255.255.255 |
| R3     | G0/0      | 10.0.23.2   | 255.255.255.252 |
| R3     | G0/1      | 192.168.3.1 | 255.255.255.0   |
| R3     | Loopback0 | 3.3.3.3     | 255.255.255.255 |
| PC-B   | NIC       | 192.168.3.2 | 255.255.255.0   |

🔹 Router Configurations
Router R1
---------------
enable
configure terminal
hostname R1
interface g0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
interface g0/1
 ip address 10.0.12.1 255.255.255.252
 no shutdown
interface loopback0
 ip address 1.1.1.1 255.255.255.255
exit
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.12.0 0.0.0.3 area 0
 network 1.1.1.1 0.0.0.0 area 0
exit
write memory

Router R2
------------
enable
configure terminal
hostname R2
interface g0/0
 ip address 10.0.12.2 255.255.255.252
 no shutdown
interface g0/1
 ip address 10.0.23.1 255.255.255.252
 no shutdown
interface loopback0
 ip address 2.2.2.2 255.255.255.255
exit
router ospf 1
 router-id 2.2.2.2
 network 10.0.12.0 0.0.0.3 area 0
 network 10.0.23.0 0.0.0.3 area 0
 network 2.2.2.2 0.0.0.0 area 0
exit
write memory

Router R3
------------
enable
configure terminal
hostname R3
interface g0/0
 ip address 10.0.23.2 255.255.255.252
 no shutdown
interface g0/1
 ip address 192.168.3.1 255.255.255.0
 no shutdown
interface loopback0
 ip address 3.3.3.3 255.255.255.255
exit
router ospf 1
 router-id 3.3.3.3
 network 10.0.23.0 0.0.0.3 area 0
 network 192.168.3.0 0.0.0.255 area 0
 network 3.3.3.3 0.0.0.0 area 0
exit
write memory

🔹 Verification

On Routers
------------
show ip ospf neighbor
show ip protocols
show ip route


Expect Full adjacency between R1 ↔ R2 and R2 ↔ R3.

Expect OSPF-learned routes (marked with O).

On PCs
-------------
PC-A> ping 192.168.3.2
PC-B> ping 192.168.1.2


✅ Successful reply confirms end-to-end OSPF connectivity.

🔹 Summary

Configured OSPF single area (Area 0) across 3 routers.

Added loopback interfaces as Router IDs.

Verified neighbors, routes, and pings.

Achieved full-mesh connectivity across the network.

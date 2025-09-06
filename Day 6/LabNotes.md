# Day 6 – RIP (Routing Information Protocol) Lab

## 🔹 Topology
   [PC0]                         [PC1]
 192.168.1.2/24              192.168.2.2/24
     |                           |
     |                           |
192.168.1.1                 192.168.2.1
 [G0/0] Router0 ----------- Router1 [G0/0]
           G0/1   10.0.0.1   10.0.0.2   G0/1
                 <--- 10.0.0.0/30 --->


---

## 🔹 IP Addressing Table

| Device   | Interface | IP Address    | Subnet Mask     | Gateway       |
|----------|-----------|---------------|-----------------|---------------|
| PC0      | NIC       | 192.168.1.2   | 255.255.255.0   | 192.168.1.1   |
| Router0  | G0/0      | 192.168.1.1   | 255.255.255.0   | ---           |
| Router0  | G0/1      | 10.0.0.1      | 255.255.255.252 | ---           |
| Router1  | G0/1      | 10.0.0.2      | 255.255.255.252 | ---           |
| Router1  | G0/0      | 192.168.2.1   | 255.255.255.0   | ---           |
| PC1      | NIC       | 192.168.2.2   | 255.255.255.0   | 192.168.2.1   |

---

## 🔹 RIP Configuration

### Router0
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.1.0
Router(config-router)# network 10.0.0.0
Router(config-router)# exit
Router(config)# exit
Router# write memory

### Router1
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.2.0
Router(config-router)# network 10.0.0.0
Router(config-router)# exit
Router(config)# exit
Router# write memory



---

🔹 Verification
1. Show IP Route

On both routers:

Router# show ip route


✅ You should now see learned RIP routes (with R code), e.g.:

R    192.168.2.0/24 [120/1] via 10.0.0.2, 00:00:22, GigabitEthernet0/1
C    192.168.1.0/24 is directly connected, GigabitEthernet0/0

2. Ping Test

From PC0 → PC1

C:\> ping 192.168.2.2

Reply from 192.168.2.2: bytes=32 time<1ms TTL=127
Reply from 192.168.2.2: bytes=32 time<1ms TTL=127


From PC1 → PC0

C:\> ping 192.168.1.2

Reply from 192.168.1.2: bytes=32 time<1ms TTL=127
Reply from 192.168.1.2: bytes=32 time<1ms TTL=127


✅ Successful communication proves RIP v2 dynamically updated the routing tables without needing static routes.

🔹 Key Learnings

Unlike Static Routing, RIP v2 automatically shares networks between routers.

Simplifies configuration in larger networks.

Still distance-vector based → uses hop count (max 15 hops).

Good for learning, but in real-world setups, OSPF/EIGRP are preferred for scalability.

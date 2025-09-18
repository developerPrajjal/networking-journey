🧪 Lab Notes – OSPF Single Area (Day X)
🔹 Topology
[PC0] --- Router0 --- Router1 --- [PC1]


PC0 → 192.168.1.2/24, GW: 192.168.1.1

Router0:

G0/0: 192.168.1.1/24

G0/1: 10.0.12.1/30

Router1:

G0/0: 192.168.2.1/24

G0/1: 10.0.12.2/30

PC1 → 192.168.2.2/24, GW: 192.168.2.1

🔹 Configuration
Router0
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# router-id 1.1.1.1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 10.0.12.0 0.0.0.3 area 0
Router(config-router)# end
Router# write memory

Router1
Router> enable
Router# configure terminal
Router(config)# router ospf 1
Router(config-router)# router-id 2.2.2.2
Router(config-router)# network 192.168.2.0 0.0.0.255 area 0
Router(config-router)# network 10.0.12.0 0.0.0.3 area 0
Router(config-router)# end
Router# write memory

🔹 Verification

Ping Test

From PC0 → ping 192.168.2.2 ✅ success

From PC1 → ping 192.168.1.2 ✅ success

Router Commands

Router# show ip route
Router# show ip ospf neighbor
Router# show ip protocols
Router# show ip ospf interface brief


✅ With this, OSPF is successfully configured & verified.

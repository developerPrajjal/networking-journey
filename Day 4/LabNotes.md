Day 4 – Static Routing (Lab Notes)
🔹 Lab Topology:

Router0 (LAN: 192.168.1.0/24)

Router1 (LAN: 192.168.2.0/24)

Inter-router link: 10.0.0.0/30

🔹 Step 1: Configure Router0
Router> enable
Router# configure terminal
Router(config)# interface g0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface g0/1
Router(config-if)# ip address 10.0.0.1 255.255.255.252
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# ip route 192.168.2.0 255.255.255.0 10.0.0.2

🔹 Step 2: Configure Router1
Router> enable
Router# configure terminal
Router(config)# interface g0/0
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface g0/1
Router(config-if)# ip address 10.0.0.2 255.255.255.252
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# ip route 192.168.1.0 255.255.255.0 10.0.0.1

🔹 Step 3: Configure PCs

PC0: IP → 192.168.1.2, Subnet → 255.255.255.0, Gateway → 192.168.1.1

PC1: IP → 192.168.2.2, Subnet → 255.255.255.0, Gateway → 192.168.2.1

🔹 Step 4: Testing

Ping between Router0 ↔ Router1 (10.0.0.1 ↔ 10.0.0.2)

Ping PC0 ↔ PC1 (192.168.1.2 ↔ 192.168.2.2)

Verify routing tables:

show ip route

show running-config

🔹 Issues Faced Today

Initially ping was failing between routers.

Debugging showed interfaces were shut down / cable mismatch.

Corrected by using crossover cable (Router-to-Router) and no shutdown.

Still in progress → Full PC-to-PC ping will be validated in Day 5.

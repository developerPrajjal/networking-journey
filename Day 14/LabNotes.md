🔹 Lab Topology
PC0 (192.168.10.2) --- VLAN10 ---|
PC1 (192.168.20.2) --- VLAN20 ---| 
PC2 (192.168.30.2) --- VLAN30 ---|--- Switch --- Router (G0/0 trunk)
PC3 (192.168.40.2) --- VLAN40 ---|

🔹 IP Addressing Table

| Device  | Interface | IP Address   | Subnet Mask   | Gateway      |
| ------- | --------- | ------------ | ------------- | ------------ |
| PC0     | NIC       | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 |
| PC1     | NIC       | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 |
| PC2     | NIC       | 192.168.30.2 | 255.255.255.0 | 192.168.30.1 |
| PC3     | NIC       | 192.168.40.2 | 255.255.255.0 | 192.168.40.1 |
| Router0 | G0/0.10   | 192.168.10.1 | 255.255.255.0 | ---          |
| Router0 | G0/0.20   | 192.168.20.1 | 255.255.255.0 | ---          |
| Router0 | G0/0.30   | 192.168.30.1 | 255.255.255.0 | ---          |
| Router0 | G0/0.40   | 192.168.40.1 | 255.255.255.0 | ---          |
| Router0 | G0/0      | Trunk Link   | ---           | ---          |

🔹 Configurations
Switch
Switch> enable
Switch# configure terminal

! VLAN creation
Switch(config)# vlan 10
Switch(config-vlan)# name Sales
Switch(config-vlan)# exit

Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config-vlan)# exit

Switch(config)# vlan 30
Switch(config-vlan)# name IT
Switch(config-vlan)# exit

Switch(config)# vlan 40
Switch(config-vlan)# name Management
Switch(config-vlan)# exit

! Assign ports
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit

Switch(config)# interface fa0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit

Switch(config)# interface fa0/3
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 30
Switch(config-if)# exit

Switch(config)# interface fa0/4
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 40
Switch(config-if)# exit

! Trunk link
Switch(config)# interface fa0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit

Router (Router-on-a-Stick)
Router> enable
Router# configure terminal

! VLAN 10
Router(config)# interface g0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

! VLAN 20
Router(config)# interface g0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit

! VLAN 30
Router(config)# interface g0/0.30
Router(config-subif)# encapsulation dot1Q 30
Router(config-subif)# ip address 192.168.30.1 255.255.255.0
Router(config-subif)# exit

! VLAN 40
Router(config)# interface g0/0.40
Router(config-subif)# encapsulation dot1Q 40
Router(config-subif)# ip address 192.168.40.1 255.255.255.0
Router(config-subif)# exit

! Enable physical interface
Router(config)# interface g0/0
Router(config-if)# no shutdown
Router(config-if)# exit

🔹 Verification

From PC0 → ping 192.168.20.2 / 30.2 / 40.2 ✅ Success

From PC1 → ping 192.168.10.2 / 30.2 / 40.2 ✅ Success

From PC2 → ping 192.168.10.2 / 20.2 / 40.2 ✅ Success

From PC3 → ping 192.168.10.2 / 20.2 / 30.2 ✅ Success

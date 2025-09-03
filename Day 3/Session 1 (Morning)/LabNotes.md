🧾 Step-by-Step VLAN Configuration Commands
1. Enter Switch Configuration Mode:
	Switch> enable
	Switch# configure terminal
2. Create VLANs

Example: VLAN 10 (HR) and VLAN 20 (Finance)
	Switch(config)# vlan 10
	Switch(config-vlan)# name HR
	Switch(config-vlan)# exit

	Switch(config)# vlan 20
	Switch(config-vlan)# name Finance
	Switch(config-vlan)# exit
3. Assign Switch Ports to VLANs

Suppose PC-A is on FastEthernet 0/1

Suppose PC-B is on FastEthernet 0/2

	Switch(config)# interface fastEthernet 0/1
	Switch(config-if)# switchport mode access
	Switch(config-if)# switchport access vlan 10
	Switch(config-if)# exit

	Switch(config)# interface fastEthernet 0/2
	Switch(config-if)# switchport mode access
	Switch(config-if)# switchport access vlan 20
	Switch(config-if)# exit

4. Verify VLAN Configuration

	Switch# show vlan brief

5. Testing

Ping between PC-A and PC-B.

❌ They will not ping because they are in different VLANs.

This proves VLAN segmentation is working.


Lab 2:

Step 1: Network Topology

Switch in the middle

PC-A → HR VLAN 10

PC-B → Finance VLAN 20

PC-C → Admin VLAN 30



      PC-A (192.168.10.2, VLAN 10 HR)
                   |
                   |
         --------------------
         |     Switch       |
         --------------------
          |           |
          |           |
PC-B (192.168.20.2,   PC-C (192.168.30.2,
     VLAN 20 Finance)      VLAN 30 Admin)


Step 2: Create VLANs on Switch

Go to switch CLI and type:

	enable
	configure terminal
	vlan 10
 		name HR
	exit
	vlan 20
	 	name Finance
	exit
	vlan 30
 		name Admin
	exit

Step 3: Assign Ports

Suppose:

PC-A is on Fa0/1

PC-B is on Fa0/2

PC-C is on Fa0/3

interface fa0/1
 switchport access vlan 10
exit
interface fa0/2
 switchport access vlan 20
exit
interface fa0/3
 switchport access vlan 30
exit

Step 4: Assign IPs on PCs

PC-A (HR) → 192.168.10.2 / 255.255.255.0

PC-B (Finance) → 192.168.20.2 / 255.255.255.0

PC-C (Admin) → 192.168.30.2 / 255.255.255.0

Step 5: Test Communication (Ping Matrix)

From PC-A → ping PC-B (fail ❌), ping PC-C (fail ❌)

From PC-B → ping PC-C (fail ❌)

Only PCs in same VLAN + same subnet can talk (in this lab, each one is in different VLAN, so isolation = strong).

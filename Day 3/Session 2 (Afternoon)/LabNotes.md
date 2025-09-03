🔹 Lab Notes

Devices Required:

1 Switch (2960)

1 Router (1941)

3 PCs (HR, Finance, Admin)

Connections:

PC-A → Switch Fa0/1 (VLAN 10, HR)

PC-B → Switch Fa0/2 (VLAN 20, Finance)

PC-C → Switch Fa0/3 (VLAN 30, Admin)

Switch Fa0/24 → Router G0/0 (Trunk)

IP Addressing Plan:

PC-A → 192.168.10.2 /24 | GW: 192.168.10.1

PC-B → 192.168.20.2 /24 | GW: 192.168.20.1

PC-C → 192.168.30.2 /24 | GW: 192.168.30.1

🔹 Switch Configuration

	enable
configure terminal

! Create VLANs

vlan 10
 name HR
exit
vlan 20
 name Finance
exit
vlan 30
 name Admin
exit

! Assign ports to VLANs

interface fa0/1
 switchport access vlan 10
exit
interface fa0/2
 switchport access vlan 20
exit
interface fa0/3
 switchport access vlan 30
exit

! Trunk to Router

interface fa0/24
 switchport mode trunk
exit

🔹 Router Configuration

	enable
configure terminal

! Enable physical interface
interface g0/0
 no shutdown
exit

! Sub-interface for VLAN 10
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
exit

! Sub-interface for VLAN 20
interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
exit

! Sub-interface for VLAN 30
interface g0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0
exit


🔹 Verification

From PC-A → ping 192.168.10.1 ✅ Success (gateway reachable).

From PC-A → ping 192.168.20.2 ✅ Success (via router).

From PC-C → ping 192.168.10.2 ✅ Success.

First ping may fail (due to ARP), subsequent pings succeed.

✅ Conclusion

VLANs isolate departments but block communication across VLANs.

Router-on-a-Stick enables inter-VLAN routing using sub-interfaces.

Each VLAN needs its own sub-interface + IP (gateway).

This is a core CCNA concept and widely used in practice.


⚙️ Topology
   PC0 ---- Switch2 ==== Switch3 ---- PC1
              |Fa0/1-4   |Fa0/1-4
              \__________Port-Channel1__________/


Switch2 ↔ Switch3 connected using 4 links (Fa0/1–Fa0/4) bundled into EtherChannel.

PC0 connected to Switch2 (Fa0/5).

PC1 connected to Switch3 (Fa0/5).

IP Addressing Table
Device	Interface	IP Address	Subnet Mask	Gateway
PC0	NIC	192.168.1.2	255.255.255.0	192.168.1.1
PC1	NIC	192.168.1.3	255.255.255.0	192.168.1.1
Switches	N/A	Layer 2 only	N/A	N/A
🔹 Configuration
On Switch2
enable
configure terminal
interface range fa0/1 - 4
 channel-group 1 mode desirable
exit

On Switch3
enable
configure terminal
interface range fa0/1 - 4
 channel-group 1 mode desirable
exit

🔹 Verification Commands

Check EtherChannel Summary

show etherchannel summary


Expected:

Po1(SU) → Port-Channel1 is up and in use.

Member ports should show (P) → bundled in channel.

Check Port-Channel Interface

show interfaces port-channel 1


Expected:

Port-channel1 is up, line protocol is up (connected).

Bandwidth is sum of all links (e.g., 400 Mb/s).

Check VLAN Membership

show vlan brief


Ensure PC ports (Fa0/5 on both switches) are in same VLAN (default VLAN 1).

Ping Test
On PC0:

ping 192.168.1.3


On PC1:

ping 192.168.1.2

🔹 Troubleshooting Steps (if ping fails)

Check if all ports are bundled: (P) flag must appear.

Verify VLAN membership of PC-facing ports.

Ensure both sides use same EtherChannel protocol (PAgP in this lab).

Check STP state: show spanning-tree.

Test with direct PC-to-PC same switch to isolate issue.

🔹 Key Takeaways

EtherChannel bundles multiple links to act as one logical connection.

Provides resilience, higher bandwidth, and STP efficiency.

In this lab, PAgP (desirable mode) was used to auto-negotiate EtherChannel.

Next step → Troubleshoot inter-switch EtherChannel to achieve end-to-end PC communication.

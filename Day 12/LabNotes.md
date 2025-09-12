🧪 Lab Setup
🔹 Topology

Switch0 ↔ Switch1 connected with 4 FastEthernet cables (Fa0/1 – Fa0/4).

PC0 connected to Switch0.

PC1 connected to Switch1.

🔹 IP Addressing
Device	Interface	IP Address	Subnet Mask	Gateway
PC0	NIC	192.168.1.2	255.255.255.0	192.168.1.1 (Switch Virtual)
PC1	NIC	192.168.1.3	255.255.255.0	192.168.1.1

(For simple PC-to-PC connectivity, no gateway config required in Packet Tracer, but usually assigned in real setups).

⚙️ Configuration
🔹 Switch0 (Configuring EtherChannel)
Switch> enable
Switch# configure terminal
Switch(config)# interface range fa0/1 - 4
Switch(config-if-range)# channel-group 1 mode desirable
Switch(config-if-range)# exit
Switch(config)# exit
Switch# show etherchannel summary

🔹 Switch1 (Configuring EtherChannel)
Switch> enable
Switch# configure terminal
Switch(config)# interface range fa0/1 - 4
Switch(config-if-range)# channel-group 1 mode desirable
Switch(config-if-range)# exit
Switch(config)# exit
Switch# show etherchannel summary

🔎 Verification
1. Check EtherChannel Status
Switch# show etherchannel summary


✅ Ports Fa0/1–Fa0/4 should show as (P) meaning they are active in the Port-Channel.

2. Ping Test Between PCs
PC0> ping 192.168.1.3
PC1> ping 192.168.1.2


✅ Successful replies confirm EtherChannel is passing traffic.

3. Failover Test

Shut down one member link on either switch:

Switch(config)# interface fa0/1
Switch(config-if)# shutdown


Ping again between PCs → ✅ traffic still flows (through remaining links).

✅ Results

EtherChannel successfully configured with 4 links bundled.

Verified redundancy and load sharing.

Failover test proved link resilience.

📌 Conclusion

EtherChannel is a powerful Layer 2 feature that boosts bandwidth while ensuring redundancy. It’s widely used in enterprise switching for scalable, fault-tolerant, and efficient network design.

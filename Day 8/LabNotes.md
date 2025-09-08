Lab — Triangle topology (full step-by-step)

Objective: configure RSTP (rapid-pvst) on three switches connected in a triangle and verify fast convergence.

Topology (text):
  Switch1 Fa0/1 <----> Fa0/1 Switch2
       \                   /
        \                 /
       Fa0/2           Fa0/2
          \             /
           \           /
             Switch3


Place PC0 on Switch1 and PC1 on Switch2 for connectivity tests.

IPs for PCs (example):

PC0: 192.168.10.2 /24 (default GW not needed for switch tests)

PC1: 192.168.10.3 /24

Step A — Build & cable

Place 3 × 2960 switches (Switch1, Switch2, Switch3).

Connect:

S1 Fa0/1 ↔ S2 Fa0/1 (Straight-through or cross—works due to auto-MDIX)

S2 Fa0/2 ↔ S3 Fa0/1

S3 Fa0/2 ↔ S1 Fa0/2

Connect PC0 to S1 Fa0/3, PC1 to S2 Fa0/3 using straight-through.

Step B — Enable RSTP (Rapid PVST) on all switches

On each switch (S1, S2, S3):

enable
configure terminal
spanning-tree mode rapid-pvst
end
write memory

Step C — (Optional) Force root switch (for deterministic results)

Choose Switch1 as root:

Switch1(config)# spanning-tree vlan 1 root primary


This reduces randomness in lab.

Step D — Verify initial STP state

On each switch:

show spanning-tree


Expected: Protocol = rstp (or rapid-pvst) and you will see port roles and states.

Step E — Simulate link failure & test convergence

Shutdown a link (on Switch2 side for example):

Switch2# configure terminal
Switch2(config)# interface fa0/1
Switch2(config-if)# shutdown


Immediately check other switches:

Switch1# show spanning-tree
Switch3# show spanning-tree


The Alternate port on the relevant switch should immediately transition to Forwarding (no 30-second waiting).

Re-enable interface:

Switch2(config-if)# no shutdown


Verify role/state returns to previous.

Step F — Ping test between PCs

On PC0:

ping 192.168.10.3


Should always succeed; during the simulated failure, convergence should be fast and ping drop minimal or zero depending on exact timing.

Verification & sample outputs
show spanning-tree (sample condensed output)
VLAN0001
  Spanning tree enabled protocol rstp
  Root ID    Priority    4097
             Address     001b.0c9f.9e80
             This bridge is the root

  Bridge ID  Priority    4097  (priority 4096 sys-id-ext 1)
             Address     001b.0c9f.9e80
             Hello Time  2 sec  Max Age 6 sec  Forward Delay 15 sec

Interface        Role Sts Cost      Prio.Nbr Type
---------------- ---- --- --------- -------- --------------------------------
Fa0/1            Desg FWD 19        128.1    P2p
Fa0/2            Desg FWD 19        128.2    P2p
Fa0/3            Edge FWD 0         128.3    P2p


protocol rstp confirms RSTP.

Port roles: Desg (Designated), Edge (PortFast enabled), etc.

show spanning-tree vlan 1 detail (useful fields)

Root ID, Bridge ID, root path cost, expected root port, timer values, port role & state per port, BPDU info.

show spanning-tree interface fa0/2 detail (sample)
Interface Fa0/2
 Port role    : alternate
 Port state   : discarding
 Path cost    : 19
 Port ID      : 128.2
 Designated root: 001b.0c9f.9e80
 Designated bridge: 001b.0c9f.9e80
 Last transition to forwarding: 00:02:44

Troubleshooting checklist

If something doesn't behave as expected, follow this checklist:

Mode mismatch

Ensure all switches use spanning-tree mode rapid-pvst (or compatible modes). Mixed STP/RSTP can force legacy behavior.

Verify cables & interfaces

show interface status — confirm ports are up.

show ip interface brief if layer3 devices.

Check BPDU exchange

show spanning-tree — are BPDUs being sent? If a port is blocked because no BPDU, maybe portfast misconfigured.

Root election unexpected

If the wrong switch is root, set root with:

spanning-tree vlan 1 root primary


Or adjust priority:

spanning-tree vlan 1 priority 4096


Port stuck in blocking / discarding

If port does not transit, check if it is Edge/PortFast. PortFast is only for access ports (do NOT use on trunk links!).

Use show spanning-tree inconsistent-ports to find misconfiguration.

Interoperability issues

If network has legacy STP-only devices, RSTP will interoperate but convergence may revert to legacy timers — check logs.

BPDU Guard

If PortFast is enabled on a trunk by mistake, BPDUguard can disable the port to prevent loops; check show logging.

Check logs

show logging may reveal topology change notifications or BPDU guard events.

Best practices & recommendations

Enable RSTP (rapid-pvst) globally in Cisco networks for per-VLAN rapid convergence.

Determine & set root bridges intentionally (use spanning-tree vlan X root primary) to avoid random root election.

Enable PortFast on access ports (user/PC ports) to skip learning delay:

Interface: spanning-tree portfast

Global: spanning-tree portfast default (use cautiously)

Enable BPDU Guard on PortFast ports to protect network from accidental switches:

spanning-tree bpduguard enable on interface

Global: spanning-tree portfast bpduguard default

Do NOT enable PortFast on trunk or switch-to-switch ports.

Document topology and ensure STP mode is consistent across the network.

Use EtherChannel when you want aggregated bandwidth across multiple links — avoids wasting links due to STP blocking (we do EtherChannel lab next).

Use per-VLAN RSTP (rapid-pvst) on Cisco when multiple VLANs exist for best behavior; consider MST for large deployments for scalability.

References / next steps

Next lab: EtherChannel (Day 9) — bundle multiple links and observe how STP interacts with aggregated links.

After that: MST, OSPF and other campus design topics.

Quick copy-paste checklist (commands to run during lab)
! On all switches
spanning-tree mode rapid-pvst
write memory

! Make a switch Root (optional)
spanning-tree vlan 1 root primary

! Portfast on access ports
interface fa0/3
 spanning-tree portfast
 spanning-tree bpduguard enable
 no shutdown
end

! Shutdown link to test (on S2)
interface fa0/1
 shutdown

! Re-enable
no shutdown

! Verify
show spanning-tree
show spanning-tree vlan 1 detail
show spanning-tree interface fa0/2 detail
show spanning-tree summary

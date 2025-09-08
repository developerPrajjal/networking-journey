Day 8 — Rapid Spanning Tree Protocol (RSTP) — Detailed Notes

Scope: deep theory + configuration examples (Cisco IOS), lab steps, verification commands, sample outputs, troubleshooting and best practices.
Use this for your GitHub repository so others can follow your Day-8 RSTP work.

1. Introduction & motivation

RSTP (IEEE 802.1w) is the rapid convergence version of the original Spanning Tree Protocol (STP, IEEE 802.1D).

Goal: maintain a loop-free Layer-2 topology and reduce downtime when topology changes occur (failover in seconds rather than tens of seconds).

RSTP is backwards compatible with STP; often deployed as Rapid PVST (Cisco) to operate per-VLAN.

2. STP recap — why RSTP?

Ethernet has no TTL; loops cause broadcast storms, MAC-table instability and network meltdown.

Classic STP (802.1D) uses 5 port states and timers resulting in 30–50 seconds of downtime on topology changes.

RSTP solves this by:

reducing states to 3,

introducing new port roles (Alternate/Backup),

exchanging BPDUs more proactively,

immediately transitioning point-to-point links to forwarding when safe.

3. RSTP fundamentals
Port roles (RSTP)

Root Port (RP): best path from the switch to the root bridge.

Designated Port (DP): forwards frames for a given LAN segment.

Alternate Port: a backup for the Root Port (blocks but can take over instantly).

Backup Port: a backup to a Designated Port on the same switch/collision domain.

Port states (RSTP simplified)

Discarding (no data forwarding) — replaces Blocking + Listening.

Learning (learns MACs, no forwarding).

Forwarding (learns + forwards).

BPDUs & handshake

RSTP uses BPDUs as in STP but every switch sends BPDUs (not just the root).

For point-to-point links, RSTP uses a proposal/agreement handshake which allows two switches to quickly agree which port becomes forwarding.

Timers (RSTP recommended values)

Hello Time: 2 seconds

Max Age: typically 6 seconds in RSTP contexts (but in Cisco PVST variants, defaults may still reflect compatibility)

Forward Delay: still exists for interoperability but RSTP transitions are often immediate on point-to-point

Note: On Cisco, rapid-pvst is the recommended per-VLAN RSTP mode. Some IOS versions show Max Age still as 20 if interoperating with legacy switches — check show spanning-tree outputs.

4. Cisco implementation notes

Cisco supports Rapid PVST (Rapid Per-VLAN Spanning Tree) (command: spanning-tree mode rapid-pvst). This runs an RSTP instance per VLAN (similar to PVST vs STP).

spanning-tree mode rstp is single-instance RSTP (less commonly used on Cisco).

Cisco also has RPVST+ and MST for multiple VLAN scalability.

5. Cost & path selection

Bridge ID (BID) = priority (default 32768) + system-id-extension (VLAN) + MAC address. Lowest BID wins as root.

Path cost: STP/RSTP picks lowest path cost to the root. Cisco default costs:

FastEthernet (100Mb): cost = 19

GigabitEthernet (1Gb): cost = 4

(These are Cisco’s default PVST costs. Always check show spanning-tree for active costs).

If path cost ties, next tie-breaker is lowest root path bridge ID, then lowest sender port ID, etc.

Cost formula (IEEE 802.1D-2004 reference):

Cost can be derived from bandwidth, but Cisco uses its own default values for backward compatibility. For precise calculations, reference switch documentation or show spanning-tree states.

6. CLI commands (useful IOS commands)
Global mode
! Set RSTP per-VLAN (Cisco recommended)
Switch(config)# spanning-tree mode rapid-pvst

! Set a switch as root for VLAN 1 (preferred modern command)
Switch(config)# spanning-tree vlan 1 root primary
! or specific value
Switch(config)# spanning-tree vlan 1 priority 4096

! Show summary & detail
Switch# show spanning-tree summary
Switch# show spanning-tree
Switch# show spanning-tree vlan 1
Switch# show spanning-tree vlan 1 detail

! Show root and bridge info
Switch# show spanning-tree root
Switch# show spanning-tree bridge

Interface mode
! set portfast (edge ports)
Switch(config-if)# spanning-tree portfast
! globally enable PortFast on all access ports (use with caution)
Switch(config)# spanning-tree portfast default

! enable BPDU guard on interface
Switch(config-if)# spanning-tree bpduguard enable
! globally enable BPDUguard on PortFast ports
Switch(config)# spanning-tree portfast bpduguard default

! set edge port with modern CLI (some IOS)
Switch(config-if)# spanning-tree link-type point-to-point

Viewing
Switch# show spanning-tree
Switch# show spanning-tree interface fa0/1 detail
Switch# show spanning-tree inconsistent-ports
Switch# show spanning-tree active
Switch# show logging

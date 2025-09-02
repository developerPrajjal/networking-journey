📖 Day 2 Afternoon Session – Packet Journey & Default Gateway
🔹 1. Local Network Communication

If PC0 (192.168.1.2) wants to talk to another PC in same network (192.168.1.X):

PC0 checks → Is destination IP in my subnet?

If YES → PC0 sends packet directly to that PC using its MAC (via ARP).
✅ Example: 192.168.1.2 → 192.168.1.3 (no router needed).

🔹 2. Remote Network Communication (Different Subnet)

If PC0 (192.168.1.2) wants to talk to PC1 (192.168.2.2):

PC0 checks → Is 192.168.2.2 in my subnet (192.168.1.0/24)?

Answer = NO ❌ (different network).

So PC0 cannot send directly.

Instead → PC0 forwards the packet to its Default Gateway (192.168.1.1).

👉 Default Gateway = Router IP in the same network as PC, responsible for sending traffic outside.

🔹 3. Step by Step Journey (Our Lab Topology)

Step 1 – PC0 Prepares Packet

Source IP = 192.168.1.2

Destination IP = 192.168.2.2

Destination NOT in local subnet → Forward to Gateway = 192.168.1.1

Step 2 – ARP Request (First Time Only)

PC0: “Who has 192.168.1.1? Tell 192.168.1.2”

Router replies with its MAC address.

PC0 stores Gateway’s MAC in its ARP table.

Step 3 – Send Packet to Router

Packet goes from PC0 → Router G0/0 (192.168.1.1).

Step 4 – Router Processing

Router checks Destination IP (192.168.2.2).

Router sees → Destination belongs to network 192.168.2.0/24.

Router knows → “That network is directly connected on my G0/1 interface (192.168.2.1).”

Router forwards packet out of G0/1.

Step 5 – ARP for PC1

Router: “Who has 192.168.2.2?”

PC1 replies with its MAC.

Router stores it in ARP table.

Step 6 – Deliver Packet

Router sends packet to PC1.

PC1 processes it → sends Reply packet back the same way (via Router).

🔹 4. Key Concepts Learned

Same Network = Direct communication

Different Network = Needs Router (Gateway)

ARP helps discover MAC address of next hop.

Router uses its Routing Table to forward packets to correct interface.

Without correct Default Gateway, PC cannot reach outside networks.



-----------------------------------


🔹 What is ARP (Address Resolution Protocol)?

👉 ARP is like a translator between IP address and MAC address.

IP Address = Logical address (like your home’s street address).

MAC Address = Physical hardware address of a device’s NIC (like your house number on the building).

For a packet to actually travel inside a LAN, the sender must know the MAC address of the next device.

That’s where ARP comes in.

🔸 How ARP Works (Step-by-Step)

PC0 wants to send data to 192.168.1.1 (its Default Gateway).

PC0 checks its ARP Table: “Do I already know the MAC of 192.168.1.1?”

If YES → Use it directly.

If NO → Send an ARP Request:

“Who has IP 192.168.1.1? Tell me (192.168.1.2).”

Router (192.168.1.1) replies with ARP Reply:

“192.168.1.1 is at MAC aa:bb:cc:dd:ee:ff.”

PC0 stores this mapping in its ARP Table.

Now, PC0 can send packets to Router using the Router’s MAC.

🔸 Key Points

ARP only works inside a LAN (local network), because MAC addresses are not routed.

Every time a new device is contacted → an ARP request is made (unless already cached).

Without ARP → IP communication cannot happen, because Ethernet needs MAC addresses to deliver frames.

🔸 Example with our Lab

PC0 (192.168.1.2) → wants to talk to PC1 (192.168.2.2).

First, PC0 ARPs for its Default Gateway (192.168.1.1).

Then Router ARPs for PC1 (192.168.2.2).

Both ARPs resolve MACs → and only then actual ICMP packets flow.

📓 Notebook Note:
ARP = Address Resolution Protocol

Maps IP → MAC inside LAN.

Uses Request (broadcast) + Reply (unicast).

Stored in ARP Table for quick use.

Required for communication even with Default Gateway.

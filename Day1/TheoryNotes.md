📝 Concepts Learned:

1. Every device in a network must have an IP Address to communicate.

2. Devices must be in the same subnet to talk directly.

Example: 192.168.1.1 and 192.168.1.2 work together with subnet mask 255.255.255.0.

3. Subnet Mask (255.255.255.0)

Network Portion = First 3 octets (192.168.1)

Host Portion = Last octet (.x)

Range of usable hosts: 192.168.1.1 – 192.168.1.254

Total usable = 254 devices

4. Cables:

PC ↔ PC → Copper Cross-Over Cable

PC ↔ Switch → Straight-Through Cable

5. Ping Command is used to test connectivity.

-----------------------

7 Layers of OSI Model

1.Physical → Cables, switches, signals (bits: 0s and 1s).

2.Data Link → MAC addresses, Ethernet (frames).

3.Network → IP addresses, routing (packets).

4.Transport → TCP/UDP, port numbers, reliability (segments).

5.Session → Manages sessions (start/end communication).

6.Presentation → Encryption, compression, data format.

7.Application → End-user apps (browser, email, WhatsApp).

------------------------

🔹 Why do we need Switches?

In real networks, you don’t connect every PC directly to another PC (that would be messy and impossible).

Instead, all PCs connect to a central device = Switch.

The switch works at Layer 2 (Data Link) of OSI model.

👉 You can think of a switch as a traffic cop that forwards data only to the correct PC instead of shouting to everyone.

🔹 How Does a Switch Work?

Every device (PC, printer, etc.) has a MAC address (unique hardware ID).

When PC0 sends data to PC1:

Switch looks at PC0’s MAC (source).

Learns which port PC0 is connected to.

Forwards the data only to the port where PC1 is connected.

This is called MAC Address Learning.

🔹 Switch vs Hub (old device)

Hub: sends data to all devices → slow, insecure.

Switch: sends data only to the right device → fast, efficient.


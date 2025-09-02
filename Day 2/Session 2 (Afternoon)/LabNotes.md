🧪 Lab Task: Watching ARP in Simulation Mode

Open your PC0 Command Prompt.

Type: arp -a → (it will probably show an empty table at first).

Now, in Simulation Mode:

From PC0, ping 192.168.2.2.

Watch carefully → before ICMP packets go, you’ll see ARP Request + ARP Reply being exchanged.

After the ping, check again:

On PC0 Command Prompt, type: arp -a.

Now you’ll see the Router’s MAC address mapped to 192.168.1.1

______________________________________________________________________________



🧪 Lab: Watching ARP in Action (Packet Tracer)
🔹 Step 1: Open Simulation Mode

At the bottom right of Packet Tracer, switch from Realtime → Simulation.

🔹 Step 2: Clear ARP Table

On PC0, open the Command Prompt.

Type:
	arp -a
{ It should show empty or very few entries (since no communication happened yet). }

🔹 Step 3: Trigger Communication

On PC0 Command Prompt, type:
	ping 192.168.2.2
Watch the simulation window — you’ll see ARP Request → ARP Reply → then ICMP packets flowing.

🔹 Step 4: Check ARP Table Again

On PC0, after the ping succeeds, type:
	arp -a

Now you’ll see the Router’s MAC address mapped to 192.168.1.1.

🔹 Step 5 (Bonus)

Do the same from PC1 → ping 192.168.1.2.

Then check arp -a on PC1.

You’ll see the Router’s MAC for 192.168.2.1 stored.


🔎 Why 1 Timeout?

The first ping usually times out because before the PC can send the ICMP Echo request, it must resolve the MAC address of the default gateway (router’s interface).

This happens via ARP (Address Resolution Protocol) → PC asks: “Who has 192.168.1.1?” → Router replies with its MAC.

That ARP exchange takes time, so the first ping gets dropped.

✅ Why the next 3 work?

Once ARP knows the router’s MAC address, the PC can send packets directly.

Now all pings succeed with <5ms delay (normal in Packet Tracer).

📝 Key Takeaway Notes (add this in your notebook today):

Ping + ARP relation: The first ping may fail due to ARP lookup.

ARP Cache: After the ARP entry is saved in cache, subsequent pings succeed.

Router’s role: The router forwards packets between different networks (192.168.1.0/24 ↔ 192.168.2.0/24).

Practical tip: Always expect the first ping to fail in real networks too, because of ARP or DNS lookups.

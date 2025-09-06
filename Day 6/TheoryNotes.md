# Day 6 – Routing Information Protocol (RIP)

## 🔹 Recap of Static Routing
- Static routing requires **manual configuration** of all routes by the administrator.  
- It works well in **small networks**.  
- However, in **larger and more complex networks**, managing static routes becomes error-prone and time-consuming.  
- Static routes do not adapt automatically to changes or link failures.  

**Example:**  
ip route 192.168.2.0 255.255.255.0 10.0.0.2

markdown
Copy code

---

## 🔹 Dynamic Routing – Introduction
Dynamic routing protocols allow routers to **automatically share and learn routes** from neighboring routers.  
- They **adapt to changes** in the network automatically.  
- Reduce **administrative overhead**.  
- Provide **fault tolerance** compared to static routes.  

### Types of Dynamic Routing Protocols
1. **Distance Vector Protocols**  
   - Example: RIP  
   - Routers share routing tables with neighbors.  
   - Simple but slower and less scalable.  

2. **Link State Protocols**  
   - Example: OSPF  
   - Each router builds a complete map of the network.  
   - Faster convergence, used in larger networks.  

3. **Hybrid Protocols**  
   - Example: EIGRP  
   - Combines benefits of both Distance Vector and Link State.  

---

## 🔹 RIP – Routing Information Protocol
- RIP is one of the **oldest and simplest** dynamic routing protocols.  
- Type: **Distance Vector**.  
- Metric: **Hop Count** (each router = 1 hop).  
- Maximum hops: **15** (16 = unreachable).  
- Sends routing updates every **30 seconds**.  
- Best suited for **small to medium networks**.  
- Though outdated in real enterprise networks, RIP is still widely used for **learning CCNA fundamentals**.  

---

## 🔹 RIP Configuration Syntax
To enable RIP on a Cisco Router:  
Router> enable
Router# configure terminal
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network [network-address]
Router(config-router)# exit
Router(config)# exit
Router# write memory

yaml
Copy code

---

✅ End of Theory Notes for Day 6.  
Lab exercise with full topology and configuration will follow in **Day 6 - Lab.md**.

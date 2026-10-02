# Westfold Textile Mills – Computer Networking & Cyber Security

##  Project Overview

This project is a Cisco Packet Tracer implementation of the network infrastructure for **Westfold Textile Mills**.

The network connects the company's **Headquarters (HQ), Weaving Plant, and Loomcraft Fabrics network** while maintaining the existing EIGRP routing environment at Loomcraft.

The project focuses on multi-site routing, network segmentation, access control, Internet connectivity, and address translation.

---

##  Objectives

The main objectives of this project are:

- Configure static and default routing as the initial routing setup.
- Replace HQ–Plant static routing with multi-area OSPF.
- Configure OSPF Area 0 and Area 10.
- Verify OSPF neighbor adjacency and DR/BDR election.
- Maintain the Loomcraft EIGRP network using AS 950.
- Configure OSPF–EIGRP route redistribution.
- Configure route summarization.
- Configure eBGP connectivity with two ISPs.
- Implement VLAN segmentation for Finance and Guest networks.
- Configure ACLs to restrict Guest access to Finance.
- Configure NAT/PAT for internal Internet access.
- Configure Static NAT for external access to the internal web server.
- Verify routing, security, NAT and failover using connectivity tests and Cisco IOS commands.

---

##  Network Architecture

The topology contains:

- **7 Cisco 2911 Routers**
- **4 Cisco 2960-24TT Switches**
- **10 End Devices**
- **2 Internet Service Providers**

### Routers

| Router | Purpose |
|---|---|
| HQ-EDGE | Internet edge, BGP and NAT/PAT |
| HQ-CORE | HQ internal routing and VLAN gateway |
| PLANT-ABR | OSPF Area 0 ↔ Area 10 |
| PLANT-BOUNDARY | OSPF/EIGRP redistribution |
| LOOMCRAFT-R1 | Loomcraft EIGRP routing |
| ISP-C | ISP-Crestline |
| ISP-H | ISP-Harbor |

---

##  Routing Protocols

### Static Routing

Static and default routes were initially configured to establish basic connectivity between HQ, Plant and the ISP.

The HQ–Plant static routes were later replaced by OSPF.

### OSPF

- Process ID: **10**
- Area 0: HQ backbone
- Area 10: Plant LAN
- PLANT-ABR connects Area 0 and Area 10
- OSPF neighbor adjacency was verified
- DR/BDR election was verified on the Plant LAN

### EIGRP

- Autonomous System: **950**
- Used for the existing Loomcraft network
- Loomcraft LAN: `172.31.50.0/24`

### Route Redistribution

PLANT-BOUNDARY acts as the routing boundary between OSPF and EIGRP.

Routes are redistributed in both directions:

```text
OSPF → EIGRP
EIGRP → OSPF

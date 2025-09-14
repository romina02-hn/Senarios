# EIGRP Lab in EVE-NG

## Project Goal
This project demonstrates the implementation of **Enhanced Interior Gateway Routing Protocol (EIGRP)** in an enterprise-like topology using Cisco IOS routers in **EVE-NG**.  
The lab simulates dynamic routing between multiple routers, ensuring reachability across different networks and loopbacks.

---

## Topology
- **5 Cisco Routers (R1 – R5)**
- **1 Layer 3 Switch (SW4)**
- **1 End Host (VPC)**

### Connections
- SW4 ↔ R1 → 1.1.1.0/24  
- R1 ↔ R2 → 2.2.2.0/24  
- R1 ↔ R3 → 3.3.3.0/24  
- R1 ↔ R4 → 4.4.4.0/24  
- R2 ↔ R3 → 6.6.6.0/24  
- R3 ↔ R4 → 5.5.5.0/24  
- R3 ↔ R5 → 7.7.7.0/24  

### Loopbacks
- R5:  
  - lo0 → 8.8.8.8/32  
  - lo1 → 10.0.0.1/24  
  - lo2 → 10.0.1.1/24  
  - lo3 → 10.0.4.1/24  
  - lo4 → 40.0.0.1/24  
  - lo5 → 40.0.2.1/23  
  - lo6 → 40.0.1.1/25  
  - lo7 → 40.0.1.129/25  
  - lo8 → 40.0.16.1/20  
  - lo9 → 10.0.2.1/23  
  - lo10 → 100.100.100.100/32  

- End Host (VPC):  
  - 9.9.9.2/24 → connected via SW4  

---

## Configuration Overview

### EIGRP Setup
- **AS Number:** 100  
- All routers (R1–R5) participate in EIGRP process 100  
- Network statements include:  
  - All inter-router links  
  - Loopback interfaces on R5  

### Key Features
- Automatic discovery of neighbors on directly connected networks  
- R5 advertises multiple Loopbacks into EIGRP  
- End Host (VPC) can reach all loopbacks via dynamic routing  
- Feasible successor routes can be tested for redundancy (ex: multiple paths R1 ↔ R3 ↔ R2)  



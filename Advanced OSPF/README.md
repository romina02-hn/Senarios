# Advanced OSPF Lab in EVE-NG

## Project Goal
This project demonstrates the implementation of an **Advanced OSPF topology** using Cisco IOS routers in **EVE-NG**.  
The lab simulates a real-world enterprise/service provider environment with multiple OSPF areas, different network types, redistribution of external routes, and advanced area designs.

## Topology
- **12 Cisco Routers (R1 – R12)**
- OSPF Areas and their functions:
  - **Area 0 (Backbone):** Non-Broadcast  
  - **Area 39:** Standard Area  
  - **Area 40:** Stub Area with multiple loopbacks (R11)  
  - **Area 57:** Point-to-Point  
  - **Area 68:** Hybrid Area  
  - **Area 90:** Standard Area  

- **External Routes** redistributed into OSPF at R2:
  - 100.10.1.0/24  
  - 100.10.2.0/24  
  - 100.10.3.0/24  
  - 100.10.4.0/24  

*(The `.unl` topology file is included in this repository for EVE-NG.)*

## Configuration Overview
### OSPF Setup
- **Multiple OSPF Areas** with proper backbone connectivity  
- **Redistribution of External Routes** into OSPF at R2  
- **Loopback Interfaces** in Area 40 to simulate multiple subnets  
- **Different OSPF Network Types**:
  - Area 0 → Non-Broadcast  
  - Area 57 → Point-to-Point  
  - Area 68 → Hybrid  

### Advanced Features
- Inter-area routing across multiple OSPF areas  
- External route injection (Type-5 LSAs)  
- OSPF neighbor adjacencies over different network types  

## Sample Configurations
#### R2 – External Redistribution into OSPF
```cisco
router ospf 1
 router-id 2.2.2.2
 network 10.0.0.0 0.255.255.255 area 0
 redistribute static subnets
!
ip route 100.10.1.0 255.255.255.0 Null0
ip route 100.10.2.0 255.255.255.0 Null0
ip route 100.10.3.0 255.255.255.0 Null0
ip route 100.10.4.0 255.255.255.0 Null0

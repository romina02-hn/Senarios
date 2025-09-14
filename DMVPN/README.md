# DMVPN Lab in EVE-NG

## Project Goal
This project demonstrates the implementation of a **Dynamic Multipoint VPN (DMVPN)** topology using Cisco IOS routers in **EVE-NG**.  
The lab simulates a scalable site-to-site VPN where multiple branch routers (Spokes) dynamically establish tunnels with the Hub and optionally with each other.

## Topology
- **4 Cisco Routers (R1 – R4)**
  - **R1:** DMVPN Hub  
  - **R2, R3, R4:** DMVPN Spokes  
- Public WAN connections:
  - R1 ↔ R2: 10.0.12.0/24  
  - R1 ↔ R3: 10.0.13.0/24  
  - R1 ↔ R4: 10.0.14.0/24  
- Private LANs behind each spoke:
  - R2: 192.168.2.0/24  
  - R3: 192.168.3.0/24  
  - R4: 192.168.4.0/24  
- DMVPN Tunnel network: **172.16.0.0/24**  
  - R1 (Hub): 172.16.0.1  
  - R2 (Spoke): 172.16.0.2  
  - R3 (Spoke): 172.16.0.3  
  - R4 (Spoke): 172.16.0.4  

*(The `.unl` topology file is included in this repository for EVE-NG.)*

## Configuration Overview
### DMVPN Setup
- **Phase 1 Hub-and-Spoke Topology**
- Tunnel interfaces using `tunnel mode gre multipoint`
- NHRP for dynamic tunnel mapping
- Hub (R1) with a multipoint GRE tunnel  
- Spokes (R2, R3, R4) with dynamic NHRP registration  

### Routing
- OSPF or EIGRP running over the DMVPN tunnel  
- Full reachability between spoke LANs through the Hub

### Advanced Features
- **NHRP Mapping** for dynamic tunnel resolution  
- **Multipoint GRE Tunnel** for scalability  
- **Optional IPsec Protection** for secure DMVPN deployment  

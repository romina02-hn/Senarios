# GRE over IPsec Lab in EVE-NG

## Project Goal
This project demonstrates the implementation of a **GRE over IPsec tunnel** using Cisco IOS routers in **EVE-NG**.  
The lab simulates a secure site-to-site connection where GRE provides multiprotocol support and IPsec ensures encryption and authentication.

## Topology
- **3 Cisco Routers (R1, R2, R3)**
- **2 Switches (SW4, SW5)**
- **2 End Hosts (VPC6, VPC7)**

- Networks:
  - R1 ↔ R2 ↔ R3 WAN: **64.100.0.0/24**
  - R1 LAN: **10.10.1.0/24**, plus Loopbacks (10.10.2.0/24, 10.10.3.0/24)
  - R3 LAN: **10.10.4.0/24**, **10.10.5.0/24**, plus Loopbacks (10.10.16.0/24 … 10.10.23.0/24)

*(The `.unl` topology file is included in this repository for EVE-NG.)*

## Configuration Overview
### GRE Setup
- GRE Tunnel configured between R1 and R3 over the public WAN (64.100.0.0/24)
- Tunnel interface carries private LAN and loopback subnets
- OSPF 123 enabled over the GRE tunnel (Area 0)

### IPsec Setup
- ISAKMP Phase 1 policy for authentication and encryption
- IPsec Phase 2 transform set for traffic protection
- Crypto map applied on WAN interfaces of R1 and R3
- GRE tunnel traffic selected by ACL for encryption

### Advanced Features
- **Routing:** OSPF adjacency built over the GRE tunnel
- **Security:** IPsec ensures confidentiality, integrity, and authentication of tunnel traffic
- **Connectivity:** End hosts (VPC6 ↔ VPC7) communicate securely through the GRE over IPsec tunnel



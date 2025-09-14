# BGP Multi-AS Lab in EVE-NG

## Project Goal
This project demonstrates the implementation of a **BGP Multi-AS topology** using Cisco IOS routers in **EVE-NG**.  
The lab simulates a real-world service provider environment with multiple Autonomous Systems (AS), iBGP and eBGP peering, and route policies.

## Topology
- **21 Cisco Routers (R1 – R21)**
- Devices are divided into multiple AS domains:
  - AS 65001: R1 – R7
  - AS 65002: R8 – R14
  - AS 65003: R15 – R21

*(The `.unl` topology file is included in this repository for EVE-NG.)*

## Configuration Overview
### BGP Setup
- **eBGP Peering** between edge routers of each AS
- **iBGP Full-Mesh** inside each AS
- **Route Reflectors** to reduce iBGP peering overhead
- **Loopback Interfaces** as BGP router IDs

### Routing Policies
- **Prefix-Lists** for route advertisement filtering
- **Route-Maps** for controlling inbound/outbound traffic
- **Local Preference & MED** for path selection
- **AS-Path Prepending** to influence upstream routing

### Sample Configurations
#### Router in AS 65001 (R1)
```cisco
router bgp 65001
 bgp log-neighbor-changes
 neighbor 192.168.12.2 remote-as 65001
 neighbor 192.168.12.2 update-source Loopback0
 neighbor 10.10.23.2 remote-as 65002
 network 10.1.0.0 mask 255.255.255.0

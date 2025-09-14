# VXLAN + EVPN Lab in EVE-NG

## Project Goal
This project demonstrates the implementation of a **VXLAN with EVPN (MP-BGP)** topology using Cisco NX-OSv switches in **EVE-NG**.  
The lab simulates a modern data center fabric where **L2 networks are extended over an IP underlay** using VXLAN, and EVPN provides the control plane for MAC/IP distribution.

---

## Topology
- **4 Cisco NX-OSv Switches (NXOS1 – NXOS4)**  
  - **NXOS1, NXOS2:** Leaf switches (VTEPs connected to end-hosts)  
  - **NXOS3, NXOS4:** Spine switches (IP Fabric only, no direct host connections)  

- **Loopback Interfaces (VTEP source addresses):**  
  - NXOS1 → 10.10.10.10  
  - NXOS2 → 20.20.20.20  
  - NXOS3 → 30.30.30.30  
  - NXOS4 → 40.40.40.40  

- **Underlay IP Fabric Links:**  
  - NXOS1 ↔ NXOS3 → 1.1.1.0/24  
  - NXOS1 ↔ NXOS4 → 2.2.2.0/24  
  - NXOS2 ↔ NXOS3 → 3.3.3.0/24  
  - NXOS2 ↔ NXOS4 → 4.4.4.0/24  

- **VLANs & Hosts:**  
  - **VLAN 10:**  
    - VPC5 (10.0.0.1/24) → NXOS1  
    - VPC7 (10.0.0.2/24) → NXOS2  
  - **VLAN 20:**  
    - VPC6 (20.0.0.1/24) → NXOS1  
    - VPC8 (20.0.0.2/24) → NXOS2  

---

## Configuration Overview

### Underlay (IP Fabric)
- OSPF or IS-IS is configured to provide reachability between loopback interfaces.  
- Spine switches (NXOS3, NXOS4) serve as **Route Reflectors** in the EVPN control plane.  
- All links between Leafs and Spines are pure Layer-3 connections.

### Overlay (VXLAN EVPN)
- **VTEP** functionality enabled on NXOS1 and NXOS2 using `interface nve1` with source Loopback0.  
- **VLAN-to-VNI mapping** is defined:  
  - VLAN 10 → VNI 10100  
  - VLAN 20 → VNI 10200  
- **BGP EVPN (MP-BGP)** runs across all devices:  
  - Leafs peer with Spines  
  - Spines act as BGP Route Reflectors  
- **EVPN Route Types:**  
  - **Type-2:** MAC/IP advertisement  
  - **Type-3:** Inclusive Multicast (BUM traffic handling)

---

## Advanced Features
- **Distributed Anycast Gateway** to provide L3 gateway redundancy across Leaf switches.  
- **MP-BGP EVPN** to advertise MAC/IP bindings dynamically.  
- **Multi-tenancy Support** via VRFs and separate VNIs.  

---

## Verification
- `show bgp l2vpn evpn summary` → check BGP EVPN neighbors  
- `show nve peers` → verify VXLAN peer establishment  
- `ping` between VPC5 ↔ VPC7 and VPC6 ↔ VPC8 → test L2 VXLAN connectivity  
- `traceroute` to confirm traffic path across the underlay  

---

## Files
- The `.unl` topology file for EVE-NG is included in this repository.

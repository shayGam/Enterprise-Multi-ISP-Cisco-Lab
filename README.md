# Enterprise Multi-Site & Multi-ISP Network Architecture

![Network Topology](./topology.png)

## 📋 Overview
This project demonstrates a comprehensive, highly available, and secure enterprise network environment simulated in **EVE-NG**. The architecture integrates multi-site routing, redundancy protocols, dynamic ISP failover, Layer 2 security defenses, and secure WAN connectivity using Cisco IOS devices.

---

## 🏗️ Architecture & Key Features

### 🌐 Core & Edge Routing
- **Dynamic Routing Protocols**: Implemented **OSPF** for internal core routing and **eBGP** for external multi-homed ISP connections.
- **Interior Gateway Protocols**: Configured **EIGRP** across branch locations to support multi-protocol routing integration.
- **Multi-ISP Redundancy & NAT**: Configured Port Address Translation (**PAT**) combined with dynamic routing and policy routing to support multi-ISP failover and load balancing.

### 🛡️ Layer 2 & High Availability (HA)
- **Default Gateway Redundancy**: Configured **HSRP** and **VRRP** across core switches to eliminate single points of failure for host gateways.
- **Spanning Tree Protocol (STP)**: Implemented Rapid-PVST with **BPDU Guard** and **Root Guard** to prevent unauthorized bridge injection and loops.
- **Link Aggregation**: Configured LACP-based **EtherChannel** for high-bandwidth switch-to-switch interconnections.
- **Switchport Security**: Enforced Layer 2 defenses including **Port Security**, **DHCP Snooping**, and **Dynamic ARP Inspection (DAI)** to mitigate ARP spoofing and rogue DHCP servers.

### 🔒 WAN & Virtualization
- **Site-to-Site Tunnels**: Deployed **L2TPv3** WAN encapsulation and overlay tunnels for secure inter-site communications.
- **Virtual Routing & Forwarding**: Implemented **VRF-Lite** for traffic segmentation and multi-tenant environment isolation.

---

## 🛠️ Tools & Technologies Used
- **Simulator**: EVE-NG
- **Vendor Operating Systems**: Cisco IOS
- **Network Tools**: , Wireshark, PuTTY, DEBUG

---

## 📁 Repository Structure

```text
├── topology/               # Topologies, diagrams, and export files
│   └── topology.png        # Network topology screenshot
├── configs/                # Saved Cisco running configurations
│   ├── Core-SW1.txt
│   ├── Edge-Router1.txt
│   └── Branch-Router1.txt
└── README.md               # Project documentation

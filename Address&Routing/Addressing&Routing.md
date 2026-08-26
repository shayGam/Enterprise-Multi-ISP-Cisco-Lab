# Architecture and Topology Breakdown

## Headquarters Domain — AS600
**IGP:** OSPF for core internal routing between Core Distribution Switches and HQ Edge Router.

### VLAN and Subnet Plan
| VLAN | Subnet | Role / Description |
| :--- | :--- | :--- |
| **VLAN 10** | `192.168.10.0/24` | HQ Host 1 |
| **VLAN 20** | `192.168.20.0/24` | HQ Host 2 |
| **VLAN 30** | `192.168.30.0/24` | HQ Host 3 |
| **VLAN 100** | `192.168.100.0/24` | HQ DHCP Server |

---

## Branch Office Domain — AS601
**IGP:** EIGRP for internal routing within the branch distribution and access layers.

### VLAN and Subnet Plan
| VLAN | Subnet | Role / Description |
| :--- | :--- | :--- |
| **VLAN 10** | `192.168.110.0/24` | Branch Host 1 |
| **VLAN 20** | `192.168.120.0/24` | Branch Host 2 |
| **VLAN 30** | `192.168.130.0/24` | Branch Host 3 |
| **VLAN 101** | `192.168.101.0/24` | Branch DHCP Server |

---

### WAN & Overlay Point-to-Point Interconnects

| Segment / Link | IP Subnet | Allocation | Routing Domain |
| :--- | :--- | :--- | :--- |
| **HQ Link to ISP-1 (Primary)** | 50.50.50.0/30 | HQ: .2, ISP-2: .1 | eBGP (AS 600 ↔ AS 610) |
| **HQ Link to ISP-2 (Backup)** | 40.40.40.0/30 | HQ: .2, ISP-1: .1 | eBGP (AS 600 ↔ AS 620) |
| **Branch Link to ISP-2 (Primary)** | 20.20.20.0/30 | Branch: .2, ISP-2: .1 | eBGP (AS 601 ↔ AS 620) |
| **Branch Link to ISP-1 (Backup)** | 30.30.30.0/30 | Branch: .2, ISP-1: .1 | eBGP (AS 601 ↔ AS 610) |
| **DMVPN Tunnel 1 Overlay** | 172.16.1.0/24 | Hub: .1, Spoke: .2 |

---

## Secure WAN Overlay
* **DMVPN GRE Tunnel over IPsec:** Secure site-to-site connectivity interconnecting HQ Router and Branch Router over untrusted public ISP infrastructure.
* **Subnet:** `172.16.0.0/30`

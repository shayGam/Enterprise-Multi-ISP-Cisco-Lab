# Architecture and Topology Breakdown

## Headquarters Domain — AS600
**IGP:** OSPF for core internal routing between Core Distribution Switches and HQ Edge Router.

### VLAN and Subnet Plan
| VLAN | Subnet | Role / Description |
| :--- | :--- | :--- |
| **VLAN 10** | `192.168.10.0/24` | Data Host 1 |
| **VLAN 20** | `192.168.20.0/24` | Data Host 2 |
| **VLAN 30** | `192.168.30.0/24` | Data Host 3 |
| **VLAN 100** | `192.168.100.0/24` | Central Services HQ DHCP Server |

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

## Secure WAN Overlay
* **DMVPN GRE Tunnel over IPsec:** Secure site-to-site connectivity interconnecting HQ Router and Branch Router over untrusted public ISP infrastructure.
* **Subnet:** `172.16.0.0/30`

# 🛠️ Network Troubleshooting: Asymmetric Routing & NAT State Conflict

## 📋 Problem Description
During the implementation of redundancy and load balancing between the Distribution/Core layer and the HQ/Edge router, **Equal-Cost Multi-Path (ECMP)** was enabled via the dynamic routing protocol.

As a result, internal traffic (e.g., ICMP pings targeting the router interface `10.0.0.1`) experienced **Asymmetric Routing**:
* **Outbound path:** Packets exited via interface `Ethernet0/0`.
* **Inbound path:** Return packets (Echo Reply) arrived via interface `Ethernet0/1`.

Because **Stateful NAT Overload** (`ip nat inside`) was configured on both Core-facing interfaces, Cisco IOS dropped the asymmetric return traffic due to a missing translation state entry for the second interface.

---

## 🔍 Root Cause Analysis (RCA)

1. **NAT State Inspection:**
   * Running `show ip nat translations` confirmed active PAT entries for ICMP, but returning packets arriving on the secondary interface failed state lookup and were dropped.
2. **Routing Table Verification:**
   * Executing `show ip route` revealed two equal-cost paths to internal subnets via interfaces `e0/0` and `e0/1`.
3. **Cisco IOS Order of Operations:**
   * Traditional Cisco IOS NAT (`ip nat inside/outside`) binds state enforcement to specific interface pairs. Asymmetric pathing invalidates the expected state lookup on ingress.

---

## 💡 Mitigations & Solutions Applied

### 1. Lab Workaround: OSPF ECMP Suppression
* **Implementation:** Configured `maximum-paths 1` under the OSPF routing process.
* **Result:** Forced the router to install a single active route in the RIB, eliminating asymmetry.
* **Architectural Note:** Suitable for lab/testing environments only. Disabled in production due to lack of link load sharing.

### 2. EIGRP Optimization (Active/Standby Pathing)
* **Implementation:** Adjusted link metric by increasing interface delay on the secondary link:
  ```cisconetconf
  interface Ethernet0/0
   delay 1000

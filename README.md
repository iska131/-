# CCNA Troubleshooting Lab: Comprehensive Network Recovery (31 Fixes)

## Project Overview
This project involved a deep-dive audit and recovery of a broken multi-site network. The infrastructure relies on **Router-on-a-Stick**, **EtherChannel**, and **DHCP**. I identified and resolved 31 specific configuration failures to restore full site-to-site connectivity.

---

## Detailed Troubleshooting Log (All 31 Issues)

### Layer 1: Physical & Interface Connectivity
1.  **Router0:** Re-enabled `GigabitEthernet 0/0` (administratively down).
2.  **Switch0:** Restored `FastEthernet 0/1` after manual shutdown.
3.  **Switch0:** Restored `GigabitEthernet 0/1` connectivity.
4.  **Switch1:** Enabled `GigabitEthernet 0/2` to restore link.
5.  **Switch0(1):** Fixed manual shutdown on `FastEthernet 0/3`.
6.  **Router0(1):** Re-enabled sub-interface `GigabitEthernet 0/0.30`.
7.  **Switch0(1):** Resolved `Port-Channel 1` failure, restoring member interfaces `Gig0/1` and `Gig0/2`.

### Layer 2: VLANs & Trunking
8.  **Router0:** Corrected encapsulation mismatch on `Gig0/0.10` (`dot1q 100` -> `10`).
9.  **Router0:** Fixed encapsulation on `Gig0/0.30` (`dot1q 31` -> `30`).
10. **Switch0:** Created missing `VLAN 30` in the database.
11. **Switch0:** Fixed `Fa0/3` trunk allowed list (removed invalid VLANs 11/400, added 10/20/30/40).
12. **Switch0/1 Trunk:** Optimized `PO1` to allow only necessary `VLAN 30, 40` (VLAN Pruning).
13. **Switch1:** Deleted invalid `VLAN 300`.
14. **Switch1:** Removed `FastEthernet 0/3` from incorrect `VLAN 300` assignment.
15. **Switch1:** Reassigned `FastEthernet 0/2` to the correct VLAN (moved from 40).
16. **Switch1:** Created missing `VLAN 30` and assigned proper access ports.
17. **Switch0(1):** Created missing `VLAN 30` and `VLAN 40`.
18. **Switch0(1):** Fixed `Fa0/3` trunk to include missing `VLAN 30` and `VLAN 40`.
19. **Switch0(1):** Restricted `PO1` trunk to necessary `VLAN 30, 40` only.
20. **Switch1(1):** Corrected trunk allowed list (removed 10/20, added 30/40).
21. **Switch1(1):** Reassigned `VLAN 30` from `Fa0/2` to correct port `Fa0/1`.
22. **Switch1(1):** Removed phantom `VLAN 400` and cleaned up `Fa0/1`.
23. **Switch1(1):** Assigned missing `Fa0/2` to `VLAN 40` to restore host access.
24. **STP:** Deployed `Spanning-tree Portfast` on all access ports to prevent DHCP timeouts.

### Layer 3: Routing & IP Addressing
25. **Router0:** Corrected IP on `Gig0/0.30` (fixed `192.168.60.254` mismatch).
26. **Router0:** Fixed IP on `Gig0/0.40` (corrected `192.169.40.254` typo).
27. **Router0(1):** Fixed IP on `Gig0/0.20` (`172.16.20.244` -> `172.16.20.254`).
28. **Router0(1):** Corrected `Gig0/0.40` IP from `192.168.x.x` range to proper `172.16.40.254`.
29. **Static Routing:** Removed invalid static route on Router0(1) pointing to unreachable `10.10.10.3`.

### DHCP Services
30. **Router0:** Added missing `default-router` gateway to the DHCP pool for `VLAN 40`.
31. **Router0(1):** Created entirely missing DHCP pools for `VLAN 10` and `VLAN 40`.

---

**Verification:** Full site-to-site connectivity restored. Tested via cross-vlan pings and DHCP binding checks.

**Engineer:** Iskender

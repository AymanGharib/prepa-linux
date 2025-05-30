
---

## **1. Concepts of STP (Spanning Tree Protocol)**

### What is STP and why is it important?

* **Network Redundancy**: To ensure reliability, networks often have redundant paths (multiple routes between devices). However, these redundant paths can cause problems.
* **Switching Loops**: If multiple paths exist, Ethernet frames can loop indefinitely because Layer 2 frames don't have a TTL (Time To Live) like IP packets.
* **Broadcast Storms**: The looping frames multiply, causing network congestion and possibly total network failure.
* **MAC Table Instability**: Switches learn MAC addresses dynamically. Loops cause frames to arrive on multiple ports, confusing MAC tables.
* **Resource Consumption & Instability**: Excess traffic overloads switches and reduces network performance.

### How does STP solve these problems?

* STP builds a **loop-free logical topology** called a "spanning tree".
* It **blocks redundant links** that could cause loops but keeps them ready to be activated if the primary link fails.
* This ensures **redundancy without loops**.

### STP origin and placement:

* Developed by Radia Perlman (1985).
* Standardized as IEEE 802.1D.
* Operates at **Layer 2 (Data Link Layer)**.
* Manages network link topology.

---

## **2. Variants of STP**

| Protocol           | Description                                               | Convergence Speed | CPU & Memory Usage |
| ------------------ | --------------------------------------------------------- | ----------------- | ------------------ |
| **STP (802.1D)**   | Original IEEE standard, single root bridge for entire LAN | Slow              | Low                |
| **PVST+ (Cisco)**  | Cisco variant, elects root per VLAN                       | Slow              | High               |
| **RSTP (802.1w)**  | IEEE standard, faster convergence than STP                | Fast              | Medium             |
| **PVRST+ (Cisco)** | Cisco Rapid PVST+, faster than PVST+                      | Fast              | Very high          |

---

## **3. How STP Works (Main Steps)**

### 1. Election of the Root Bridge

* The switch with the **lowest Bridge ID** becomes the **Root Bridge**.
* **Bridge ID** = Bridge Priority (default 32768) + MAC Address.
* If priorities tie, lowest MAC wins.
* The Root Bridge is the central reference point of the topology.

### 2. Path Cost Calculation

* Each switch calculates the **shortest path to the Root Bridge** based on link costs.
* Link cost depends on speed (e.g., 10 Mbps = 100, 100 Mbps = 19, 1 Gbps = 4, 10 Gbps = 2).
* The path with the lowest cumulative cost to the Root Bridge is preferred.

### 3. Port Roles and States

* **Root Port (RP)**: The port on a switch with the lowest cost path to the Root Bridge.
* **Designated Port (DP)**: The port on a LAN segment that has the best path to the Root Bridge, responsible for forwarding traffic.
* **Blocked Port**: Ports not forwarding traffic to prevent loops.

### 4. Port States

* **Blocking**: No data frames forwarded, only BPDU listening.
* **Listening**: Listening for BPDUs to determine topology.
* **Learning**: Learning MAC addresses but not forwarding frames.
* **Forwarding**: Forwarding data frames normally.
* **Disabled**: Administratively disabled port.

### 5. BPDU (Bridge Protocol Data Units)

* Switches exchange BPDUs regularly to maintain topology and elect the root.
* BPDUs carry Bridge ID and priority info.

---

## **4. STP Behavior**

* STP constantly monitors links.
* If an active link fails, STP recalculates the topology and activates a previously blocked link to maintain connectivity without loops.
* This dynamic behavior maintains network stability.

---

## **5. Best Practices**

* Manually set the **Root Bridge** for better topology control.
* Adjust **priority values** to influence root election.
* Enable **PortFast** on ports connected to end devices for faster startup.
* Use **BPDU Guard** to prevent rogue switches from altering topology.
* Use **Loop Guard** and **Root Guard** to prevent topology changes and protect the root bridge.

---

## **6. Key Commands for STP Configuration and Verification**

* **Show spanning-tree**
  Displays current spanning tree status, including root bridge and port states.

* **spanning-tree vlan \[ID] root primary**
  Configure switch to become the primary root bridge for the VLAN.

* **spanning-tree vlan \[ID] root secondary**
  Configure as secondary root bridge in case primary fails.

* **spanning-tree vlan \[ID] priority \[value]**
  Set switch priority for root bridge election (lower value = higher priority).

* **spanning-tree cost \[value]**
  Manually set the cost of a port (affects path selection).

* **show spanning-tree interface \[interface ID]**
  Show STP status on a specific interface.

* **show running-config | include span**
  Show all STP-related config lines.

* **no spanning-tree vlan \[vlan-id]**
  Disable STP on a specific VLAN.

---

# Summary

* **STP** prevents Layer 2 loops in redundant Ethernet networks by electing a root bridge and blocking redundant paths.
* It uses **Bridge IDs** (priority + MAC) to elect the root and port roles.
* Ports transition through different states before forwarding data to ensure loop-free topology.
* STP recalculates the tree dynamically if links go down.
* Variants (RSTP, PVST+) improve convergence times and VLAN-specific spanning trees.
* Cisco offers extended versions (PVST+, PVRST+).
* Proper configuration and verification commands help manage STP.

---

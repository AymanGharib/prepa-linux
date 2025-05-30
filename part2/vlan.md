
---

# Summary and Explanation of the Document (VLANs, VTP, and Related Concepts)

---

## 1. **Network Basics and Problems in LANs**

* A **LAN (Local Area Network)** is a network where all devices belong to the same **broadcast domain**. Broadcasts sent by one device are received by all others.
* Issues in LANs:

  * **Collisions** — when two devices transmit simultaneously.
  * **Latency** — delays caused by network devices.
  * **Broadcast storms** — excessive broadcast traffic.
  * **Security concerns** — e.g., anyone can sniff broadcast traffic.

---

## 2. **Solutions to LAN Problems: VLANs and Routing**

* **Router between LANs**: Blocks broadcasts and filters packets but is costly and introduces latency.
* **Virtual LANs (VLANs)**: Create logical network segments to improve performance and security without new physical hardware.

---

## 3. **What is a VLAN?**

* A **VLAN (Virtual Local Area Network)** is a logical segmentation of a physical LAN.
* VLANs allow grouping machines logically, regardless of their physical location.
* VLANs reduce broadcast traffic and enhance security by isolating groups.
* VLANs are standardized by IEEE:

  * **802.1Q** — VLAN tagging
  * **802.1p** — Quality of Service (QoS)
  * **802.1v** — Classification by Protocol and Port

---

## 4. **VLAN Functioning on Switches**

* Without VLANs, a switch considers all ports in one broadcast domain.
* With VLANs, ports are grouped logically into VLANs — a switch can have multiple broadcast domains.
* VLANs improve performance by limiting broadcast scope and enhance security by isolating traffic.

---

## 5. **Types of VLANs**

* **Port-Based VLAN (Level 1 VLAN)**: Ports on switches are statically assigned to VLANs.

  * Simple to implement.
  * If a device moves to another port, VLAN assignment must be reconfigured.
* **MAC Address-Based VLAN (Level 2 VLAN)**: VLAN assignment is based on MAC addresses.

  * Allows devices to move physically without reconfiguration.
  * Requires maintaining a MAC-to-VLAN mapping table.
  * More flexible but complex to manage.
* **IP-Based VLAN (Level 3 VLAN)**: VLAN assignment based on IP addresses or protocols.
* VLAN management complexity can be reduced by protocols like VMPS (VLAN Membership Policy Server).

---

## 6. **VLAN Tagging (802.1Q)**

* When VLANs span multiple switches, frames must be tagged to indicate their VLAN.
* **Untagged VLANs**: Frames are not tagged if confined to a single switch port (access port).
* **Tagged VLANs**: Frames carry VLAN ID tags (on trunk ports) to travel across switches.
* VLAN tag consists of 4 bytes added into the Ethernet frame:

  * **TPID (Tag Protocol Identifier)** — usually 0x8100
  * **Priority** (3 bits) for QoS
  * **CFI** (1 bit) for compatibility
  * **VLAN ID (VID)** (12 bits) — identifies VLAN number (up to 4096 VLANs)

---

## 7. **Trunk Links**

* **Trunk links** carry traffic for multiple VLANs between switches or between a switch and a router.
* Trunk ports carry **tagged frames** to identify VLANs.
* Allow VLANs to be extended across multiple switches.
* Example: Switches S1, S2, S3 connected by trunks carrying VLANs 10, 20, 30, 99.
* Without trunks, VLANs can’t be effectively implemented across multiple switches.

---

## 8. **VLAN Configuration Commands (Cisco IOS style)**

* **Create VLAN:**

  ```
  vlan <vlan-id>
  name <vlan-name>
  exit
  ```

* **Assign a switch port to a VLAN (access port):**

  ```
  interface <interface-id>
  switchport mode access
  switchport access vlan <vlan-id>
  exit
  ```

* **Set port to trunk mode (to carry multiple VLANs):**

  ```
  interface <interface-id>
  switchport mode trunk
  switchport trunk allowed vlan <vlan-list>
  exit
  ```

* **Show VLANs configured:**

  ```
  show vlan brief
  ```

* **Remove VLAN from a switch:**

  ```
  no vlan <vlan-id>
  ```

* **Reset port VLAN assignment:**

  ```
  interface <interface-id>
  no switchport access vlan
  ```

---

## 9. **VLAN Trunking Protocol (VTP)**

* VTP is a Cisco proprietary protocol to manage VLAN configurations across switches automatically.
* VTP propagates VLAN configuration changes from one switch to others.
* Works only for VLANs in the "normal" range (1-1005).
* VLAN configurations stored in **vlan.dat** file in switch Flash memory.
* VLANs in the extended range (1006-4094) are not handled by VTP and saved in running-config.

---

## 10. **VLAN Advantages**

* **Performance**: Reduces unnecessary broadcast traffic.
* **Security**: Separates sensitive data groups.
* **Cost savings**: More efficient bandwidth use.
* **Mobility**: With MAC-based VLANs, users can move without reconfiguration.
* **Manageability**: Groups with similar needs can be managed collectively.
* **Quality of Service (QoS)**: Prioritize traffic by VLAN.

---

# Summary of Important Concepts and Commands

| Concept / Command          | Explanation / Use                                                                                          |
| -------------------------- | ---------------------------------------------------------------------------------------------------------- |
| VLAN                       | Logical segmentation of LAN into separate broadcast domains                                                |
| VLAN Tag (802.1Q)          | 4-byte header added to frames to identify VLANs on trunk links                                             |
| Access Port                | Switch port assigned to a single VLAN, untagged frames                                                     |
| Trunk Port                 | Port that carries multiple VLANs using tagged frames                                                       |
| VLAN Ranges                | Normal VLAN IDs 1-1005 (stored in vlan.dat, handled by VTP); Extended 1006-4094 (stored in running-config) |
| Cisco VLAN Config Commands | `vlan <id>`, `switchport access vlan <id>`, `switchport mode trunk`                                        |
| Show VLANs                 | `show vlan brief`                                                                                          |
| Remove VLAN                | `no vlan <id>`                                                                                             |
| VTP                        | Protocol to sync VLAN config among Cisco switches                                                          |
| VMPS                       | Server to dynamically assign VLANs by MAC address                                                          |

---

# Wrap-up

The document is a detailed lecture note on VLANs and network segmentation using Cisco-style configuration, highlighting the **problems with flat LANs**, the **concept of VLANs**, **types of VLANs**, **VLAN tagging**, **trunk ports**, and the **Cisco VLAN configuration commands**.

It also covers the **VTP protocol** for VLAN management and best practices to assign and remove VLANs and ports.

---


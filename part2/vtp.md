
---

# VTP (VLAN Trunking Protocol) — Explanation, Concepts, Commands, and Configurations

### What is VTP?

* **VTP** is a Cisco proprietary protocol designed to simplify VLAN management across multiple switches.
* It allows **centralized VLAN management** by synchronizing VLAN configurations automatically across all switches in a VTP domain.
* Without VTP, VLANs must be manually created on each switch, which is error-prone and time-consuming, especially in large networks.

### Why use VTP?

* It solves the challenge of managing VLANs on many switches.
* Ensures **configuration consistency** for VLANs.
* Reduces human error.
* Provides centralized control for adding, deleting, and renaming VLANs.

---

### Key Concepts of VTP

1. **VTP Domains**

   * A VTP domain is a group of switches sharing the same VTP configuration (domain name).
   * Switches in the same VTP domain share VLAN configuration information automatically.

2. **VTP Modes**

   * **Server**: Can create, modify, and delete VLANs. Sends VLAN updates to other switches.
   * **Client**: Receives VLAN updates from servers, but cannot create or change VLANs.
   * **Transparent**: Does not participate in VLAN synchronization but forwards VTP messages; VLANs must be configured manually locally.

3. **VTP Versions**

   * VTPv1: Basic VLAN management, supports normal VLAN range (1-1005).
   * VTPv2: Adds support for Token Ring VLANs and improves stability.
   * VTPv3: Supports extended VLAN range (1006-4094), enhanced security, protection against accidental VLAN deletion.

4. **VTP Advertisements (Messages)**

   * VTP servers send periodic announcements about VLAN configurations to clients.
   * Types of messages:

     * **Summary advertisements**: Basic domain and revision number info.
     * **Subset advertisements**: Details of VLANs added or removed.
     * **Request advertisements**: Requests from clients for VLAN info.

5. **Revision Number**

   * A 32-bit number that increments with each VLAN configuration change on a server.
   * Helps switches determine which VLAN info is the most recent.
   * If a switch receives a message with a higher revision number, it updates its VLAN database accordingly.

6. **Security**

   * VTP uses an MD5 hash to verify integrity of updates.
   * Passwords can be configured to protect against unauthorized VLAN updates.
   * However, a misconfigured switch with a higher revision number can overwrite VLANs, so care must be taken.

---

### How VTP Works (Summary)

* A **VTP Server** switch manages VLANs. When VLANs are added/removed/renamed, the revision number increases.
* The server sends VTP messages via VLAN trunk links using IEEE 802.1Q or Cisco ISL encapsulation.
* **VTP Clients** receive these updates and synchronize their VLAN databases automatically.
* **Transparent mode** switches forward VTP messages but do not apply changes.

---

### Example VTP Configuration Commands (Cisco CLI)

#### On a Switch to configure VTP Server mode with domain and password:

```
Switch(config)# vtp domain LSI
Switch(config)# vtp mode server
Switch(config)# vtp password MonMotDePasse
```

#### To configure VTP Client mode:

```
Switch(config)# vtp domain LSI
Switch(config)# vtp mode client
Switch(config)# vtp password MonMotDePasse
```

#### To configure Transparent mode:

```
Switch(config)# vtp mode transparent
```

---

### Verification Commands

* To check the VTP status on a switch:

```
Switch# show vtp status
```

* To see VTP counters and statistics:

```
Switch# show vtp counters
```

---

### Best Practices with VTP

* Use **VTP version 3** for better security and extended VLAN support.
* Always configure a **VTP password** to protect VLAN info.
* Put non-essential switches or those needing manual VLAN config in **transparent mode**.
* Before adding a new switch, check its **revision number** to avoid overwriting VLANs accidentally.
* Regularly backup your VLAN configurations.
* Be careful with revision numbers because a wrong update can delete VLANs network-wide.

---

### Important Technical Details

* VTP messages are sent inside Ethernet frames using multicast address **01-00-0C-CC-CC-CC**.
* VTP uses MD5 hashing on domain name, revision number, VLAN config, and a secret key for integrity.
* VLAN IDs supported vary by VTP version:

  * Normal VLANs: 1-1005 (supported by VTPv1 and v2)
  * Extended VLANs: 1006-4094 (supported by VTPv3 only)

---

# Summary

**VTP** is a powerful tool for VLAN management in Cisco networks, automating VLAN synchronization and reducing errors, but it requires careful configuration, monitoring, and security measures.

---


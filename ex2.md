
---

# Exam: Network Switching Protocols (STP, VLAN, VTP)

---

## Part 1: QCM — Spanning Tree Protocol (STP)

1. What problem does STP solve in Ethernet networks?
   A) IP address conflicts
   B) Switching loops causing broadcast storms
   C) Slow DNS resolution
   D) Packet fragmentation

2. Which device is elected as the Root Bridge in STP?
   A) The switch with the highest MAC address
   B) The switch with the lowest Bridge ID (priority + MAC)
   C) The switch with the most ports
   D) The switch with the highest IP address

3. What is the default Bridge Priority value in STP?
   A) 0
   B) 32768
   C) 65535
   D) 4096

4. Which STP port state forwards data frames?
   A) Blocking
   B) Listening
   C) Learning
   D) Forwarding

5. What type of BPDU message is used to elect the root bridge?
   A) Hello BPDU
   B) Topology Change Notification BPDU
   C) Root Bridge Advertisement BPDU
   D) Configuration BPDU

6. Which STP variant offers faster convergence than the original 802.1D?
   A) PVST+
   B) RSTP (802.1w)
   C) PVRST+
   D) Both B and C

7. What is the function of the PortFast feature?
   A) Prevents loops on trunk ports
   B) Immediately puts a port into forwarding state
   C) Blocks rogue BPDUs
   D) Increases BPDU timers

---

## Part 2: QCM — VLANs

1. What is the main benefit of using VLANs in a network?
   A) Increases IP address space
   B) Segments a physical LAN into logical broadcast domains
   C) Improves wireless signal strength
   D) Replaces routers

2. What IEEE standard defines VLAN tagging?
   A) 802.3
   B) 802.1Q
   C) 802.11
   D) 802.1X

3. What type of port carries traffic for multiple VLANs?
   A) Access port
   B) Trunk port
   C) Aggregation port
   D) Loopback port

4. What VLAN ID is typically reserved for the native VLAN on Cisco switches?
   A) VLAN 1
   B) VLAN 10
   C) VLAN 100
   D) VLAN 4094

5. Which VLAN type is NOT handled by VTP?
   A) Normal VLANs (1-1005)
   B) Extended VLANs (1006-4094)
   C) Voice VLANs
   D) Management VLANs

6. Which command assigns a switch port as an access port in VLAN 20?
   A) `switchport mode trunk`
   B) `switchport access vlan 20`
   C) `vlan 20`
   D) `interface vlan 20`

---

## Part 3: QCM — VLAN Trunking Protocol (VTP)

1. What is the primary function of VTP?
   A) To encrypt VLAN traffic
   B) To synchronize VLAN configuration across switches
   C) To route traffic between VLANs
   D) To monitor bandwidth usage

2. Which VTP mode allows a switch to create, modify, and delete VLANs?
   A) Client
   B) Server
   C) Transparent
   D) Off

3. What happens if a switch receives a VTP advertisement with a higher revision number than its own?
   A) It ignores the advertisement
   B) It overwrites its VLAN database with the advertisement
   C) It resets the revision number to zero
   D) It shuts down its trunk ports

4. What security feature can you enable to prevent unauthorized VLAN changes via VTP?
   A) BPDU Guard
   B) VTP Password
   C) Root Guard
   D) Port Security

5. Which VTP version supports extended VLAN ranges (1006-4094)?
   A) VTPv1
   B) VTPv2
   C) VTPv3
   D) All versions

---

## Part 4: Use Case Scenarios

---

### Use Case 1: STP Troubleshooting

**Scenario:**
In a redundant switch network, users report intermittent network outages. Upon investigation, you suspect switching loops causing broadcast storms.

**Questions:**

* What commands would you run to identify the root bridge and blocked ports?
* How can you manually set a preferred switch as the root bridge?
* What STP features help prevent accidental loops from user ports?
* How would enabling PortFast affect end devices connected to switches?
* What is the impact of disabling STP on a VLAN?

---

### Use Case 2: VLAN Configuration and Troubleshooting

**Scenario:**
A network has multiple VLANs configured across three switches using trunks. Hosts in VLAN 10 cannot communicate with hosts in VLAN 10 on another switch.

**Questions:**

* What commands help verify VLAN assignments and trunk status?
* How do you check if VLAN 10 is allowed on the trunk links?
* What could cause VLAN traffic to be dropped between switches?
* How would you configure a port to be an access port in VLAN 10?
* What are benefits and drawbacks of using VLANs?

---

### Use Case 3: VTP Configuration and Security

**Scenario:**
A new switch is added to an existing VTP domain. After connecting, all VLAN configurations disappear from the network.

**Questions:**

* What might have caused the VLANs to disappear?
* How does VTP revision number affect VLAN synchronization?
* How can you prevent accidental overwrites caused by VTP?
* What is the difference between VTP server, client, and transparent modes?
* How would you configure a switch to be in transparent mode?

---

Sure! Here are the detailed answers and explanations for all the QCM questions and the use case scenarios.

---

# Part 1: STP QCM Answers

1. **B)** Switching loops causing broadcast storms
2. **B)** The switch with the lowest Bridge ID (priority + MAC)
3. **B)** 32768
4. **D)** Forwarding
5. **A)** Hello BPDU
6. **D)** Both B and C (RSTP and PVRST+ are faster)
7. **B)** Immediately puts a port into forwarding state

---

# Part 2: VLAN QCM Answers

1. **B)** Segments a physical LAN into logical broadcast domains
2. **B)** 802.1Q
3. **B)** Trunk port
4. **A)** VLAN 1
5. **B)** Extended VLANs (1006-4094)
6. **B)** `switchport access vlan 20`

---

# Part 3: VTP QCM Answers

1. **B)** To synchronize VLAN configuration across switches
2. **B)** Server
3. **B)** It overwrites its VLAN database with the advertisement
4. **B)** VTP Password
5. **C)** VTPv3

---

# Part 4: Use Case Answers

---

### Use Case 1: STP Troubleshooting

* **Commands to identify root bridge and blocked ports:**

  ```bash
  show spanning-tree
  show spanning-tree interface [interface-id]
  ```

  These commands show the root bridge info, port roles, and which ports are blocked.

* **Manually setting a preferred switch as root bridge:**
  Set a lower priority value on that switch:

  ```bash
  spanning-tree vlan [id] priority 4096
  ```

  (Lower priority has higher chance to be root.)

* **STP features to prevent loops from user ports:**

  * **PortFast:** Places ports directly into forwarding, avoiding delay on end devices.
  * **BPDU Guard:** Shuts down ports if BPDUs are received (prevent rogue switches).
  * **Root Guard:** Protects root bridge position.

* **Effect of enabling PortFast:**
  Speeds up port transition to forwarding, ideal for access ports connected to end devices; prevents network outages caused by STP delays.

* **Impact of disabling STP on VLAN:**
  Risk of switching loops causing broadcast storms, network instability, and outages.

---

### Use Case 2: VLAN Configuration and Troubleshooting

* **Commands to verify VLAN assignments and trunk status:**

  ```bash
  show vlan brief
  show interfaces trunk
  ```

* **Check if VLAN 10 is allowed on trunk links:**

  ```bash
  show interfaces trunk
  ```

  Look for VLAN 10 in the "Vlans allowed and active in management domain" list.

* **Possible causes of VLAN traffic drops between switches:**

  * VLAN 10 not allowed on trunk ports.
  * Trunk misconfiguration (wrong encapsulation).
  * VLAN not created on one or more switches.
  * Native VLAN mismatches causing untagged frame drops.

* **Configure a port as access port in VLAN 10:**

  ```bash
  interface [interface-id]
  switchport mode access
  switchport access vlan 10
  ```

* **Benefits and drawbacks of VLANs:**
  *Benefits:*

  * Segmentation reduces broadcast domains.
  * Improved security and performance.
  * Easier management of groups.
    *Drawbacks:*
  * Requires proper trunk and VLAN management.
  * Misconfiguration can cause connectivity issues.
  * Complexity increases in large networks.

---

### Use Case 3: VTP Configuration and Security

* **Cause of VLANs disappearing after adding new switch:**
  The new switch had a higher VTP revision number with no VLANs configured, causing all switches to overwrite their VLAN databases and delete VLANs.

* **How VTP revision number affects VLAN synchronization:**
  Switches accept VLAN info with the highest revision number, overwriting older databases.

* **Prevent accidental overwrites in VTP:**

  * Reset revision number on new switches before connecting.
  * Use **VTP transparent mode** on non-server switches to avoid syncing.
  * Use **VTP passwords** for authentication.
  * Regularly backup VLAN configs.

* **Difference between VTP modes:**

  * **Server:** Can create, modify, and delete VLANs; advertises changes.
  * **Client:** Receives VLAN info; cannot make VLAN changes.
  * **Transparent:** Forwards VTP messages but does not sync VLAN database; VLANs configured locally.

* **Configure switch to transparent mode:**

  ```bash
  Switch(config)# vtp mode transparent
  ```

---

If you'd like, I can also prepare practical labs, config examples, or flashcards based on these!

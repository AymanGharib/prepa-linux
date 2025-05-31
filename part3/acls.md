

---

# Concise Notes on ACL (Access Control Lists) in Network Administration

### 1. What is an ACL?

* ACL = Access Control List.
* Used to **control network traffic** by permitting or denying packets based on rules.
* Can apply to **source/destination IP addresses, protocols, and ports**.
* In Linux: ACLs also mean file permission extensions (not the focus here).

### 2. Why use ACLs?

* To **secure networks** by restricting unauthorized access.
* To **filter traffic** entering or leaving an interface.
* To **prevent attacks** and control bandwidth.
* To **segment networks** and isolate sensitive zones.
* To **enforce organizational security policies**.

### 3. Types of ACLs

* **Standard ACLs**: filter only by source IP address.
* **Extended ACLs**: filter by source/destination IP, protocol (TCP/UDP/ICMP), source/destination ports.
* **Named ACLs**: same as standard or extended but managed by name (more flexible and readable).

### 4. Numbering ranges for ACLs

* Standard ACLs: 1–99, 1300–1999
* Extended ACLs: 100–199, 2000–2699

### 5. How ACLs work

* Evaluated **top-down**, first matching rule applies.
* Implicit "deny all" at the end (everything else blocked if not permitted).
* Can be applied **inbound** or **outbound** on router interfaces.
* Inbound ACLs filter before routing; outbound after routing.

### 6. Important ACL components

* **Wildcard masks**: Used in IP matching, '0' means bit must match, '1' means bit ignored.
* **Ports**:

  * Well-known (0–1023): HTTP(80), SSH(22), FTP(21)
  * Registered (1024–49151): MySQL(3306)
  * Dynamic (49152–65535): temporary client ports

### 7. Examples of ACL use cases

* Block specific host access (e.g., deny TCP from 192.168.1.10).
* Restrict protocol access (e.g., deny HTTP traffic to a server).
* Allow traffic from trusted networks only.
* Control access to services like FTP, Telnet.

### 8. Cisco IOS commands basics

* Create standard ACL:
  `access-list [number] permit|deny [source IP] [wildcard mask]`
* Create named ACL:

  ```
  ip access-list standard|extended [name]
  permit|deny ...
  ```
* Apply ACL to interface:
  `interface [name]`
  `ip access-group [ACL number or name] in|out`
* Show ACLs: `show access-lists`
* Remove ACL: `no access-list [number]`

### 9. Difference between Router and Firewall

* Router: routes packets between networks, limited security filtering.
* Firewall: dedicated to filtering and protecting network traffic based on rules.
* Modern devices may combine both functions (e.g., NGFW, UTM devices).

---


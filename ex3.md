Certainly! Below is a full exam-style package covering **ACL, DNS, NFS, and Samba** based on your provided notes. It includes:

* Multiple-choice questions (QCM)
* Use case scenarios for practical understanding
* Answers and explanations

---

# Exam: Network Services & Security — ACL, DNS, NFS, Samba

---

## Part 1: QCM — Access Control Lists (ACL)

1. What is the main purpose of an ACL in networking?
   A) Encrypt data packets
   B) Filter network traffic by permitting or denying packets
   C) Assign IP addresses
   D) Route packets between networks

2. Which ACL type can filter by source and destination IP, protocol, and ports?
   A) Standard ACL
   B) Extended ACL
   C) Named ACL
   D) Wildcard ACL

3. How are ACLs evaluated on a router?
   A) Bottom-up, last matching rule applies
   B) Top-down, first matching rule applies
   C) Random order
   D) By port number

4. What does a wildcard mask of 0.0.0.255 mean in ACL?
   A) Match the first 3 octets exactly, ignore last octet
   B) Match any IP address
   C) Match last octet exactly, ignore first 3 octets
   D) Match none

5. Which Cisco IOS command applies an ACL inbound on an interface?
   A) `ip access-group 101 out`
   B) `ip access-list 101 in`
   C) `ip access-group 101 in`
   D) `access-list 101 in`

---

## Part 2: QCM — Domain Name System (DNS)

1. What is the primary function of DNS?
   A) Translate IP addresses to MAC addresses
   B) Map domain names to IP addresses
   C) Manage DHCP leases
   D) Secure web traffic

2. How many root DNS servers exist globally?
   A) 7
   B) 13
   C) 26
   D) 50

3. What is **anycast** routing used for in DNS?
   A) To route packets to a single destination
   B) To distribute queries to multiple root server replicas
   C) To encrypt DNS traffic
   D) To provide DNS redundancy only within a single LAN

4. What is BIND9 used for?
   A) As a DHCP server
   B) As an FTP server
   C) As a DNS server implementation
   D) As a firewall software

5. Which port does DNS typically use?
   A) 53 UDP/TCP
   B) 80 TCP
   C) 443 TCP
   D) 22 TCP

---

## Part 3: QCM — NFS (Network File System)

1. NFS primarily operates at which OSI layer?
   A) Network Layer
   B) Application Layer
   C) Data Link Layer
   D) Transport Layer

2. What is the default port for NFS version 4?
   A) 2049
   B) 111
   C) 139
   D) 445

3. Which NFS version introduced strong security features like Kerberos?
   A) NFSv2
   B) NFSv3
   C) NFSv4
   D) NFSv1

4. Why should NFS generally not be exposed directly to the internet?
   A) It uses UDP which is slow
   B) It lacks encryption and authentication by default
   C) It only works on Windows
   D) It is incompatible with Linux

5. How does NFS client access remote files?
   A) By FTP transfer
   B) By mounting remote filesystem locally
   C) Through a web interface
   D) Using SMB protocol

---

## Part 4: QCM — Samba (SMB Server)

1. What protocol does Samba implement for file sharing?
   A) FTP
   B) NFS
   C) SMB/CIFS
   D) HTTP

2. Which Samba daemon handles file and printer sharing?
   A) smbd
   B) nmbd
   C) winbindd
   D) samba

3. What command adds a user to Samba’s password database?
   A) `adduser`
   B) `smbpasswd -a [username]`
   C) `useradd`
   D) `passwd [username]`

4. Which version of Samba supports Active Directory domain controller features?
   A) Samba 2.x
   B) Samba 3.x
   C) Samba 4.x
   D) Samba 1.x

5. What major vulnerability affected SMBv1 on Windows?
   A) Heartbleed
   B) EternalBlue
   C) Shellshock
   D) POODLE

---

## Part 5: Use Case Scenarios

---

### Use Case 1: ACL Implementation to Secure a Network

**Scenario:**
You need to configure a Cisco router to block all incoming HTTP (port 80) traffic from a specific IP address 192.168.10.50 but allow all other traffic.

**Questions:**

* Write a standard ACL to deny only that IP.
* Write an extended ACL to deny HTTP traffic from that IP but allow other traffic.
* How do you apply the ACL inbound on interface GigabitEthernet0/1?
* Why is ACL order important in configuration?

---

### Use Case 2: DNS Server Setup and Troubleshooting

**Scenario:**
A company sets up a BIND9 DNS server for their internal network. Users report some domain names don’t resolve correctly.

**Questions:**

* What files are important for BIND zone configuration?
* How do you check the status of the DNS server?
* Which command tests DNS resolution from a client?
* What common errors in zone files cause resolution failures?
* How can you secure your DNS server?

---

### Use Case 3: NFS Mount Failure

**Scenario:**
A Linux client cannot mount a remote NFS share hosted on another server.

**Questions:**

* What commands would you use to verify the NFS server status and exports?
* How do you check network connectivity?
* Which logs do you check for errors?
* What NFS version mismatch issues might occur?
* How to secure NFS shares on a LAN?

---

### Use Case 4: Samba File Share Access Denied

**Scenario:**
Windows clients fail to access a Samba share configured on a Linux server.

**Questions:**

* What Samba configuration file controls share permissions?
* How do you check Samba service status?
* What command verifies Samba users?
* How to synchronize Linux user accounts with Samba?
* How to protect Samba shares against EternalBlue?

---

# Answers & Explanations

---

## Part 1: ACL Answers

1. B) Filter network traffic by permitting or denying packets
2. B) Extended ACL
3. B) Top-down, first matching rule applies
4. A) Match the first 3 octets exactly, ignore last octet
5. C) ip access-group 101 in

---

## Part 2: DNS Answers

1. B) Map domain names to IP addresses
2. B) 13
3. B) To distribute queries to multiple root server replicas
4. C) As a DNS server implementation
5. A) 53 UDP/TCP

---

## Part 3: NFS Answers

1. B) Application Layer
2. A) 2049
3. C) NFSv4
4. B) It lacks encryption and authentication by default
5. B) By mounting remote filesystem locally

---

## Part 4: Samba Answers

1. C) SMB/CIFS
2. A) smbd
3. B) smbpasswd -a \[username]
4. C) Samba 4.x
5. B) EternalBlue

---

## Part 5: Use Case Answers

---

### Use Case 1: ACL Implementation

* **Standard ACL to deny IP 192.168.10.50:**

  ```
  access-list 10 deny 192.168.10.50 0.0.0.0
  access-list 10 permit any
  ```

* **Extended ACL to deny HTTP from IP 192.168.10.50:**

  ```
  access-list 100 deny tcp host 192.168.10.50 any eq 80
  access-list 100 permit ip any any
  ```

* **Apply ACL inbound:**

  ```
  interface GigabitEthernet0/1
  ip access-group 100 in
  ```

* **ACL order importance:**
  ACLs are processed top-down; the first matching rule is applied. Put more specific deny rules before general permits.

---

### Use Case 2: DNS Server

* **Important BIND files:**
  `/etc/bind/named.conf`, zone files usually in `/var/cache/bind/` or `/etc/bind/zones/`

* **Check DNS status:**

  ```
  systemctl status bind9
  ```

* **Test DNS resolution:**

  ```
  dig example.com
  nslookup example.com
  ```

* **Common zone file errors:**
  Syntax errors, missing SOA or NS records, incorrect TTL values.

* **Securing DNS:**
  Use DNSSEC, restrict recursive queries, run on secure hosts, limit zone transfers.

---

### Use Case 3: NFS Mount

* **Verify server status and exports:**

  ```
  systemctl status nfs-server
  exportfs -v
  ```

* **Check network connectivity:**

  ```
  ping nfs_server_ip
  showmount -e nfs_server_ip
  ```

* **Check logs:**
  `/var/log/syslog`, `/var/log/messages`

* **Version mismatch:**
  Client and server NFS versions must match or be compatible.

* **Secure NFS:**
  Use firewalls, restrict exports to trusted IPs, use Kerberos authentication.

---

### Use Case 4: Samba Access Denied

* **Samba config file:**
  `/etc/samba/smb.conf`

* **Check service status:**

  ```
  systemctl status smbd
  ```

* **Verify Samba users:**

  ```
  pdbedit -L
  ```

* **Synchronize Linux and Samba users:**

  ```
  smbpasswd -a username
  ```

* **Protect against EternalBlue:**
  Patch Windows clients, disable SMBv1, use firewalls to block SMB ports (139, 445).

---

If you want, I can help you create detailed labs or flashcards for memorizing these concepts!

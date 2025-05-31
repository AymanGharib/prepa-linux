

---




### Main Topics Covered:

1. **Overview of Key Network Services under Linux:**

   * FTP, Telnet, SSH servers
   * Apache HTTP server
   * VPN solutions like OpenVPN
   * Network configurations: VLAN, VTP, STP
   * ACL (Access Control Lists)
   * SNMP protocol for supervision
   * NFS and Samba file servers
   * DNS server (BIND9)
   * OpenLDAP for directory services, authentication, and service centralization
   * Print servers

---

### Focused Sections on NFS and Samba:

#### NFS (Network File System)

* **History and Purpose:**
  Developed by Sun Microsystems in 1984, NFS allows remote file system access over a network, mostly used on Unix/Linux systems. It operates at the application layer of OSI using RPC (Remote Procedure Call).

* **Versions:**

  * Versions 1 & 2: Early versions, not secure, use UDP.
  * Version 3: Supports TCP but still with basic security and stateless design.
  * Version 4 (and 4.x): Major rewrite introducing:

    * Single configurable TCP port (default 2049) improving firewall compatibility.
    * Stronger security: negotiation of security levels, Kerberos 5, SPKM, LIPKEY4, encryption options.
    * Compatibility with Unix, Windows, Mac.
    * Use of UTF-8 for file names.
    * Updates in versions 4.1 and 4.2 with RFC publications.

* **Security Note:**
  NFS is mainly designed for local networks and should not be used directly over the internet unless via VPN due to security concerns.

* **How NFS Works:**
  Client requests files/directories using RPC calls. The server checks file availability and permissions. The file system is mounted remotely, allowing clients to access files as if local, including caching and file locking.

---

#### Samba (SMB Server under Linux)

* **Purpose:**
  Samba is a free software suite that implements the SMB/CIFS protocol, allowing Linux/Unix systems to share files and printers with Windows clients, as well as acting as an Active Directory Domain Controller since version 4.

* **Components:**

  * `samba`: AD Domain Controller daemon.
  * `smbd`: Handles file and printer sharing.
  * `nmbd`: Manages NetBIOS name resolution.
  * `winbindd`: Maps Windows SIDs to Linux UIDs for authentication.

* **Installation & User Management:**

  * Install Samba with `apt-get install samba`.
  * User accounts must be added and synchronized between Linux and Samba.
  * Commands like `smbpasswd -a user` to add users.
  * Reload configuration with `sudo service smbd reload`.

* **Configuration:**

  * Main configuration file is `/etc/samba/smb.conf`.
  * Example provided to share a photos folder allowing guest access and write permissions.
  * Comments in `smb.conf` are denoted by `#` or `;`.

* **Versions:**

  * Samba 3.x: Older, supports NT4-style domain controllers.
  * Samba 4.x: Current, supports full Active Directory features including DNS, GPOs, replication.

* **Security Advisory:**

  * EternalBlue vulnerability affects SMBv1 on Windows.
  * It allows remote code execution without authentication.
  * Protection involves patching (MS17-010), disabling SMBv1, and firewall rules.

---

### Comparison SMB vs NFS:

* Both use client-server model for file sharing.
* Both allow CRUD operations on remote files.
* SMB is native to Windows, supports a wider range of network resource sharing beyond files (printers, storage, VMs).
* NFS is native to Unix/Linux, mainly for file/directory sharing.
* SMB allows client-to-client communication via the server; NFS is strictly client-server.
* SMB requires Samba on Linux to interoperate with Windows shares.

---

### Other Topics Briefly Mentioned:

* The document also lists other Linux server services such as FTP, Telnet, SSH, Apache, VPN, DNS (BIND9), OpenLDAP, and print servers.
* VLAN, VTP, and STP protocols for network configuration.
* SNMP protocol overview for network supervision.

---

### Summary:

This PDF is a thorough teaching document about Linux network administration services focusing especially on file sharing protocols NFS and Samba. It explains their history, technical operation, versions, security considerations, installation, configuration, and practical usage. It also discusses the critical SMBv1 vulnerability known as EternalBlue and compares the SMB and NFS protocols in terms of features and typical use cases.

---


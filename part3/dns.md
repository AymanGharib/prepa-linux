
---

### 1. Domain Name System (DNS) Overview

* **Definition:** DNS is a protocol at layer 7 (application layer) of the OSI model.
* **Purpose:** It is a distributed system that maps domain names (human-readable addresses) to IP addresses (machine-readable).
* **Importance:** Since the early Internet (\~1985), DNS has been essential for navigating the Internet by resolving domain names to IPs and vice versa.
* **Key Point:** Without DNS servers, users would have to memorize IP addresses for every site, which is impractical. DNS servers store these mappings.
* **Typical use:** By default, Internet connections use DNS servers provided by the ISP, usually assigned automatically via DHCP.

---

### 2. DNS Hierarchy

* The DNS namespace is hierarchical, with the **root** at the top, represented by a dot (`.`).
* Domains can have **subdomains**, which may be delegated to other DNS servers.
* This hierarchy allows distributed management of domain information and scalability.

---

### 3. Root DNS Servers

* There are **13 root DNS servers** managed by 12 organizations worldwide (7 in the US, 2 in Europe, 1 in Japan).
* These root servers are replicated globally using **anycast** routing for redundancy and load distribution. Over 200 physical servers exist across 50 countries serving these root zones.
* Each root server has a letter name (e.g., `a.root-servers.org` to `m.root-servers.org`).
* Example usage: Server `k.root-servers.org` can handle up to 100,000 queries per second.
* The root servers' IP addresses are hard-coded in DNS resolvers and updated infrequently to maintain stability.
* Examples of public DNS servers: Google Public DNS (8.8.8.8), OpenDNS (208.67.222.222).

---

### 4. Private DNS (Local DNS)

* A **private DNS** service is used inside local networks (home or enterprise) to resolve local hostnames to IP addresses.
* This allows devices within a LAN to communicate by name instead of IP, which eases administration and improves usability.

---

### 5. BIND9 (Berkeley Internet Name Domain)

* **BIND9** is the most widely used open-source DNS server software on Linux and Unix systems.
* It implements DNS services, including hosting DNS zones and resolving queries.
* Originated from BSD UNIX at Berkeley, with development by Internet Systems Consortium since 1994.
* Default DNS server on many Linux distributions (including Ubuntu).
* Current version at the time of the document is **9.18.27 (May 15, 2024)**.
* The presentation references practical work (TP) for installation and configuration.

---

### Summary

The file is essentially an educational presentation that introduces DNS:

* Explains what DNS is, why it's important for Internet function.
* Describes the DNS hierarchical structure and root servers.
* Covers the distinction between global DNS and private/local DNS.
* Presents BIND9 as the standard Linux DNS server software with historical context and version info.

---


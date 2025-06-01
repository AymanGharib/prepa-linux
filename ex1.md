
---

### Use Case 1: Troubleshooting an FTP Server Issue

**Scenario:**
A company runs an FTP server with vsftpd on Linux to allow employees to upload and download files. Recently, users report that they can connect to the FTP server but fail to transfer files. Passive mode FTP is used due to client firewalls.

**Questions:**

* What steps would you take to troubleshoot this file transfer failure?
* What common misconfigurations or network issues could cause this problem?
* How would you verify if the passive mode port range is correctly configured and accessible?
* What security measures should be in place to protect the FTP server from unauthorized access?

---

### Use Case 2: Apache Web Server Performance and Security

**Scenario:**
An organization hosts a critical web application on an Apache HTTP server running on port 80. The application is slow and sometimes inaccessible from remote users. The server is also exposed on the public internet.

**Questions:**

* What steps can you take to diagnose and improve Apache’s performance?
* How would you enable HTTPS on the Apache server to secure data transmission?
* What Apache modules and settings would you review or enable to improve security?
* How can you restrict access to certain IP addresses or users in Apache?

---

### Use Case 3: Securing Remote Access with SSH

**Scenario:**
A system administrator notices multiple failed login attempts on a Linux server via SSH. The server currently allows root login and password authentication.

**Questions:**

* What immediate steps would you take to secure SSH access?
* How would you configure SSH to disallow root login and enable key-based authentication?
* What logs would you check to monitor suspicious SSH activity?
* How can tools like fail2ban help in securing SSH?

---

### Use Case 4: VPN Setup for Remote Office Connectivity

**Scenario:**
A company has two offices in different cities. They want to securely connect their internal networks over the Internet using a VPN.

**Questions:**

* What VPN protocol would you recommend (PPTP, L2TP/IPsec, OpenVPN, etc.) and why?
* What are the key configuration elements needed to set up a site-to-site VPN?
* How would you verify VPN connectivity and troubleshoot common issues?
* What security considerations are important for maintaining the VPN connection?

---

### Use Case 5: LDAP Directory Service Troubleshooting

**Scenario:**
Users report they cannot authenticate to the company’s network, which uses OpenLDAP for centralized authentication. Recent changes were made to the LDAP schema.

**Questions:**

* What troubleshooting steps would you follow to identify and fix authentication failures?
* How would you check if the LDAP server is reachable and responding correctly?
* How can LDAP logs and client error messages help diagnose issues?
* What security measures should be taken to protect LDAP authentication and data integrity?

---



---

# Use Case 1: Troubleshooting FTP Server Issue

**Scenario Recap:** Users connect to vsftpd FTP server but cannot transfer files; passive mode FTP is used.

---

### Troubleshooting Steps:

1. **Check vsftpd service status:**

   ```bash
   sudo systemctl status vsftpd
   ```

   Ensure the service is running.

2. **Verify vsftpd configuration:**

   * Confirm `pasv_enable=YES` in `/etc/vsftpd.conf`.
   * Check passive port range (`pasv_min_port` and `pasv_max_port`) is set (e.g., 40000-50000).
   * Ensure `listen=YES` or `listen_ipv6=YES` is properly set.

3. **Firewall Configuration:**

   * Confirm that TCP ports 21 and the entire passive port range are open on the server firewall (iptables, firewalld, ufw).
   * Check network firewalls or NAT devices for proper port forwarding.

4. **Test connectivity:**

   * Use `telnet ftp_server_ip 21` to test control connection.
   * Use `nmap` or `telnet` to test passive port availability.

5. **Examine logs:**

   * Review `/var/log/vsftpd.log` or `/var/log/xferlog` for errors.
   * Check kernel logs for firewall drops.

6. **Client Configuration:**

   * Verify FTP clients are set to passive mode.
   * Try with different FTP clients or command-line to isolate client-side issues.

---

### Common Causes:

* Firewall blocking passive ports.
* Incorrect vsftpd passive port range configuration.
* NAT/firewall does not support FTP protocol helpers or ALG.
* SELinux or AppArmor restrictions blocking connections.

---

### Security Measures:

* Disable anonymous FTP unless necessary.
* Use strong local user passwords.
* Restrict users to chroot jail (`chroot_local_user=YES`).
* Limit passive port range for firewall management.
* Enable logging to monitor activity.
* Consider using FTPS or SFTP instead of plain FTP.

---

# Use Case 2: Apache Web Server Performance and Security

**Scenario Recap:** Apache server slow and exposed to public internet.

---

### Performance Diagnosis and Improvement:

1. **Check resource usage:** CPU, memory, disk I/O on the server.
2. **Review Apache logs:** `/var/log/apache2/access.log` and `error.log` for errors or heavy requests.
3. **Enable caching modules:** e.g., `mod_cache`, `mod_deflate` for compression.
4. **Tune `KeepAlive` settings:** balance between performance and resource use.
5. **Optimize Apache worker settings:** `MaxRequestWorkers`, `StartServers`, etc.
6. **Use profiling tools:** like `ab` (ApacheBench) or `htop` for load testing.

---

### Enable HTTPS:

1. Install SSL module:

   ```bash
   sudo a2enmod ssl
   ```
2. Obtain SSL certificates (Let's Encrypt or commercial CA).
3. Configure virtual host for port 443 with SSL certificates.
4. Redirect HTTP to HTTPS.

---

### Security Modules and Settings:

* `mod_security`: Web application firewall.
* `mod_evasive`: Protects against DoS attacks.
* Disable directory listing (`Options -Indexes`).
* Use `.htaccess` or main config to restrict access by IP or user authentication.
* Keep Apache and OS updated.

---

### Access Restriction Example:

```apache
<Directory "/var/www/html/secure">
    Require ip 192.168.1.0/24
</Directory>
```

---

# Use Case 3: Securing Remote Access with SSH

**Scenario Recap:** Multiple failed login attempts; root login and password auth enabled.

---

### Immediate Security Steps:

1. **Disable root login:**
   Edit `/etc/ssh/sshd_config`:

   ```conf
   PermitRootLogin no
   ```

2. **Disable password authentication (enable key auth only):**

   ```conf
   PasswordAuthentication no
   ```

3. **Restrict users:** Use `AllowUsers` or `AllowGroups` to limit SSH access.

4. **Restart SSH:**

   ```bash
   sudo systemctl restart sshd
   ```

5. **Change SSH port (optional):** reduces automated attacks.

---

### Monitoring and Defense:

* Check `/var/log/auth.log` or `/var/log/secure` for suspicious activity.
* Install and configure **fail2ban** to ban IPs with repeated failures.
* Use **SSH keys** for authentication instead of passwords.

---

# Use Case 4: VPN Setup for Remote Office Connectivity

**Scenario Recap:** Connect two offices securely over the Internet.

---

### Recommended VPN Protocol:

* **OpenVPN** is preferred for strong security, flexibility, and cross-platform support.
* L2TP/IPsec is also an option but more complex. PPTP is insecure and discouraged.

---

### Key Configuration Elements:

* Assign static IPs or DNS names for VPN endpoints.
* Configure encryption parameters (certificates, keys).
* Define allowed subnets for routing between sites.
* Set up firewall rules to allow VPN traffic (e.g., UDP port 1194 for OpenVPN).

---

### Verification and Troubleshooting:

* Test tunnel with `ping` between subnets.
* Check VPN logs on both ends.
* Confirm firewall allows VPN traffic.
* Verify routing tables.

---

### Security Considerations:

* Use strong encryption (AES-256 recommended).
* Protect VPN credentials and keys.
* Regularly update VPN software.
* Monitor VPN connections and logs.

---

# Use Case 5: LDAP Directory Service Troubleshooting

**Scenario Recap:** Users fail to authenticate; recent schema changes made.

---

### Troubleshooting Steps:

1. **Verify LDAP server is running:**

   ```bash
   sudo systemctl status slapd
   ```

2. **Test LDAP connectivity:**

   ```bash
   ldapsearch -x -H ldap://server_ip -b "dc=example,dc=com"
   ```

3. **Check recent schema changes:**

   * Ensure schema files are correctly loaded and syntax is valid.
   * Revert changes if needed.

4. **Review logs:**

   * `/var/log/syslog` or `/var/log/slapd.log` for errors.
   * Client application logs for specific LDAP errors.

5. **Validate user entries:**

   * Confirm DN, attributes, and password hashes are correct.
   * Check if user accounts are not locked or expired.

---

### Security Measures:

* Use LDAPS (LDAP over SSL/TLS) to encrypt authentication.
* Restrict LDAP bind permissions.
* Use strong passwords and access control lists (ACLs).
* Regularly backup LDAP data.
* Monitor LDAP access and errors.

---


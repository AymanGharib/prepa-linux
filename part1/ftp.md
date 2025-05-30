
---

# Overview: FTP Server Administration with vsftpd (Linux)

---

### 1. **FTP Protocol Basics**

* **FTP (File Transfer Protocol)** is an application layer protocol designed to transfer files over TCP/IP networks.
* It allows users to copy, delete, or modify files on a remote machine.
* Originated in **1971**, originally with no security (data, including passwords, sent in plaintext).
* FTP uses **two TCP connections** per session:

  * **Control connection** on port **21** (commands & authentication)
  * **Data connection** on port **20** (actual file transfer)
* Two main FTP modes:

  * **Active mode**: Server connects back to client for data (requires client firewall to allow inbound connections).
  * **Passive mode**: Client initiates both control and data connections (better for clients behind NAT/firewalls).

---

### 2. **FTP Server vsftpd**

* **vsftpd** (Very Secure FTP Daemon) is the default FTP server on many Linux distros (Ubuntu, Debian, Kali, etc.).
* Supports anonymous FTP, virtual users, local users.
* Designed with security and performance in mind.

---

### 3. **Installing vsftpd**

Commands:

```bash
sudo apt-get install vsftpd
sudo service vsftpd start
sudo systemctl enable vsftpd.service  # Enable at startup
sudo systemctl start vsftpd.service   # Start service
sudo systemctl stop vsftpd.service    # Stop service
```

---

### 4. **Key Configuration Files**

* `/etc/vsftpd.conf` — main configuration file for vsftpd.
* `/etc/vsftpd.user_list` and `/etc/ftpusers` — files listing users denied FTP access.
* Directives in these files control vsftpd behavior.

---

### 5. **Important vsftpd.conf Directives**

**General daemon behavior:**

* `listen=YES` — run vsftpd in standalone mode.
* `listen_ipv6=YES` — use IPv6 (cannot be used with `listen=YES`).
* `session_support=YES` — enables PAM session support for authentication.

**Access control:**

* `anonymous_enable=YES|NO` — allow anonymous FTP users.
* `local_enable=YES|NO` — allow system (local) users to log in.
* `userlist_enable=YES|NO` — activate user list for blocking users.
* `userlist_file=/etc/vsftpd.user_list` — file with users blocked from login.
* `userlist_deny=YES|NO` — whether users in the list are denied (YES) or allowed only those in the list (NO).

**Anonymous user options:**

* `anon_root=/srv/ftp` — root directory for anonymous users.
* `anon_upload_enable=YES|NO` — allow anonymous upload.
* `anon_mkdir_write_enable=YES|NO` — allow anonymous users to create directories.
* `no_anon_password=YES|NO` — anonymous users don't need a password.
* `ftp_username=ftp` — local system user for anonymous FTP.

**Local user options:**

* `chroot_local_user=YES|NO` — restrict local users to their home directory (jail).
* `chroot_list_enable=YES|NO` — enable chroot for users in a list.
* `chroot_list_file=/etc/vsftpd.chroot_list` — file listing users affected by chroot.
* `local_root=/home/username` — home directory for local user.
* `local_umask=022` — default file permissions mask for new files.

**Directory listing:**

* `dirlist_enable=YES|NO` — enable directory listings.
* `dirmessage_enable=YES|NO` — show message when entering directory.
* `message_file=.message` — file containing directory message.
* `force_dot_files=YES|NO` — show hidden files starting with dot.
* `use_localtime=YES|NO` — show file times in local timezone.

**File transfer:**

* `download_enable=YES|NO` — allow file downloads.
* `write_enable=YES|NO` — allow write commands (upload, delete, rename).
* `chown_uploads=YES|NO` — uploaded files owned by specific user.
* `chown_username=root` — user to own uploaded files if above enabled.

**Logging options:**

* `xferlog_enable=YES|NO` — enable transfer log.
* `xferlog_file=/var/log/xferlog` — file for transfer logs.
* `vsftpd_log_file=/var/log/vsftpd.log` — default log file.
* `dual_log_enable=YES|NO` — enable dual logging (both formats).
* `log_ftp_protocol=YES|NO` — log FTP commands and responses.
* `syslog_enable=YES|NO` — send logs to system log instead of file.
* `xferlog_std_format=YES|NO` — use standard wu-ftpd log format.

**Networking options:**

* `listen_address=IP` — IP address to listen on.
* `listen_port=21` — port to listen on.
* `max_clients=0` — max simultaneous clients (0 means unlimited).
* `max_per_ip=0` — max clients per IP.
* `connect_from_port_20=YES|NO` — use port 20 for active FTP data.
* `accept_timeout=60` — timeout for passive connection acceptance.
* `connect_timeout=60` — timeout for active mode client response.
* `data_connection_timeout=300` — timeout for data transfer inactivity.
* `ftp_data_port=20` — port for active data connection.
* `pasv_enable=YES|NO` — enable passive mode (YES by default).
* `pasv_min_port=0` / `pasv_max_port=0` — port range for passive connections.
* `pasv_address=IP` — external IP to advertise for passive FTP (useful behind NAT).
* `pasv_promiscuous=YES|NO` — disable IP checks on passive data connection.
* `port_enable=YES|NO` — enable active mode (YES default).

---

### 6. **Multiple Instances of vsftpd (Multi-homing)**

* To serve multiple FTP domains/IPs, run multiple vsftpd daemons, each with its own config file:

  * Assign IPs to interfaces.
  * Create config files like `/etc/vsftpd/vsftpd-site-2.conf`.
  * In each config, set unique `listen_address=IP`.
  * Run daemon with specific config:

    ```bash
    vsftpd /etc/vsftpd/vsftpd-site-2.conf &
    ```

* Customize each instance with directives such as:

  * `anon_root`
  * `local_root`
  * `vsftpd_log_file`
  * `xferlog_file`

---

### 7. **FTP Security Considerations**

* FTP transmits data and credentials in **plaintext**, so it's insecure over public networks.
* Safer alternatives:

  * **FTPS** (FTP over SSL/TLS): Adds encryption layers.
  * **SFTP** (SSH File Transfer Protocol): Secure file transfer over SSH, uses a single connection.
* Use **SFTP** or **FTPS** for secure file transfers.

---

### 8. **Basic FTP Client Commands**

Once connected to FTP server (via CLI or GUI):

* `pwd` — print working directory.
* `ls` or `dir` — list files.
* `cd <dir>` — change directory.
* `get <file>` — download file.
* `put <file>` — upload file.

---

### 9. **Other Concepts Mentioned**

* **Anonymous FTP** — allows access without user credentials (usually read-only).
* **User authentication** — vsftpd uses PAM and Linux system users by default.
* **User lists** — used to deny or allow users.
* **Chroot jail** — restricts users to their home directories for security.

---

### 10. **Example Basic vsftpd.conf**

```conf
listen=YES
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
chroot_local_user=YES
userlist_enable=YES
userlist_file=/etc/vsftpd.user_list
userlist_deny=YES
pasv_enable=YES
pasv_min_port=40000
pasv_max_port=50000
```

---

# Summary

The document teaches you how to install and configure a **secure vsftpd FTP server** on Linux with:

* Understanding FTP basics (ports, modes, connections).
* Installing and starting vsftpd service.
* Configuring access for anonymous and local users.
* Controlling user access via user lists.
* Setting directory permissions and user jail (chroot).
* Configuring networking, passive/active FTP modes and firewall considerations.
* Logging options for troubleshooting and auditing.
* Running multiple FTP instances for different IPs or domains.
* Awareness of FTP security issues and alternatives.

---


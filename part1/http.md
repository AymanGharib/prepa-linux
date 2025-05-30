
---

## 1. **Concepts: Web Servers and HTTP Protocol**

### What is a Web Server?

* A **web server** is either software or hardware that serves web resources (pages, images, videos, etc.) over a network.
* It listens for requests via the HTTP protocol and responds with the requested content.
* Web servers can serve **static** content (fixed files) or **dynamic** content (generated on demand).
* Web servers can run on the internet (public) or intranets (private networks).

### HTTP (Hypertext Transfer Protocol)

* HTTP is the foundational protocol of the web for transferring hypertext documents.
* It operates as a client-server protocol: browsers (clients) send requests, servers respond.
* Standard port for HTTP is **80**.
* Requests use methods like:

  * **GET** (retrieve data),
  * **HEAD** (retrieve headers only),
  * **POST** (send data to the server, e.g., form submission).

### HTTPS (HTTP Secure)

* HTTPS adds **TLS encryption** to HTTP to secure data transfer.
* Uses port **443**.
* Ensures confidentiality, data integrity, and authentication.
* Web browsers now strongly encourage HTTPS usage for all sites.

### HTTP Versions

* **HTTP/0.9 and 1.0**: Basic protocols with simple request/response, connection closes after each request.
* **HTTP/2**: Introduced multiplexing to improve speed; based on SPDY (Google).
* **HTTP/3**: Uses QUIC protocol over UDP, solving "head-of-line blocking" problems found in TCP-based HTTP/2.

---

## 2. **Common HTTP Servers**

* **Apache HTTP Server**: Widely used, open source, modular architecture.
* Other servers include IIS (Microsoft), Nginx, Google Web Server, Node.js-based servers, Gunicorn (Python), etc.

---

## 3. **Apache Web Server Details**

### Features:

* Written in C, portable mostly for Unix/Linux.
* Multi-process or multi-threaded daemon (httpd).
* Highly modular; features added via modules (e.g., mod\_ssl for HTTPS).
* Configuration via text files (httpd.conf and others).
* Default web directory: `/var/www/html`.

### Important Apache Modules:

* **mod\_speling**: Corrects URL typos.
* **mod\_ssl**: SSL/TLS support for HTTPS.
* **mod\_cgi**: Support for CGI scripts.
* **mod\_alias**: URL aliasing.
* Many other modules available for caching, rewriting, proxying, etc.

---

## 4. **Apache Installation on Kali Linux**

Commands to install Apache and Python 3 (for running simple HTTP servers):

```bash
sudo apt install apache2
sudo apt install python3
```

---

## 5. **Basic Apache Web Server Management**

### Using `systemctl` to control Apache service:

* Enable Apache to start on boot:

  ```bash
  sudo systemctl enable apache2
  ```
* Disable Apache on boot:

  ```bash
  sudo systemctl disable apache2
  ```
* Start Apache immediately:

  ```bash
  sudo systemctl start apache2
  ```
* Stop Apache immediately:

  ```bash
  sudo systemctl stop apache2
  ```

### Testing Apache

* After starting, open a browser and go to `http://localhost`.
* You should see the default Apache welcome page.

---

## 6. **Configuring Apache and Serving a Web Page**

### Default Document Root

* Apache serves files from `/var/www/html`.

### To serve your own HTML page:

1. Create an HTML file (e.g., index.html):

```bash
echo "Bonjour et bienvenu LSI2, ci apres Apache on Kali Linux" > index.html
```

2. Move it to Apache’s web directory:

```bash
sudo mv index.html /var/www/html/
```

3. Refresh your browser on `http://localhost` to see the new page.

---

## 7. **Running a Simple HTTP Server with Python 3**

If you want a quick test server (no Apache needed), use:

```bash
python3 -m http.server --bind 127.0.0.1 9000
```

* This starts a server bound to localhost on port 9000.
* Access via `http://127.0.0.1:9000`.

---

## Summary of Key Commands

| Purpose                       | Command                                        |
| ----------------------------- | ---------------------------------------------- |
| Install Apache                | `sudo apt install apache2`                     |
| Install Python 3              | `sudo apt install python3`                     |
| Start Apache service          | `sudo systemctl start apache2`                 |
| Stop Apache service           | `sudo systemctl stop apache2`                  |
| Enable Apache on boot         | `sudo systemctl enable apache2`                |
| Disable Apache on boot        | `sudo systemctl disable apache2`               |
| Run simple Python HTTP server | `python3 -m http.server --bind 127.0.0.1 9000` |
| Serve custom HTML file        | `sudo mv index.html /var/www/html/`            |

---

If you want, I can also help with the Apache configuration file (`httpd.conf`) details or with securing Apache using HTTPS and `mod_ssl`.

---


# Web Request Flow — THM

## Related Notes

This room directly connects with concepts previously studied in my Payloab_Fx repository:

- [B2 — Transport Layer & HTTP communication](https://github.com/op0912/Payloab_Fx/blob/main/B/B2_transport.md)

- [B3 — Services & Web communication](https://github.com/op0912/Payloab_Fx/blob/main/B/B3_Services.md)

- [B4 — Web Services / HTTP / HTTPS](https://github.com/op0912/Payloab_Fx/blob/main/B/B4_ports/Web%20Services.md)

Key concepts reconnected in this room:
- TCP connections
- HTTP requests/responses
- Port 80/443 communication
- DNS resolution flow
- Web server communication
- Frontend/Backend interaction
- Dynamic web behavior

## Context

This room connected multiple web concepts together into a complete request/response flow.

Main concepts explored:
- DNS resolution
- Firewalls / WAF
- Load Balancers
- Web Servers
- Virtual Hosts
- Static vs Dynamic content
- Backend scripting
- Database interaction
- Frontend rendering

---

# High-Level Web Request Flow

Simplified modern web flow:

```text
Browser Request
↓
Local DNS Cache
↓
Recursive DNS Resolver
↓
Root DNS Server
↓
Authoritative DNS Server
↓
IP Address Returned
↓
Firewall / WAF / CDN
↓
Load Balancer
↓
Port 80 / 443 Connection
↓
Web Server
↓
Backend Application
↓
Database
↓
Generated Response
↓
Browser Rendering
```

---

# DNS Resolution Understanding

When a user types a domain:
- browser checks local cache
- recursive DNS resolver performs lookup
- root/TLD/authoritative servers participate in resolution
- authoritative DNS server returns the IP address

Key understanding:
DNS resolves domain names into IP addresses.

---

# Firewall / WAF Understanding

A WAF (Web Application Firewall):
- sits between users and the website
- filters malicious requests
- may block attacks or bots
- may apply rate limiting

Key understanding:
Traffic may pass through security layers before reaching the real server.

---

# Load Balancer Understanding

Load balancers distribute requests between multiple backend servers.

Purpose:
- handle large traffic
- improve availability
- prevent server overload

Common balancing logic:
- Round Robin
- Weighted balancing

Health checks:
- periodic checks verify if backend servers are alive
- unhealthy servers stop receiving traffic

---

# Web Server Understanding

Web servers:
- listen on ports 80/443
- receive HTTP/HTTPS requests
- serve files/content to clients

Examples:
- Apache
- Nginx
- IIS
- NodeJS environments

Key understanding:
HTTP/HTTPS requires a service listening behind the port.

Example:
- browser sends GET request
- web server processes request
- server returns resources/files

---

# Root Directory Understanding

Web servers serve files from a root directory.

Examples:
- Linux Apache/Nginx:
```text
/var/www/html
```

- Windows IIS:
```text
C:\inetpub\wwwroot
```

Example request:

```text
http://example.com/picture.jpg
```

May map to:

```text
/var/www/html/picture.jpg
```

---

# Virtual Hosts Understanding

One web server can host multiple websites.

The browser automatically sends:

```http
Host: website.com
```

The web server reads the Host header and serves the correct website.

Example:

```text
Host: one.com
→ /var/www/website_one

Host: two.com
→ /var/www/website_two
```

Key understanding:
- multiple domains may share the same IP/server
- Host headers determine which site is served

---

# Static Content Understanding

Static content:
- does not change
- served directly from disk
- same response every time

Examples:
- images
- CSS
- JavaScript files
- static HTML

---

# Dynamic Content Understanding

Dynamic content:
- generated dynamically
- changes depending on:
  - user
  - search
  - database
  - backend logic

Examples:
- social media feeds
- search results
- account dashboards

Key understanding:
Backend systems generate content before sending it to the browser.

---

# Backend Scripting Understanding

Backend languages:
- PHP
- Python
- Ruby
- NodeJS
- Perl
- others

Purpose:
- process user input
- communicate with databases
- generate dynamic responses

Example:

```text
index.php?name=adam
```

Backend processes:
- parameter input
- server-side logic
- dynamic HTML generation

Browser only receives the final generated HTML.

Important understanding:
Backend code is NOT visible in page source.

---

# Database Understanding

Web applications often communicate with databases.

Purpose:
- store users
- store posts
- store permissions
- store application data

Flow:

```text
Browser
↓
Web Server
↓
Backend
↓
Database
```

The browser usually does NOT communicate directly with the database.

---

# Frontend Rendering Understanding

After processing:
- HTML
- CSS
- JavaScript

are sent to the browser.

The browser:
- builds the DOM
- applies CSS
- executes JavaScript
- renders the final page visually

---

# Important Global Understanding

Modern websites are NOT simple static pages.

They are complex systems composed of:
- DNS infrastructure
- security layers
- load balancing
- web servers
- backend applications
- databases
- frontend rendering systems

---

# Key Takeaways

- DNS resolves domains into IP addresses
- HTTP/HTTPS communicates with web servers
- Web servers listen on ports 80/443
- Multiple websites may share one IP using virtual hosts
- Static content is served directly
- Dynamic content is generated by backend logic
- Backend code is hidden from the client
- Databases store application data
- Browsers render the final frontend content
- Modern web infrastructure contains many intermediate layers

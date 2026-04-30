# DNS — TryHackMe + Real Notes

## Context

Linked to:  

Payloab_Fx — Block B (Network)

- [B1 — Basics](https://github.com/op0912/Payloab_Fx/blob/main/B/B1_basics.md)
- [B3 — Services](https://github.com/op0912/Payloab_Fx/blob/main/B/B3_Services.md)
- [B4 — Core Network Services](https://github.com/op0912/Payloab_Fx/blob/main/B/B4_ports/Core%20network%20services.md)

This section combines:
- TryHackMe DNS room
- Real testing on PowerShell

Goal:
Understand DNS behavior in real-world conditions, not just theory.

---

## DNS — Core Concept

DNS (Domain Name System) resolves domain names to IP addresses.

Example:
google.com → 142.x.x.x

---

## DNS Resolution Flow

1. Local cache (PC)
2. Router / gateway
3. Recursive resolver (ISP / public DNS like 8.8.8.8)
4. Root server (.)
5. TLD server (.com, .ca, etc.)
6. Authoritative server
7. Final IP returned

---

## Record Types

### A Record
- Resolves domain → IPv4
- Example:
  www.site.com → 10.10.10.10

---

### AAAA Record
- Resolves domain → IPv6

---

### CNAME Record
- Alias → points to another domain
- Requires another DNS lookup

Example:
shop.website.thm → shops.myshopify.com

---

### MX Record
- Defines mail servers for a domain

Example:
10 mail1  
20 mail2  

- Lower number = higher priority
- Mail is sent to the lowest available value first

---

### TXT Record
- Stores text-based data
- Used for:
  - domain verification
  - email security (SPF, DMARC)
  - configuration tokens

---

## Key Observations

### DNS is Dynamic
- Same domain can return multiple IPs
- Used for load balancing

---

### Reverse DNS
- IP → domain
- Not always configured
- Failure ≠ issue

---

### Search Domain Behavior
- Short names are auto-completed

Example:
shop → shop.website.thm

---

##  Real Tests (PowerShell)

### CNAME Resolution

**Command:**
Resolve-DnsName www.microsoft.com -Type CNAME

Result:
www.microsoft.com → www.microsoft.com-c-3.edgekey.net

Observation:
- Microsoft uses a CDN (Akamai)
- domain points to external infrastructure

---

### Authority Check (SOA)

**Command:**
Resolve-DnsName edgekey.net

Result:
PrimaryServer: ns1-2.akamai.com

Observation:
- edgekey.net is managed by Akamai
- confirms CDN usage

---

### A / AAAA Records

**Command:**
Resolve-DnsName akamai.com

Result:
- IPv4 → 104.119.189.x
- IPv6 → 2600:...

Observation:
- multiple IPs = load balancing
- IPv4 + IPv6 support

---

### Root Domain vs Subdomain

**Command:**
Resolve-DnsName microsoft.com

Result:
A / AAAA only

Command:
Resolve-DnsName www.microsoft.com

Result:
CNAME chain → Akamai → IP

Observation:
- root domain = direct IP (no CNAME allowed)
- subdomain = flexible (can use CNAME)

---

### CNAME Chain (Real Example)

www.microsoft.com  
→ edgekey.net  
→ akadns.net  
→ akamaiedge.net  
→ IP  

Observation:
- multiple redirections
- CDN selects optimal server

---

### Cloudflare Behavior

**Command:**
Resolve-DnsName www.chatgpt.com

Result:
- direct A / AAAA (no visible CNAME)
- IPs:
  - 104.18.x.x
  - 172.64.x.x

Observation:
- Cloudflare hides backend
- returns proxy IPs directly

---

### Reverse DNS Failure

**Command:**
nslookup 104.18.32.47

Result:
Non-existent domain

Observation:
- reverse DNS not configured
- normal behavior (especially CDN)

---

### IP Ownership (OSINT)

**Command:**
Invoke-RestMethod ipinfo.io/104.18.32.47

Result:
org: AS13335 Cloudflare, Inc.

Observation:
- IP belongs to Cloudflare
- confirms proxy layer

---

## CDN Concept

CDN = Content Delivery Network

Purpose:
- reduce latency
- distribute traffic
- improve availability

Examples:
- Akamai
- Cloudflare

---

## Important Rules

- Root domain (example.com) cannot be a CNAME
- Subdomains (www.example.com) can use CNAME
- Multiple IPs = normal behavior

---

## Tools Used

### nslookup
- manual DNS queries
- supports filtering by type

### Resolve-DnsName
- PowerShell DNS tool
- clearer output

### Invoke-RestMethod
- used for API calls (OSINT)
- helps identify IP ownership

---

## Practical Skills Gained

- identify DNS record types
- interpret DNS output
- recognize CDN usage
- differentiate proxy vs backend
- validate infrastructure using real commands

---

## Key Takeaways

- DNS is not static
- CNAME can chain multiple times
- CDN adds abstraction layers
- IP ≠ real target (proxy may exist)
- A → IPv4
- AAAA → IPv6
- CNAME → alias (triggers new lookup)
- MX → mail server (lowest value = highest priority)
- TXT → configuration / verification

Quick rules:
- Root domain ≠ CNAME
- Subdomain = flexible
- Multiple IPs = normal

---

## Mindset

Seeing an IP is not enough.

Always ask:
- who owns this IP?
- is it a proxy?
- what is behind it?

# Network Basics

## Context
This section is directly related to my main networking learning block:

Payloab_Fx — Block B: Network  
Link: https://github.com/op0912/Payloab_Fx/blob/main/B-network_Basics.md

These notes represent a simplified and applied introduction based on TryHackMe content.

---

## Session Overview

This session covered introductory offensive and defensive concepts, followed by core networking fundamentals.

---

## What Was Done

### 1. Basic Web Interaction (FakeBank)
- Interacted with a simple vulnerable web application
- Objective was to manipulate or extract data in a guided environment
- No real resistance or depth

This introduced basic application-layer interaction (Layer 7).

---

### 2. Logs & Security (Defensive)
- Viewed a firewall interface and logs
- Observed:
  - inbound vs outbound traffic
  - allow / deny rules
  - basic monitoring

This introduced a defensive perspective (monitoring and control).

---

### 3. Career Orientation
- Quiz suggested pentesting as a suitable path
- This aligns with the initial objective

---

## Networking Fundamentals

### Core Concepts

#### Internet & WWW
- Basic understanding of how devices communicate over the web

#### IP Address
- Logical identifier of a device
- IPv4 vs IPv6 (basic distinction)

#### MAC Address
- Physical identifier of a network interface

#### Octet
- 1 byte (8 bits)
- Used in IPv4 structure

Note: explained in detail in my Payloab_Fx repository (Block B):  
https://github.com/op0912/Payloab_Fx/blob/main/B/B1_basics.md

---

### Basic Interaction

#### MAC Manipulation (Lab)
- Changed Bob's MAC address to match Alice's
- Used to capture a simple flag

This demonstrates a basic identity spoofing concept.

---

### ICMP / Ping
- Used to test connectivity between devices
- Indicates:
  - reachability
  - latency

Note: ICMP / Ping is explained in detail in my Payloab_Fx repository (Block B):  
https://github.com/op0912/Payloab_Fx/blob/main/B/B1_basics.md

---

### Network Structure

#### Topologies (B13)
- Star topology (central switch)

#### Subnet (Introduction) (B11)
- Concept of dividing a network into smaller segments

---

### Core Protocols (Foundations)

#### ARP (Address Resolution Protocol)
- Maps IP to MAC
- Uses broadcast requests

This is foundational for local network communication.

---

#### DHCP
- Automatically assigns:
  - IP address
  - gateway
  - DNS

This gives a device its identity on a network.

Note: DHCP is explained in detail in my Payloab_Fx repository (Block B):  
https://github.com/op0912/Payloab_Fx/blob/main/B/B3%20Services.md

---

### OSI Model (Basic Awareness)

- Learned layer names without depth

Relevant layers (focus for now):
- Layer 7: Application
- Layer 4: Transport (ports, TCP/UDP)
- Layer 3: Network (IP)
- Layer 2: Data Link (MAC)

---

## Network Access & Exposure

### Port Forwarding (Basic Understanding)

Initial understanding:
- Not used inside LAN
- Used to expose services to the Internet

Refined understanding:
- Allows external traffic to reach an internal device through the router

---

## Security Concepts (Introduction Only)

### Firewall
- Controls traffic (allow / deny)

Types:
- Stateless: rule-based filtering
- Stateful: tracks connections

Understanding remains high-level.

---

### VPN (Basic Understanding)

Initial understanding:
- Changes visible IP
- Uses an encrypted tunnel

Refined understanding:
- Creates a secure tunnel between a device and a remote network
- Traffic appears to originate from the VPN server

Protocols introduced:
- PPP (base concept)
- PPTP (older, weaker)
- IPSec (more secure)

Understanding is still incomplete.

---

### VLAN (Segmentation)

- Logical separation of networks
- Same physical switch, multiple isolated groups

Conceptual only at this stage, requires deeper study.

---

## Key Takeaways

- Devices are identified using IP and MAC
- Communication inside a LAN depends on ARP
- Networks are structured using switches and routers
- Traffic can be controlled and filtered (firewall)
- External access requires routing and forwarding (NAT / port forwarding)
- Security concepts are introduced but not yet mastered

---

## Current Level

- Understands concepts at a high level
- Can recognize network components and roles
- Lacks depth in protocols and mechanisms
- Not yet able to apply concepts confidently

---

## Next Step

Focus on strengthening understanding before moving further.

Priority areas:
- ARP (how resolution works step by step)
- OSI model (B6) — mapping concepts to layers
- Port forwarding vs NAT (clear distinction)
- VPN (how tunneling and encryption actually work)
- Firewall (B5) — difference between stateful and stateless in practice

Objective:
Build clear and precise understanding of each concept before applying them.

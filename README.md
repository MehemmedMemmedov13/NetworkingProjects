# NetworkingProjects
Cisco Packet Tracer projects focused on routing, switching, and network security

Each project folder contains a `.pkt` simulation file, a topology diagram, and its own `README.md` with full documentation.

---

## Projects

### 1. Intrusion Detection System (IDS)
> Folder: `Intrusion Detection System/`

A Network-based Intrusion Detection System (NIDS) implemented across three interconnected LANs. The IDS monitors inbound ICMP traffic on a Cisco 1941 router using IPS Signature 2004 and logs alerts to a dedicated SYSLOG server.

**Key concepts:** NIDS, IPS Signatures, SYSLOG, Dynamic Routing (RIP), CLI configuration

---

### 2. DHCP Configuration
> Folder: `DHCP configuration/`

Demonstrates automatic IP address assignment to network hosts using a **DHCP server**. Eliminates the need for manual static IP configuration across devices on a LAN.

**Key concepts:** DHCP Server, IP Address Leasing, Default Gateway, DNS Assignment

---

### 3. FTP File Server Connection
> Folder: `FTP File Server Connection/`

Sets up a **File Transfer Protocol (FTP) server** within a network, allowing hosts to upload and download files using authenticated user credentials.

**Key concepts:** FTP Server, User Authentication, File Transfer, Client-Server Model

---

### 4. Static and Default Routing (ISP)
> Folder: `Static and Default Routing(ISP)/`

Simulates an **ISP-style network** using static and default routing between multiple routers. Demonstrates how packets are forwarded across networks without dynamic routing protocols.

**Key concepts:** Static Routes, Default Routes, ISP Topology, Inter-network Communication

---

## Tools & Requirements

- **Simulator:** [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer)
- **OS Support:** Windows, macOS, Linux (Android/iOS also available)
- **Minimum Hardware:** Intel Pentium 4 @ 2.53GHz, 2GB RAM, 1GB free storage

---

## Getting Started

1. Install **Cisco Packet Tracer** from [Cisco NetAcad](https://www.netacad.com/)
2. Clone this repository:
   ```bash
   git clone https://github.com/MehemmedMemmedov13/NetworkingProjects.git
   ```
3. Open the `.pkt` file inside any project folder using Cisco Packet Tracer
4. Refer to the project's `README.md` for configuration details and commands

---

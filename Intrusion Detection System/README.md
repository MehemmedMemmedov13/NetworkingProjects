#  Intrusion Detection System (IDS) — Cisco Packet Tracer

A network-based Intrusion Detection System (NIDS) simulated using Cisco Packet Tracer, built as part of a Bachelor of Engineering project in Computer Science & Engineering at Chandigarh University.

---

##  Table of Contents

- [Overview](#overview)
- [Network Architecture](#network-architecture)
- [Devices & Components](#devices--components)
- [IP Addressing Scheme](#ip-addressing-scheme)
- [IDS Implementation](#ids-implementation)
- [Key CLI Commands](#key-cli-commands)
- [Results](#results)
- [Tools & Requirements](#tools--requirements)
- [Limitations](#limitations)
- [Future Work](#future-work)

---

## Overview

This project implements a **Network Intrusion Detection System (NIDS)** across three interconnected LANs using Cisco Packet Tracer. The IDS monitors incoming ICMP traffic on Router0 and logs any suspicious activity to a dedicated **SYSLOG server**.

The system uses **IPS Signature 2004** (ICMP Echo Request) to detect potential ping-based intrusions and alert administrators in real time via the SYSLOG server.

> This is an IDS (detection only), not an IPS — it alerts on suspicious traffic but does not block it.

---

## Network Architecture

Three LANs are connected via three **Cisco 1941 Routers** using dynamic routing (RIP).

```
[Network 1: 192.168.1.0/24]         [Network 3: 192.168.30.0/24]
        |                                       |
     Router0 -------- Router1 ----------- Router2
        |                                       |
  [HTTP Server]                        [Network 2: 192.168.10.0/24]
  100.50.0.0/24
```

---

## Devices & Components

| Device | Model | Quantity |
|---|---|---|
| Router | Cisco 1941 (2x GigE, 4x Serial) | 3 |
| Switch | Cisco 2960-24TT | 3 |
| Personal Computer | PC-PT | 9 |
| Laptop | Laptop-PT | 3 |
| SYSLOG Server | Server-PT | 1 |
| HTTP Server | Server-PT | 1 |
| FTP Server | Server-PT | 1 |
| Printer | Printer-PT | 2 |
| Smartphone | Smartphone-PT | 1 |
| Mobile Tower | Cell Tower (3G/4G) | 1 |

**Cables used:**
- Copper Straight-through (PC ↔ Switch, Switch ↔ Router)
- Serial DCE (Router ↔ Router)

---

## IP Addressing Scheme

### Network 1 — `192.168.1.0/24`
| Device | IP Address |
|---|---|
| PC0 | 192.168.1.2 |
| PC1 | 192.168.1.3 |
| PC2 | 192.168.1.4 |
| PC3 | 192.168.1.5 |
| SYSLOG Server | 192.168.1.6 |
| Printer0 | 192.168.1.7 |
| Default Gateway | 192.168.1.1 |

### Network 2 — `192.168.10.0/24`
| Device | IP Address |
|---|---|
| PC4–PC7 | 192.168.10.2–10.5 |
| Laptop0 | 192.168.10.6 |
| FTP Server | 192.168.10.6 |
| Printer1 | 192.168.10.7 |
| Default Gateway | 192.168.10.1 |

### Network 3 — `192.168.30.0/24`
| Device | IP Address |
|---|---|
| PC10 | 192.168.30.3 |
| Laptop2 | 192.168.30.2 |
| Smartphone1 | 192.168.30.4 |
| Default Gateway | 192.168.30.1 |

### WAN / Router Links (Class A)
| Interface | IP |
|---|---|
| Router0 GigE 0/1 | 100.50.0.1 |
| HTTP Server | 100.50.0.2 |
| Router0 ↔ Router1 (Serial) | 10.10.10.1 / 10.10.10.2 |
| Router1 ↔ Router2 (Serial) | 20.20.20.1 / 20.20.20.2 |

---

## IDS Implementation

The NIDS is applied on **Router0**, interface `GigabitEthernet0/0`, monitoring all inbound ICMP traffic entering Network 1.

**Signature used:**
```
2004 — ICMP Echo Request (Info, Atomic)
Triggers on IP protocol field = 1 (ICMP) and ICMP type field = 8 (Echo Request)
```

**Other available signatures:**
- `2001` — ICMP Host Unreachable
- `1101` — Unknown IP Protocol
- `2007` — ICMP Timestamp Request
- `3040` — TCP no flags set
- `3100` — Smail Attack

**Action configured:** `produce-alert` → logs to SYSLOG server at `192.168.1.6`

---

## Key CLI Commands

```bash
# Enter privileged mode and activate security package
enable
show version
license boot module c1900 technology-package securityk9
do reload

# Configure IDS
mkdir idsdir
ip ips config location idsdir
ip ips name myIDS

# Manage signature categories
ip ips signature-category
  category all
    retired true
  category ios_ips basic
    retired false

# Apply IDS rule to interface
interface GigabitEthernet0/0
  ip ips myIDS in

# Enable logging to SYSLOG server
logging on
logging host 192.168.1.6
service timestamps log datetime msec

# Configure specific signature
ip ips signature-definition
  signature 2004 0
    status
      enabled true
    engine
      event-action produce-alert
```

---

## Results

-  Successfully established connectivity across all 3 networks using dynamic routing
-  ICMP traffic from external hosts detected and logged by the IDS
-  SYSLOG server captured all IDS alert events in real time
-  HTTP server accessible from all hosts via `100.50.0.2`
-  FTP server operational with user authentication (`harsh` / `123`)

---

## Tools & Requirements

**Software:**
- [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer) (cross-platform)

**Minimum Hardware:**
- Intel Pentium 4 @ 2.53GHz or equivalent
- 2 GB RAM
- 1 GB free disk space
- Display resolution: 1024×768

**Supported OS:** Windows, macOS, Linux (also available on Android/iOS)

---

## Limitations

- Cannot analyse all traffic on a high-volume busy network
- Detects but **cannot prevent** attacks (detection only — use IPS for prevention)
- Limited compatibility with modern network hardware features
- Packet Tracer is a simulation tool and does not fully replicate real Cisco IOS

---

## Future Work

- Implement a **Honeypot System** alongside the IDS
- Upgrade to an **Intrusion Prevention System (IPS)** with `deny-packet-inline` action
- Simulate more attack types (SYN flood, DDoS, port scanning)
- Integrate with a real SIEM platform

---



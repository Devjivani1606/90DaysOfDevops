# 🌐 Network Communication Fundamentals (Day 3-4)

## Overview

In Day 1-2, we learned:

* Networks
* Routers
* Switches
* Packets
* IP Addresses

Now it's time to understand how devices actually communicate.

This section covers:

* MAC Addresses
* OSI Model
* TCP/IP Model
* ARP
* TCP vs UDP
* Ports
* Three-Way Handshake

These concepts form the foundation of:

* AWS Networking
* Docker Networking
* Kubernetes Networking
* API Communication
* Cloud Infrastructure

---

# How Does Data Travel?

Example:

```text
Laptop
   │
   ▼
Router
   │
   ▼
Internet
   │
   ▼
Google Server
```

Question:

How does the laptop know where to send data?

Answer:

Networking protocols help devices identify and communicate with each other.

---

# What is a MAC Address?

MAC = Media Access Control Address

Every network card has a unique hardware address.

Example:

```text
00:1A:2B:3C:4D:5E
```

Think of it as:

```text
IP Address = House Address

MAC Address = Person's Identity Card
```

---

## Properties of MAC Address

* Unique per Network Interface Card (NIC)
* Assigned by manufacturer
* Layer 2 Address
* Used inside local networks

Check MAC Address:

```bash
ip link
```

or

```bash
ifconfig
```

---

# IP Address vs MAC Address

| IP Address           | MAC Address               |
| -------------------- | ------------------------- |
| Logical Address      | Physical Address          |
| Can Change           | Usually Fixed             |
| Layer 3              | Layer 2                   |
| Used Across Networks | Used Within Local Network |

Example:

```text
IP  = 192.168.1.10
MAC = 00:1A:2B:3C:4D:5E
```

---

# OSI Model

OSI = Open Systems Interconnection Model

It explains how data moves through a network.

---

## 7 Layers of OSI

```text
7 Application
6 Presentation
5 Session
4 Transport
3 Network
2 Data Link
1 Physical
```

---

## Layer 7 - Application

User-facing applications.

Examples:

* Browser
* Gmail
* WhatsApp
* APIs

Protocols:

```text
HTTP
HTTPS
FTP
SMTP
DNS
```

---

## Layer 6 - Presentation

Responsible for:

* Encryption
* Compression
* Data Formatting

Examples:

```text
SSL/TLS
JPEG
JSON
```

---

## Layer 5 - Session

Creates and manages communication sessions.

Examples:

```text
User Login Session
Database Session
```

---

## Layer 4 - Transport

Responsible for:

* Reliability
* Flow Control
* Error Checking

Protocols:

```text
TCP
UDP
```

---

## Layer 3 - Network

Responsible for routing.

Uses:

```text
IP Addresses
```

Devices:

```text
Router
```

Protocols:

```text
IPv4
IPv6
ICMP
```

---

## Layer 2 - Data Link

Uses:

```text
MAC Addresses
```

Devices:

```text
Switch
```

Protocols:

```text
Ethernet
ARP
```

---

## Layer 1 - Physical

Actual transmission of bits.

Examples:

```text
Cables
Fiber
Wireless Signals
```

---

# Easy Way to Remember OSI

```text
Please
Do
Not
Throw
Sausage
Pizza
Away
```

Bottom → Top

---

# TCP/IP Model

Real-world networking uses TCP/IP.

---

## Layers

```text
Application
Transport
Internet
Network Access
```

Mapping:

```text
OSI Layer 7,6,5
        ↓
Application

OSI Layer 4
        ↓
Transport

OSI Layer 3
        ↓
Internet

OSI Layer 2,1
        ↓
Network Access
```

---

# What is ARP?

ARP = Address Resolution Protocol

Purpose:

Convert:

```text
IP Address
      ↓
MAC Address
```

Example:

```text
192.168.1.5
      ↓
00:1A:2B:3C:4D:5E
```

---

## Why ARP is Needed

A device knows:

```text
Destination IP
```

but needs:

```text
Destination MAC
```

before sending data.

ARP helps discover it.

---

## View ARP Table

```bash
arp -a
```

or

```bash
ip neigh
```

---

# TCP vs UDP

Transport Layer Protocols.

---

## TCP

TCP = Transmission Control Protocol

Features:

* Reliable
* Ordered Delivery
* Error Checking
* Connection Oriented

Examples:

```text
HTTP
HTTPS
SSH
FTP
```

---

## UDP

UDP = User Datagram Protocol

Features:

* Faster
* No Connection
* No Error Checking
* Lower Overhead

Examples:

```text
Video Streaming
Gaming
DNS
VoIP
```

---

## TCP vs UDP Comparison

| TCP                 | UDP                    |
| ------------------- | ---------------------- |
| Reliable            | Faster                 |
| Connection Oriented | Connectionless         |
| Error Checking      | Minimal Checking       |
| Slower              | Faster                 |
| HTTP, HTTPS, SSH    | DNS, Gaming, Streaming |

---

# What is a Port?

A port identifies a specific service running on a machine.

Example:

```text
IP Address = Building

Port = Apartment Number
```

---

# Common Ports

| Service | Port |
| ------- | ---- |
| HTTP    | 80   |
| HTTPS   | 443  |
| SSH     | 22   |
| FTP     | 21   |
| DNS     | 53   |
| SMTP    | 25   |

---

## View Open Ports

```bash
ss -tulnp
```

or

```bash
netstat -tulnp
```

---

# TCP Three-Way Handshake

Before TCP communication starts:

A connection must be established.

---

## Step 1

Client Sends:

```text
SYN
```

Meaning:

```text
Can we communicate?
```

---

## Step 2

Server Responds:

```text
SYN + ACK
```

Meaning:

```text
Yes, I am ready.
```

---

## Step 3

Client Sends:

```text
ACK
```

Meaning:

```text
Connection Established.
```

---

## Handshake Flow

```text
Client                     Server

SYN ---------------------->

      <---------------- SYN-ACK

ACK ---------------------->
```

Connection Established

---

# Practical Commands

Check Interfaces:

```bash
ip link
```

Check IP Address:

```bash
ip addr
```

Check ARP Table:

```bash
ip neigh
```

Check Open Ports:

```bash
ss -tulnp
```

Check Connectivity:

```bash
ping google.com
```

Trace Route:

```bash
traceroute google.com
```

---

# Practical Exercises

## Task 1

Find:

```bash
ip addr
```

Identify:

* Interface Name
* IP Address

---

## Task 2

View MAC Address:

```bash
ip link
```

---

## Task 3

View ARP Entries:

```bash
ip neigh
```

---

## Task 4

Check Open Ports:

```bash
ss -tulnp
```

Identify:

* SSH Port
* Running Services

---

# Key Concepts Learned

By the end of Day 3-4, I understand:

✅ MAC Address

✅ IP vs MAC Address

✅ OSI Model

✅ TCP/IP Model

✅ ARP

✅ TCP vs UDP

✅ Ports

✅ Three-Way Handshake

✅ Basic Network Troubleshooting Commands

---

# Revision Notes

```text
MAC Address → Device Identity

IP Address → Device Location

ARP → IP to MAC Mapping

TCP → Reliable Communication

UDP → Fast Communication

Port → Service Identifier
```

---

# Motivation Corner

> Every packet follows networking rules.

> Every cloud service depends on networking.

> Every DevOps engineer troubleshoots networks.

> Learn networking deeply, and infrastructure becomes easier to understand.

---

# Challenge Motto

```text
Understand Packets
        ↓
Understand Networking
        ↓
Understand Cloud
        ↓
Understand DevOps
```

🚀 One Packet at a Time.

🚀 One Protocol at a Time.

🚀 One Layer at a Time.

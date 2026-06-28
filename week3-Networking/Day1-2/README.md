# Networking Fundamentals for DevOps (Day 1-2)

## Overview

Networking is one of the most important skills for a DevOps Engineer.

Every cloud service, container, virtual machine, database, and application communicates through a network.

Before learning AWS VPCs, Kubernetes Networking, Load Balancers, and DNS, it is important to understand the fundamentals.

---

# What is a Network?

A network is a group of devices connected together to exchange data.

Examples:

* Computers
* Mobile Phones
* Servers
* Routers
* Printers

Simple Network:

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
Web Server
```

---

# Why Networking is Important in DevOps?

DevOps Engineers work with:

* Cloud Infrastructure
* Servers
* Databases
* APIs
* Containers
* Kubernetes Clusters

All of these communicate using networks.

Without networking knowledge:

* Troubleshooting becomes difficult
* Cloud architecture becomes confusing
* Kubernetes networking becomes difficult

---

# Types of Networks

## LAN (Local Area Network)

Small network inside:

* Home
* Office
* College

Example:

```text
Laptop
   │
   ├── WiFi Router
   │
Phone
```

---

## MAN (Metropolitan Area Network)

Connects multiple LANs within a city.

Example:

```text
Office A
   │
   ▼
City Network
   │
   ▼
Office B
```

---

## WAN (Wide Area Network)

Large network connecting countries and continents.

Example:

```text
India
   │
   ▼
Internet
   │
   ▼
USA
```

The Internet is the world's largest WAN.

---

# What Happens When You Open Google?

Example:

```text
https://google.com
```

Flow:

```text
Your Browser
      │
      ▼
Router
      │
      ▼
Internet
      │
      ▼
Google Server
      │
      ▼
Response Returned
```

This communication happens within milliseconds.

---

# Network Devices

## Router

A router connects different networks.

Responsibilities:

* Forward packets
* Route traffic
* Connect local network to internet

Example:

```text
Laptop
    │
    ▼
Router
    │
    ▼
Internet
```

---

## Switch

A switch connects devices inside the same network.

Example:

```text
PC1
PC2
PC3
 │
 ▼
Switch
```

---

## Modem

Converts ISP signals into data your devices can use.

Example:

```text
ISP
 │
 ▼
Modem
 │
 ▼
Router
```

---

# What is Data?

When you send:

```text
Hello
```

over a network,

it is converted into:

```text
01001000
01100101
01101100
01101100
01101111
```

(Binary Data)

---

# What is a Packet?

Large data is broken into smaller pieces called packets.

Example:

```text
Message:
Hello World

Packet 1
Packet 2
Packet 3
Packet 4
```

Packets travel independently through the network.

---

# What is an IP Address?

IP Address = Internet Protocol Address

Every device connected to a network needs a unique address.

Similar to:

```text
House Address
```

for postal delivery.

Without an address, data would not know where to go.

---

# Why Do We Need IP Addresses?

Imagine sending a package.

Without:

```text
House Number
Street
City
Country
```

the package cannot reach its destination.

Similarly, computers need IP addresses.

---

# IPv4 Address

Example:

```text
192.168.1.10
```

IPv4 contains:

```text
4 Octets
```

Example:

```text
192 .168 .1 .10
```

Each section ranges:

```text
0 - 255
```

---

# Structure of IPv4

Example:

```text
192.168.1.10
```

Each part is:

```text
8 Bits
```

Total:

```text
32 Bits
```

---

# Public IP Address

Used on the internet.

Example:

```text
103.45.12.10
```

Assigned by:

* ISP
* Cloud Provider

Examples:

* AWS EC2 Public IP
* Home Internet Public IP

---

# Private IP Address

Used inside local networks.

Examples:

```text
192.168.x.x
10.x.x.x
172.16.x.x - 172.31.x.x
```

Example:

```text
Laptop → 192.168.1.5
Phone  → 192.168.1.7
```

Private IPs cannot be accessed directly from the internet.

---

# How to Check Your IP Address

Linux:

```bash
ip addr
```

or

```bash
ifconfig
```

---

# Important Networking Commands

Check IP Address:

```bash
ip addr
```

Show Routing Table:

```bash
ip route
```

Check Connectivity:

```bash
ping google.com
```

Check Network Interfaces:

```bash
ip link
```

DNS Lookup:

```bash
nslookup google.com
```

---

# Practical Exercise

## Task 1

Check your IP address:

```bash
ip addr
```

Identify:

* Loopback Interface
* Private IP Address

---

## Task 2

Ping Google:

```bash
ping google.com
```

Observe:

* Response Time
* Packets Sent
* Packets Received

---

## Task 3

Check Routes:

```bash
ip route
```

Try to understand:

```text
Where packets go when leaving your machine.
```

---

# Key Concepts Learned

By the end of Day 1-2, I understand:

✅ What a Network Is

✅ Types of Networks (LAN, MAN, WAN)

✅ Routers, Switches, and Modems

✅ Data and Packets

✅ Why IP Addresses Exist

✅ Public vs Private IP Addresses

✅ IPv4 Structure

✅ Basic Networking Commands

---

# Revision Notes

Remember:

```text
Network = Communication

Packet = Small Unit of Data

Router = Connects Networks

Switch = Connects Devices

IP Address = Unique Device Address
```

---

# Motivation Corner

> Every cloud service runs on networking.

> Every Kubernetes cluster runs on networking.

> Every API request travels through a network.

> Master Networking, and the Cloud becomes easier to understand.

---

# Challenge Motto

```text
Learn Networking
       ↓
Understand Communication
       ↓
Understand Cloud
       ↓
Become a Better DevOps Engineer
```

🚀 One Packet at a Time.

🚀 One Concept at a Time.

🚀 One Day Closer to Mastery.

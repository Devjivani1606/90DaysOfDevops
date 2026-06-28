# Day 5–6: Web Networking for DevOps

## Overview

In the previous lessons, we learned how computers communicate using IP addresses, MAC addresses, ports, and networking protocols.

Now we'll understand how web applications communicate over the internet. These concepts are fundamental for working with Docker, Kubernetes, Nginx, AWS, and cloud-native applications.

---

# Request Journey

Whenever you open a website, many networking components work together behind the scenes.

```
User
 │
 ▼
Browser
 │
 ▼
DNS
 │
 ▼
IP Address
 │
 ▼
TCP Three-Way Handshake
 │
 ▼
TLS Handshake (HTTPS Only)
 │
 ▼
HTTP Request
 │
 ▼
Reverse Proxy
 │
 ▼
Application Server
 │
 ▼
Database
 │
 ▼
HTTP Response
 │
 ▼
Browser Displays Website
```

---

# DNS (Domain Name System)

## What is DNS?

DNS converts a human-readable domain name into an IP address.

Example:

```
google.com
      ↓
142.250.xxx.xxx
```

Without DNS, users would have to remember IP addresses for every website.

---

## Why DNS Exists

Humans remember names.

Computers communicate using IP addresses.

DNS acts like the internet's phonebook.

---

## How DNS Works

```
Browser
   │
   ▼
DNS Resolver
   │
   ▼
Root DNS Server
   │
   ▼
Top-Level Domain (.com)
   │
   ▼
Authoritative DNS Server
   │
   ▼
IP Address Returned
```

The browser then connects to the returned IP address.

---

## Useful Commands

```bash
nslookup google.com

dig google.com

host google.com
```

---

# URL Anatomy

Example:

```
https://www.example.com:443/products?id=10
```

Breaking it down:

```
https://
│
├── Protocol

www.example.com
│
├── Domain Name

443
│
├── Port Number

/products
│
├── Path

?id=10
│
└── Query Parameter
```

---

# HTTP

HTTP stands for HyperText Transfer Protocol.

It is the protocol used for communication between clients and web servers.

Default Port

```
80
```

Example

```
Browser
      │
HTTP Request
      │
Web Server
```

---

## HTTP Request Methods

GET

Retrieve data.

POST

Create data.

PUT

Replace existing data.

PATCH

Update part of existing data.

DELETE

Remove data.

---

# HTTP Status Codes

```
200 → Success

201 → Created

301 → Redirect

400 → Bad Request

401 → Unauthorized

403 → Forbidden

404 → Not Found

500 → Internal Server Error

502 → Bad Gateway

503 → Service Unavailable
```

---

# HTTPS

HTTPS = HTTP + TLS Encryption

Default Port

```
443
```

HTTPS provides:

- Encryption
- Authentication
- Data Integrity

Without HTTPS, anyone on the network could potentially read unencrypted traffic.

---

# TLS / SSL

TLS (Transport Layer Security) is the modern protocol that secures communication between a client and a server. SSL is the older protocol that TLS replaced, but the term "SSL" is still commonly used.

---

## TLS Handshake

Before encrypted communication starts:

```
Browser
      │
      ▼
Client Hello
      │
      ▼
Server Hello
      │
      ▼
Certificate Exchange
      │
      ▼
Session Key Generated
      │
      ▼
Encrypted Communication Begins
```

---

## Why TLS Matters

Without TLS:

```
User
 │
 ▼
Internet
 │
 ▼
Anyone can read the data
```

With TLS:

```
User
 │
 ▼
Encrypted Data
 │
 ▼
Server
```

Even if someone intercepts the traffic, they cannot easily understand its contents.

---

# Request / Response Lifecycle

When a user opens:

```
https://example.com
```

The browser performs these steps:

```
User enters URL
        │
        ▼
DNS Lookup
        │
        ▼
IP Address Found
        │
        ▼
TCP Connection
        │
        ▼
TLS Handshake
        │
        ▼
HTTP Request Sent
        │
        ▼
Reverse Proxy
        │
        ▼
Application Server
        │
        ▼
Database Query
        │
        ▼
Application Response
        │
        ▼
HTTP Response
        │
        ▼
Browser Renders Page
```

---

# Reverse Proxy

A reverse proxy sits between users and backend servers.

Example:

```
Users
   │
   ▼
Nginx
   │
   ▼
Backend Server
```

The client communicates only with the reverse proxy.

---

## Why Reverse Proxies Are Used

- Hide backend servers
- SSL termination
- Load balancing
- Caching
- Security
- Compression

Common Reverse Proxy Software:

- Nginx
- HAProxy
- Traefik
- Apache

---

# Load Balancer

A load balancer distributes incoming requests across multiple servers.

```
Users
   │
   ▼
Load Balancer
   │
 ┌─┴─────────┐
 ▼           ▼
Server 1   Server 2
```

---

## Why Load Balancers Exist

Without Load Balancer

```
1000 Users
      │
      ▼
One Server

❌ High Load
```

With Load Balancer

```
1000 Users
      │
      ▼
Load Balancer
   │    │    │
   ▼    ▼    ▼
 S1    S2    S3
```

Benefits:

- High Availability
- Scalability
- Fault Tolerance

---

## Load Balancing Algorithms

Round Robin

```
Server 1
Server 2
Server 3
Server 1
Server 2
```

Least Connections

Routes traffic to the server with the fewest active connections.

Weighted Round Robin

More powerful servers receive more traffic.

---

# CDN (Content Delivery Network)

A CDN stores copies of static files closer to users around the world.

```
Origin Server
      │
      ▼
CDN Edge Servers
      │
 ┌────┴─────┐
 ▼          ▼
India      Europe
```

Instead of every request going to the origin server, users receive content from the nearest edge location.

---

## CDN Stores

- Images
- CSS
- JavaScript
- Videos
- Fonts

---

## Benefits of CDN

- Faster loading times
- Reduced latency
- Lower bandwidth usage
- Reduced load on origin servers
- Better user experience

---

# Complete Flow

```
User
 │
 ▼
DNS
 │
 ▼
Public IP
 │
 ▼
Load Balancer
 │
 ▼
Reverse Proxy (Nginx)
 │
 ▼
Application Server
 │
 ▼
Database
 │
 ▼
HTTP Response
 │
 ▼
Browser
```

---

# Practical Commands

Check HTTP Headers

```bash
curl -I https://google.com
```

Download a Web Page

```bash
wget https://example.com
```

DNS Lookup

```bash
dig google.com
```

Show Response Headers

```bash
curl -v https://google.com
```

Trace Network Path

```bash
traceroute google.com
```

---

# Revision Summary

After completing Day 5–6, I understand:

- ✅ DNS and domain name resolution
- ✅ URL structure
- ✅ HTTP vs HTTPS
- ✅ TLS/SSL and secure communication
- ✅ Complete request/response lifecycle
- ✅ Reverse Proxy architecture
- ✅ Load Balancers and traffic distribution
- ✅ CDN architecture and caching
- ✅ Basic web troubleshooting commands

---

# Motivation Corner

> **Every website starts with a DNS lookup.**

> **Every secure connection begins with a TLS handshake.**

> **Every scalable application depends on load balancing.**

> **Every DevOps Engineer should understand how a request travels from a browser to a server and back again.**

---

# Challenge Motto

```
Understand the Request
        ↓
Understand the Infrastructure
        ↓
Understand the Cloud
        ↓
Become a Better DevOps Engineer
```

🚀 One Request at a Time.

🚀 One Layer at a Time.

🚀 One Step Closer to Production Infrastructure.
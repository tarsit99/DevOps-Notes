# Networking for DevOps

## 🌐 1. Networking Basics
* **Computer Network:** A set of interconnected nodes that transfer data from one device to another [cite: IMG_20260619_093854.jpg, image_71eb42.png].
* **How does the Internet work?** The internet is a long piece of wire (a web of optic fiber cables) that connects different computers to each other globally (e.g., connecting nodes in Pune, Mumbai, Toronto, etc.) [cite: IMG_20260619_093854.jpg, image_71eb42.png, image_71eb9f.png].
    * *Hierarchy:* Tier 1 (Backbone/Satellites) -> Tier 2 (ISPs like Tata, Jio, Airtel) -> Tier 3 (Local Area Networks/Home routers) [cite: image_71eb42.png].

---

## 🏗️ 2. Networking Models

### OSI Model (Theoretical Framework - 1974)
Open Systems Interconnection (OSI) provides a 7-step framework explaining how data travels [cite: IMG_20260619_093854.jpg, image_71eb9f.png].
1.  **Physical:** Router/Hardware [cite: IMG_20260619_093854.jpg, image_71eb9f.png].
2.  **Data Link:** Data transfer between adjacent nodes [cite: IMG_20260619_093854.jpg, image_71eb9f.png].
3.  **Network:** Routing (e.g., WhatsApp msg stuck on "Sending..." is an L3 issue) [cite: IMG_20260619_093854.jpg, IMG_20260619_093927.jpg, image_71eb9f.png].
4.  **Transport:** TCP/UDP [cite: IMG_20260619_093854.jpg, image_71eb9f.png]. *(Note: If a ping to port 80 is refused, it's an L4 issue)* [cite: IMG_20260619_093919.jpg].
5.  **Session:** Login session management [cite: IMG_20260619_093854.jpg, image_71eb9f.png].
6.  **Presentation:** Encryption/Decryption [cite: IMG_20260619_093854.jpg, image_71eb9f.png].
7.  **Application:** WhatsApp/Web browser interface [cite: IMG_20260619_093854.jpg, image_71eb9f.png].

### TCP/IP Model (Practical Implementation)
The practical version of OSI, condensed into 4 layers [cite: IMG_20260619_093854.jpg, image_71ec1d.png]:
1.  **Application Layer:** (Combines OSI 5, 6, 7). Protocols: HTTP/HTTPS, Encryption, Session [cite: IMG_20260619_093854.jpg, image_71ec1d.png].
2.  **Transport Layer:** (OSI 4). Protocols: TCP, UDP [cite: IMG_20260619_093854.jpg, image_71ec1d.png].
3.  **Internet Layer:** (OSI 3). Handles IP address and routing [cite: IMG_20260619_093854.jpg, image_71ec1d.png].
4.  **Network Access Layer:** (Combines OSI 1, 2). Handles cables and MAC addresses [cite: IMG_20260619_093854.jpg, image_71ec1d.png].

---

## 📜 3. Protocols & Ports
**Protocols** are sets of rules for internet communication [cite: IMG_20260619_093854.jpg].
* **TCP (Transmission Control Protocol):** Focuses on *Accuracy* (used for browsing) [cite: IMG_20260619_093854.jpg, IMG_20260619_093919.jpg].
* **UDP (User Datagram Protocol):** Focuses on *Speed*. Preferred for video streaming because speed is more important than perfection [cite: IMG_20260619_093854.jpg, IMG_20260619_093919.jpg].
* **ICMP (Internet Control Message Protocol):** An L3 (network layer) protocol used by devices (routers, hosts) to send error messages and operational info [cite: IMG_20260619_093903.jpg]. Used by `ping` and `traceroute` [cite: image_71ec1d.png].
* **DHCP:** Dynamic Host Configuration Protocol. Automatically assigns dynamic IPs to devices for seamless network communication [cite: IMG_20260619_093903.jpg].

**Ports** act as virtual doors on a device that direct incoming network traffic to the correct application/service [cite: IMG_20260619_093903.jpg].
* *Common Ports:* Nginx Web Server (80), MySQL DB (3306), MongoDb (27017), PostGres (5432) [cite: image_723db9.png].

---

## 📍 4. Addressing (IP, MAC, & DNS)

### IP Addresses (Logical)
* A logical address given to a device over the network [cite: IMG_20260619_093903.jpg].
* *How to find your IP via CLI:*
    * **Public IP:** `$ curl ifconfig.me` [cite: IMG_20260619_093903.jpg, IMG_20260619_093910.jpg].
    * **Private IP:** `$ hostname -i` [cite: IMG_20260619_093910.jpg].

### MAC Address (Physical)
* Media Access Control address given to the hardware's NIC (Network Interface Card) [cite: IMG_20260619_093903.jpg].

### DNS (Domain Name System)
* Hypothetically, it is a souped-up phonebook record that can look up the exact IP for a website from its database [cite: IMG_20260619_093903.jpg].
* *Common DevOps Meme:* "It's always DNS" [cite: IMG_20260619_093919.jpg].
* **DNS Troubleshooting Tools:**
    * `nslookup`: Simpler tool for quick DNS lookups (domain info grabber) [cite: IMG_20260619_093903.jpg].
    * `dig`: Modern DNS tool that provides detailed query results & troubleshooting info. Used to query DNS to get IP addresses or verify records (A, MX, TXT, CNAME) [cite: IMG_20260619_093903.jpg, IMG_20260619_093919.jpg].
* **TTL (Time To Live):** How long a device remembers (caches) an address [cite: IMG_20260619_093919.jpg].

---

## ☁️ 5. Cloud Networking Concepts (VPC, Subnets, Proxies)
*Most accurate description of modern DevOps responsibility in a cloud environment: Define & Manage VPC, Subnets, Firewalls.* [cite: IMG_20260619_093927.jpg]

* **VPC (Virtual Private Cloud):** Your own private network in the cloud where you can deploy your own resources (Servers, IPs, Subnets, Security, Route tables) [cite: IMG_20260619_093910.jpg, image_723db9.png].
* **Subnet:** A smaller, logical network segmentation of a larger network, allowing IPs to be managed efficiently [cite: IMG_20260619_093903.jpg].
* **CIDR (Classless Inter-Domain Routing):** A compact way to write IP address ranges and their network masks [cite: IMG_20260619_093910.jpg].
    * *Rule:* A LOWER CIDR number = MORE IPs [cite: IMG_20260619_093919.jpg].
    * `/32` represents 1 single IP address ($2^0 = 1$) [cite: IMG_20260619_093919.jpg].
    * `/26` represents 64 IPs ($2^6 = 64$) [cite: IMG_20260619_093919.jpg].
    * `0.0.0.0/0`: Represents the entire internet (approx 4.3 billion IPs). Opening all traffic (`0.0.0.0/0`) in Security Groups (SGs) to fix a connection issue is a major security risk [cite: IMG_20260619_093919.jpg].
* **Route Table:** A set of rules that tells the network where to send traffic [cite: IMG_20260619_093910.jpg].
* **NAT Gateway:** Network Address Translation gateway allows private servers (with no public IP) to access the internet (outgoing only) [cite: IMG_20260619_093910.jpg].
* **Load Balancers:** Distribute traffic across healthy servers [cite: IMG_20260619_093927.jpg].
* **Proxies:**
    * *Forward Proxy:* Hides the CLIENT (e.g., VPN) [cite: IMG_20260619_093927.jpg].
    * *Reverse Proxy:* Hides the SERVER [cite: IMG_20260619_093927.jpg].

### 3-Tier Application Architecture
A typical application architecture setup [cite: IMG_20260619_093910.jpg, image_723db9.png]:
1.  **UI/Frontend:** e.g., EC2 instance with a Public IP.
2.  **Backend (Logic):** Could be placed under private or public IP (APIs).
3.  **Database:** e.g., RDS with a Private IP.

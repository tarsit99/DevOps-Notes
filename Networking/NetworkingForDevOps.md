## 🌐 1. Networking Basics
* **Computer Network:** A set of interconnected nodes that transfer data from one device to another.
* **How does the Internet work?** The internet is a long piece of wire (a web of optic fiber cables) that connects different computers to each other globally (e.g., connecting nodes in Pune, Mumbai, Toronto, etc.) .
    * *Hierarchy:* Tier 1 (Backbone/Satellites) -> Tier 2 (ISPs like Tata, Jio, Airtel) -> Tier 3 (Local Area Networks/Home routers).

---

## 🏗️ 2. Networking Models

### OSI Model (Theoretical Framework - 1974)
Open Systems Interconnection (OSI) provides a 7-step framework explaining how data travels.
1.  **Physical:** Router/Hardware.
2.  **Data Link:** Data transfer between adjacent nodes.
3.  **Network:** Routing (e.g., WhatsApp msg stuck on "Sending..." is an L3 issue).
4.  **Transport:** TCP/UDP. *(Note: If a ping to port 80 is refused, it's an L4 issue)*.
5.  **Session:** Login session management.
6.  **Presentation:** Encryption/Decryption.
7.  **Application:** WhatsApp/Web browser interface.

### TCP/IP Model (Practical Implementation)
The practical version of OSI, condensed into 4 layers:
1.  **Application Layer:** (Combines OSI 5, 6, 7). Protocols: HTTP/HTTPS, Encryption, Session.
2.  **Transport Layer:** (OSI 4). Protocols: TCP, UDP.
3.  **Internet Layer:** (OSI 3). Handles IP address and routing.
4.  **Network Access Layer:** (Combines OSI 1, 2). Handles cables and MAC addresses.

---

## 📜 3. Protocols & Ports
**Protocols** are sets of rules for internet communication.
* **TCP (Transmission Control Protocol):** Focuses on *Accuracy* & *ReliableDataDelivery* (used for browsing).
* **UDP (User Datagram Protocol):** Focuses on *Speed*. Preferred for video streaming because speed is more important than perfection.
* **ICMP (Internet Control Message Protocol):** An L3 (network layer) protocol used by devices (routers, hosts) to send error messages and operational info . Used by `ping` and `traceroute`.
* **DHCP:** Dynamic Host Configuration Protocol. Automatically assigns dynamic IPs to devices for seamless network communication.

**Ports** act as virtual doors on a device that direct incoming network traffic to the correct application/service.
* *Common Ports:* Nginx Web Server (80), MySQL DB (3306), MongoDb (27017), PostGres (5432).

---

## 📍 4. Addressing (IP, MAC, & DNS)

### IP Addresses (Logical)
* A logical address given to a device over the network.
* *How to find your IP via CLI:*
    * **Public IP:** `$ curl ifconfig.me`.
    * **Private IP:** `$ hostname -I`.

### MAC Address (Physical)
* Media Access Control address given to the hardware's NIC (Network Interface Card).

### DNS (Domain Name System)
* Hypothetically, it is a souped-up phonebook record that can look up the exact IP for a website from its database.
* *Common DevOps Meme:* "It's always DNS" 😂
* **DNS Troubleshooting Tools:**
    * `nslookup`: Simpler tool for quick DNS lookups.
    * `dig`: (domain info grabber) Modern DNS tool that provides detailed query results & troubleshooting info. Used to query DNS to get IP addresses or verify records (A, MX, TXT, CNAME).
* **TTL (Time To Live):** How long a device remembers (caches) an address.

---

## ☁️ 5. Cloud Networking Concepts (VPC, Subnets, Proxies)
*Most accurate description of modern DevOps responsibility in a cloud environment: Define & Manage VPC, Subnets, Firewalls.

* **VPC (Virtual Private Cloud):** Your own private network in the cloud where you can deploy your own resources (Servers, IPs, Subnets, Security, Route tables).
* **Subnet:** A smaller, logical network segmentation of a larger network, allowing IPs to be managed efficiently.
* **CIDR (Classless Inter-Domain Routing):** A compact way to write IP address ranges and their network masks.
    * *Rule:* A LOWER CIDR number = MORE IPs.
    * `/32` represents 1 single IP address ($2^0 = 1$).
    * `/26` represents 64 IPs ($2^6 = 64$).
    * `0.0.0.0/0`: Represents the entire internet (approx 4.3 billion IPs). Opening all traffic (`0.0.0.0/0`) in Security Groups (SGs) to fix a connection issue is a major security risk.
* **Route Table:** A set of rules that tells the network where to send traffic.
* **NAT Gateway:** Network Address Translation gateway allows private servers (with no public IP) to access the internet (outgoing only).
* **Load Balancers:** Distribute traffic across healthy servers.
* **Proxies:**
    * *Forward Proxy:* Hides the CLIENT (e.g., VPN).
    * *Reverse Proxy:* Hides the SERVER (e.g., NGINX).

### 3-Tier Application Architecture
A typical application architecture setup:
1.  **UI/Frontend:** e.g., EC2 instance with a Public IP.
2.  **Backend (Logic):** Could be placed under private or public IP (APIs).
3.  **Database:** e.g., RDS with a Private IP.

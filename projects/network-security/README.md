---

# 🏦 OriginBank Secure Network Infrastructure

### Enterprise Network Security Design & Implementation (Cisco Packet Tracer)

## 📌 Project Overview

This project demonstrates the design and implementation of a **secure enterprise network infrastructure** for a fictional financial institution, **OriginBank**.

The network was designed to address security weaknesses such as weak authentication, poor segmentation, and lack of monitoring by implementing layered security controls and Zero Trust principles.

This project showcases real-world network security practices, including segmentation, firewall policy enforcement, secure management, VPN encryption, and intrusion prevention.

---

## 🎯 Objectives

✔ Design a secure enterprise network architecture
✔ Implement VLAN segmentation & secure communication
✔ Enforce firewall policies & access controls
✔ Secure network device management
✔ Establish encrypted site-to-site connectivity
✔ Monitor and prevent malicious traffic
✔ Apply Zero Trust security principles

---

## 🗺️ Network Topology
<img width="1162" height="658" alt="Screenshot 2026-02-18 at 6 57 04 AM" src="https://github.com/user-attachments/assets/239d3bb2-bc04-4835-8eb2-09a176189f8b" />

📍 The network consists of:

* Headquarters (HQ)
* Branch Office
* DMZ (Public Services Zone)
* ASA Firewall
* Border Router & WAN links
* External network simulation


---

## 🧱 Network Architecture

### VLAN Segmentation

| VLAN | Zone       | Purpose         |
| ---- | ---------- | --------------- |
| 10   | DMZ        | Public services |
| 20   | HQ LAN     | Internal users  |
| 30   | Branch LAN | Remote office   |

Segmentation ensures isolation and controlled access between zones.

---

## 🌐 IP Addressing Plan

* Structured IP allocation for HQ, Branch, DMZ & WAN
* Static IPs for servers
* DHCP for client devices

| Zone / Link | Device / Interface | IP Address | Network / Subnet Mask | Responsibility |
|-------------|-------------------|-----------|----------------------|---------------|
| **DMZ (VLAN 10)** | ASA1 Et0/0 | 192.168.0.1 | 192.168.0.0/26 (255.255.255.192) | Default Gateway |
| | DNS/DHCP Server | 192.168.0.2 | | DHCP + DNS |
| | Exchange Server | 192.168.0.3 | | Mail |
| | Web Server | 192.168.0.4 | | www.originbank.com |
| **HQ LAN (VLAN 20)** | HQ Router Gi7/0 | 192.168.0.65 | 192.168.0.64/26 (255.255.255.192) | Default Gateway |
| | Internal DNS/DHCP Server | 192.168.0.66 | | DHCP + DNS |
| | Syslog/NTP Server | 192.168.0.67 | | Logs + Time |
| | HQ PCs (DHCP) | 192.168.0.68 – 126 | | Workstations |
| **Branch LAN (VLAN 30)** | Branch Router Fa0/0 | 192.168.0.129 | 192.168.0.128/25 (255.255.255.0) | Default Gateway |
| | Branch DNS/DHCP Server | 192.168.0.130 | | DHCP + DNS |
| | Branch PCs (DHCP) | 192.168.0.131 – 254 | | Workstations |
| **WAN Link 1** | HQ Router Fa1/0 | 20.20.0.1 | 20.20.0.0/30 (255.255.255.252) | Link to ASA |
| | ASA Gig1/1 | 20.20.0.2 | | Link to HQ Router |
| **WAN Link 2** | ASA Gig1/2 | 20.20.0.5 | 20.20.0.4/30 (255.255.255.252) | Link to Border Router |
| | Border Router Fa0/0 | 20.20.0.6 | | Link to ASA |
| **WAN Link 3** | Border Router Se2/0 | 20.20.0.9 | 20.20.0.8/30 (255.255.255.252) | Link to Router0 |
| | Router0 Se2/0 | 20.20.0.10 | | Link to Border Router |
| **WAN Link 4** | Border Router Se3/0 | 20.20.0.13 | 20.20.0.12/30 (255.255.255.252) | Link to Router1 |
| | Router1 Se2/0 | 20.20.0.14 | | Link to Border Router |
| **WAN Link 5** | Router0 Se3/0 | 20.20.0.17 | 20.20.0.16/30 (255.255.255.252) | Link to Router2 |
| | Router2 Se7/0 | 20.20.0.18 | | Link to Router0 |
| **WAN Link 6** | Router1 Se3/0 | 20.20.0.21 | 20.20.0.20/30 (255.255.255.252) | Link to Router2 |
| | Router2 Se6/0 | 20.20.0.22 | | Link to Router1 |
| **WAN Link 7** | Router2 Se2/0 | 20.20.0.25 | 20.20.0.24/30 (255.255.255.252) | Link to Branch Router |
| | Branch Router Se2/0 | 20.20.0.26 | | Link to Router2 |
| **WAN Link 8** | Router2 Se3/0 | 20.20.0.29 | 20.20.0.28/30 (255.255.255.252) | Link to External Router |
| | External Router Se2/0 | 20.20.0.30 | | Link to Router2 |


---

## 🔐 Security Implementation

### 🖥️ Device Hardening

* Strong authentication & encrypted passwords
* Disabled unused services & ports
* Login warning banners
* Port security & interface shutdown

---

### 🌍 Core Network Services

✔ DNS server for name resolution
✔ Web server hosted in DMZ
✔ Syslog server for centralized logging

---

### 🔄 Dynamic Routing & VLAN Communication

* OSPF for dynamic routing
* VLAN trunking (802.1Q)
* Inter-VLAN routing (Router-on-a-Stick)

📷 *(Insert routing verification screenshot)*

---

### 🔥 Firewall & Access Control (ASA)

Security policies enforce strict traffic control:

#### ✔ HQ → DMZ

* Allow HTTP/HTTPS, DNS, SMTP
* Allow admin SSH & ICMP
* Deny all other traffic

#### ✔ Outside → DMZ

* Allow public web & DNS access
* Block all other services

#### ✔ HQ → Internet

* Allow web & DNS
* Block P2P & dangerous ports

#### ✔ DMZ → HQ

* Blocked (Zero Trust principle)

📷 *(Insert ACL & blocked traffic proof)*

---

### 🌍 NAT / PAT Configuration

* PAT enables internet access for DMZ hosts
* Public access to DMZ web server via firewall public IP

---

## 🔑 Secure Management Access

### SSH Implementation

* SSH v2 enabled
* Telnet disabled
* RSA key encryption
* Secure remote administration

### AAA Authentication

* Local user authentication
* Role-based privilege levels
* Session timeout enforcement

📷 *(Insert SSH login screenshot)*

---

## 🔐 Site-to-Site IPsec VPN

A secure tunnel connects HQ and Branch networks.

### Security Features:

✔ AES-256 encryption
✔ SHA-based integrity verification
✔ IKE key exchange
✔ Perfect Forward Secrecy (PFS)

📷 *(Insert encrypted ping / VPN proof)*

---

## 🛡️ Intrusion Prevention System (IPS)

### IPS Capabilities:

* Detects known attack signatures
* Monitors inbound & outbound traffic
* Logs security events to Syslog server
* Blocks suspicious activity

### Test Performed:

✔ ICMP flood attack simulation
✔ IPS detection & blocking confirmed

📷 *(Insert IPS alert screenshot)*

---

## 🧠 Zero Trust Security Principles

This network partially implements Zero Trust through:

✔ Network segmentation & micro-isolation
✔ Least-privilege access policies
✔ Secure management authentication
✔ Continuous monitoring & logging

### Recommended Improvements:

* RADIUS/TACACS+ centralized AAA
* Multi-Factor Authentication (MFA)
* SIEM integration
* Zero Trust Network Access (ZTNA)

---

## 🔍 Security Benefits Achieved

✅ Reduced attack surface
✅ Controlled access between zones
✅ Encrypted inter-site communication
✅ Centralized monitoring & logging
✅ Protection against unauthorized access
✅ Improved confidentiality, integrity, and availability

---

## 🧰 Technologies Used

* Cisco Packet Tracer
* Cisco ASA Firewall
* OSPF Routing Protocol
* VLAN & Inter-VLAN Routing
* IPsec VPN
* AAA & SSH Security
* Intrusion Prevention System (IPS)
* Network Segmentation
* Zero Trust Concepts

---

## 🧪 Testing & Verification

✔ Connectivity testing between VLANs
✔ Firewall rule validation
✔ VPN tunnel verification
✔ IPS attack detection test
✔ Service accessibility testing

---

## 📚 Key Learning Outcomes

This project strengthened practical skills in:

* Enterprise network design
* Network security architecture
* Firewall & ACL policy design
* VPN configuration & cryptography
* Secure device management
* Intrusion detection & prevention
* Zero Trust security implementation

---

## 🚀 Future Improvements

* Implement centralized AAA (RADIUS/TACACS+)
* Deploy SIEM for security analytics
* Implement MFA for admin access
* Upgrade to certificate-based VPN authentication
* Integrate cloud-based monitoring

---

## 👨‍💻 Author

**Soriful Islam Shoaib**
MSc Cybersecurity
Network Security & Cloud Security Enthusiast

📎 LinkedIn: *(add link)*
📎 Portfolio: *(add link)*

---


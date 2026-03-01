# 🏢 Uni-Network: Campus Network & Security Simulation

This repository contains the configuration files, testing evidence, and documentation for **Uni-Network**, a multi-building Campus Network Simulation built using Cisco Packet Tracer. 

The project bridges theoretical networking concepts with practical implementation, scaling from fundamental routing and switching to a hardened, security-focused architecture.

## 🚀 Project Evolution

### Phase 1: Core Network Infrastructure
The foundation of the campus network focuses on scalable design and automated dynamic addressing across multiple subnets and buildings.
* **Dynamic IP Allocation (DHCP):** Automated IP management for end devices across all organizational subnets.
* **Traffic Isolation (VLANs):** Segregated network traffic within buildings to enhance performance and broadcast control.
* **Inter-Building Connectivity (RIP):** Dynamic routing configured to ensure seamless communication between distinct building subnets.
* **Internet Access (NAT):** Network Address Translation implemented to provide secure external internet access for internal private networks.

### Phase 2: Cybersecurity & Network Hardening (Current)
Upgraded the topology to protect against unauthorized access, internal threats, and unencrypted management traffic.
* **Secure Device Management (SSH):** Deprecated plaintext Telnet in favor of SSH with RSA crypto keys and local user authentication for secure remote router/switch management.
* **Layer 2 Hardening (Port Security):** Configured access ports with MAC address sticky learning and violation shutdown rules to prevent unauthorized rogue devices from accessing the network.
* **Traffic Filtering (Extended ACLs):** Implemented strict Access Control Lists to enforce security policies, such as restricting student VLAN access to highly classified administration servers while permitting standard outbound traffic.

## 🛠️ Tech Stack & Tools
* **Simulation Environment:** Cisco Packet Tracer
* **Core Concepts:** Routing & Switching, Network Security, OSI Model applied, Cisco IOS CLI

## 📂 Repository Contents
* `Uni-Network-v3.pkt`: The core Cisco Packet Tracer simulation file containing the full topology and configurations.
* `Project Report.pdf`: Full documentation detailing the objectives, subnetting math, and testing outcomes.
* **Testing & Verification:** Evidence of successful DHCP leases, NAT translations, and ACL drop logs (`show access-lists`).

## 🔍 How to Test the Security Features
1. Open the `.pkt` file in Cisco Packet Tracer.
2. Open a PC in the Student Subnet and attempt to `ping 192.168.20.50` (Admin Server). The request will be actively blocked by the Extended ACL.
3. Access a Router CLI and type `show access-lists` to view the active drop counts and verify the firewall rules are working.

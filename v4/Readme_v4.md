# 🏢 Uni-Network: Campus Network & Security Simulation

Welcome to **Uni-Network**! This project is a comprehensive, multi-building campus network simulation built in Cisco Packet Tracer. 

It demonstrates the full lifecycle of enterprise network engineering—starting from fundamental routing and switching, and scaling up to a hardened architecture with active security monitoring. With dedicated subnets for IoT research and cybersecurity testing, this topology mimics a realistic, modern university environment.

---

## 🗺️ Network Topology & IP Addressing

The campus is divided into distinct operational and academic zones using a Class C addressing scheme:

| Department / Building | Subnet | Gateway | VLAN |
| :--- | :--- | :--- | :--- |
| **Student Network** | `192.168.10.0 /24` | `192.168.10.1` | VLAN 10 |
| **Administration** | `192.168.20.0 /24` | `192.168.20.1` | VLAN 20 |
| **IoT Research Lab** | `192.168.30.0 /24` | `192.168.30.1` | VLAN 30 |
| **Cybersecurity "Subnet"** | `192.168.40.0 /24` | `192.168.40.1` | VLAN 40 |

---

## ✨ Features & Project Phases

### Phase 1: Core Infrastructure
* **Dynamic Addressing (DHCP):** Automated IP allocation across all subnets.
* **Traffic Isolation (VLANs):** Logical separation of departments to optimize broadcast domains.
* **Inter-VLAN Routing (RIPv2):** Dynamic routing allowing seamless campus-wide communication.
* **Internet Access (NAT):** Network Address Translation bridging private internal IPs to the external simulated web.

### Phase 2: Network Hardening
* **Secure Management (SSH):** Deprecated plaintext Telnet in favor of encrypted RSA-key remote access.
* **Physical Layer Protection (Port Security):** `mac-address sticky` configurations with violation shutdowns to prevent rogue hardware connections.
* **Traffic Filtering (Extended ACLs):** Internal firewall rules blocking Student VLAN access to the Administration servers while permitting standard outbound traffic.

### Phase 3 & 4: Scaling & Active Monitoring
* **Topology Expansion:** Integrated the IoT and Cybersecurity labs with dedicated hardware and routing updates.
* **Mitigating MitM Attacks (DHCP Snooping):** Trusted/Untrusted port configurations to block rogue DHCP servers.
* **Centralized Logging (Syslog):** Configured all campus devices to forward millisecond-stamped security alerts to a central monitoring server.

### Phase 5: Upcoming Features 🚧
* Migration from RIPv2 to Single-Area **OSPF**.
* Enterprise Wireless implementation (WLC + RADIUS Authentication).
* Rapid PVST+ optimization for redundant links.

---

## 🛠️ How to Replicate This Project

Want to build this yourself? Follow this step-by-step roadmap in Cisco Packet Tracer:

### Step 1: Physical Cabling & Core Setup
1. Place your Core Router, Distribution Switches, and End Devices (PCs/Laptops/Servers).
2. Wire the topology using Copper Straight-Through cables (end devices to switches) and Cross-Over cables (switch to switch, if applicable).
3. Assign the Default Gateway IP addresses to the Core Router's physical/sub-interfaces.

### Step 2: Routing & Switching
1. Configure **VLANs** on your switches and assign the appropriate access ports to them.
2. Set up trunk links between your switches and the core router.
3. Configure **DHCP Pools** on the router for each distinct subnet.
4. Enable **RIPv2** (or your protocol of choice) and advertise your directly connected networks. 
5. *Test: Ensure PCs can successfully ping across different VLANs.*

### Step 3: Implementing Security Measures
1. Generate Crypto Keys and enforce **SSH** on the VTY lines of all routers and switches.
2. Configure **Port Security** on all switch access ports (Max 1 MAC, Sticky, Violation Shutdown).
3. Write an **Extended ACL** on the router to block specific inter-VLAN traffic (e.g., denying the `192.168.10.0` network from reaching `192.168.20.50`), and apply it `inbound` on the correct interface.

### Step 4: Advanced Hardening
1. Enable **DHCP Snooping** globally on your switches. Trust the uplink ports facing the router and untrust the ports facing the PCs.
2. Place a **Syslog Server** in your Admin network. Configure all network devices using `logging [server-ip]` and `service timestamps log datetime msec` to forward alerts.
3. *Test: Plug a rogue PC into a secure switch port. Watch the interface drop and verify the log appears on the Syslog Server.*

---

## 💻 Prerequisites
* Cisco Packet Tracer (Version 8.0 or higher recommended)
* Basic understanding of Cisco IOS CLI commands

## 📜 License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

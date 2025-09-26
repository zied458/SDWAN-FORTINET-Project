# ⚙️ Technical Specifications

## 🌐 Network Architecture Overview

### Topology Design
- **Architecture Type**: Hub-and-spoke SD-WAN with mesh connectivity  
- **Sites**: 1 Headquarters (HQ) + 2 Branch offices  
- **Redundancy**: High Availability (HA) cluster at HQ  
- **WAN Connections**: Multiple redundant paths per site  

---

## 🗂️ IP Addressing Scheme

### Headquarters (HQ)
- **FGT-HQ01 Port1 (WAN1):** 5.2.0.1/24  
- **FGT-HQ01 Port2 (WAN2):** 5.3.0.1/24  
- **FGT-HQ01 Port3 (LAN):** 172.28.0.254/24  
- **FGT-HQ01 Port4 (Inet02):** 192.168.126.100/24  
- **FGT-HQ01 Port5 (WAN3):** 5.4.0.1/24  
- **FGT-HQ01 Port6 (DMZ):** 172.28.100.254/24  

### Branch Office 01
- **FGT-BR01 Port1 (WAN1):** 5.2.2.2/24  
- **FGT-BR01 Port2 (WAN2):** 5.3.2.2/24  
- **FGT-BR01 Port3 (LAN):** 172.28.2.254/24  
- **FGT-BR01 Port4 (Inet02):** 192.168.126.138/24  

### Branch Office 02
- **FGT-BR02 Port1 (WAN1):** 5.2.1.2/24  
- **FGT-BR02 Port2 (WAN2):** 5.3.1.2/24  
- **FGT-BR02 Port3 (LAN):** 172.28.1.254/24  
- **FGT-BR02 Port4 (Inet1):** 192.168.126.140/24  

---

## 🖥️ Hardware & Software Specifications

### Fortinet Equipment
- **FortiGate Firewalls (v7.0.2)**  
  - Next-Generation Firewall (NGFW)  
  - SD-WAN capabilities  
  - VPN concentrator  
  - Intrusion Prevention System (IPS)  
  - Web filtering & Application Control  

- **FortiManager (v7.0.2)**  
  - Centralized management platform  
  - Policy orchestration  
  - Device monitoring  
  - Backup & restore  

- **FortiClient**  
  - SSL VPN client  
  - Endpoint protection  
  - Zero-trust access  

- **FortiToken**  
  - Two-Factor Authentication (OTP)  
  - Mobile app & hardware tokens  

### Network Infrastructure
- **Cisco Routers (IOS)**: WAN connectivity, BGP & OSPF  
- **Cisco Switches (L2)**: VLAN configuration  

### Virtualization Platform
- **VMware Workstation 17 Player**  
  - 8GB RAM, 2 CPUs, 60GB storage  
  - Multi-OS support  
  - Snapshots  

- **EVE-NG Network Emulator**  
  - Topology simulation  
  - Device interconnection  

### Cloud Services
- **Microsoft Azure**  
  - Windows Server 2019 Datacenter  
  - Active Directory services  
  - Domain: `pfe.tn`  
  - VM: `40.127.15.101`  

---

## 🔐 SD-WAN Configuration

### IPSec Tunnel Configuration
| Tunnel Name | Local IP    | Remote IP   | Interface |
|-------------|------------|-------------|-----------|
| HQTOBR01    | 10.10.1.1  | 10.10.1.2   | Port1     |
| HQTOBR02    | 10.10.2.1  | 10.10.2.2   | Port1     |
| HQTOBR01-1  | 10.10.3.1  | 10.10.3.2   | Port2     |
| HQTOBR02-2  | 10.10.4.1  | 10.10.4.2   | Port2     |

---

## 📡 Routing Protocols

### OSPF Configuration
| Device   | Router ID | Area   | Networks                     |
|----------|-----------|--------|------------------------------|
| FGT-HQ01 | 3.3.3.3   | 0.0.0.0| 5.2.0.0/24, 172.28.0.0/24   |
| FGT-BR01 | 4.4.4.4   | 0.0.0.0| 5.2.2.0/24, 172.28.2.0/24   |
| FGT-BR02 | 2.2.2.2   | 0.0.0.0| 5.2.1.0/24, 172.28.1.0/24   |

### BGP Configuration
- **eBGP (External)**: AS 200  
- **iBGP (Internal)**: AS 65400  
- **Neighbors**: Tunnel endpoints for SD-WAN mesh  

---

## 🔀 VLAN Configuration

| VLAN ID | Name      | Interfaces   | Purpose                |
|---------|----------|--------------|------------------------|
| 50      | HQ-Inet01| Eth1/0-1/2   | Internet connectivity  |
| 150     | HQ-WAN01 | Eth2/0-2/2   | WAN connection 1       |
| 200     | HQ-WAN02 | Eth3/0-3/2   | WAN connection 2       |
| 300     | HQ-PART  | Eth4/0-4/2   | Partner connectivity   |

---

## 🔒 Security Configuration

### Firewall Policies
- SD-WAN traffic rules (source/destination matching, SLA path selection)  
- SSL VPN policies (Azure AD integration, certificate-based security)  
- Web filtering (gambling, dating, weapons blocked)  
- Application control (social media, games restricted)  

### Authentication Systems
- **LDAP Integration**: Azure AD connectivity  
- **Two-Factor Authentication**: FortiToken OTP  
- **PKI Certificates**: Infrastructure security  
- **Role-Based Access Control** via user groups  

---

## 📊 Performance Monitoring

### SLA Monitoring
- Latency, jitter, packet loss detection  
- Automatic failover for HA  

### Monitoring Tools
- **FortiManager** dashboards  
- **Wireshark** packet capture  
- Built-in FortiGate diagnostics  
- Performance graphs (real-time & historical)  

---

## 🔄 High Availability (HA)

### Redundancy Features
- Active-Passive HA (HQ cluster sync)  
- Multiple WAN paths with load balancing  
- Dynamic routing redundancy  
- Automatic config sync  

### Failover Capabilities
- Link/device failure monitoring  
- Seamless switching  
- Automatic recovery  
- Continuous health monitoring  

---

## 🧪 Testing & Validation

### Connectivity Testing
- End-to-end communication across all segments  
- IPSec & SSL VPN validation  
- OSPF/BGP convergence check  
- DNS resolution tests  

### Security Testing
- Firewall rule validation  
- Malware blocking  
- Web filtering enforcement  
- Authentication (Azure AD + 2FA)  

### Performance Testing
- Bandwidth measurement  
- Latency testing  
- Failover validation  
- Load balancing distribution  


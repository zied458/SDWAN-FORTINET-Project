# 🚀 Deployment Guide

## 📌 Prerequisites

### Hardware Requirements
- **FortiGate Firewalls**: Minimum 3 units (1 HQ cluster + 2 branches)  
- **Network Infrastructure**: Routers, switches, and WAN connections  
- **Virtualization Platform**: VMware Workstation or equivalent  
- **Cloud Services**: Microsoft Azure subscription  

### Software Requirements
- **FortiOS**: Version 7.0.2 or later  
- **FortiManager**: Version 7.0.2 or later  
- **EVE-NG**: Network emulation platform  
- **Supporting Tools**: WinSCP, PuTTY, Wireshark  

---

## Phase 1: Infrastructure Setup

### 1.1 Network Planning
- Design network topology with hub-and-spoke architecture  
- Allocate IP addressing for all network segments  
- Plan VLAN structure for network segmentation  
- Define security zones and access policies  

### 1.2 Hardware Installation
- Deploy FortiGate devices at each location  
- Configure basic network connectivity  
- Establish WAN connections with ISP providers  
- Set up management network for device access  

### 1.3 Initial Configuration
```bash
# Basic FortiGate setup
config system global
    set hostname "FGT-HQ01"
    set timezone "GMT+1"
end

config system interface
    edit "port1"
        set mode static
        set ip 5.2.0.1 255.255.255.0
        set allowaccess ping https ssh
    next
end
```

## Phase 2: SD-WAN Configuration

### 2.1 Interface Configuration
- Configure **WAN interfaces** on all FortiGate devices  
- Set up **LAN interfaces** for local network connectivity  
- Define interface roles (**WAN, LAN, DMZ**)  
- Enable necessary services on each interface  
### 2.2 IPSec VPN Setup

```bash
# IPSec tunnel configuration
config vpn ipsec phase1-interface
    edit "HQTOBR01"
        set interface "port1"
        set remote-gw 5.2.2.2
        set psksecret "your-psk-secret"
    next
end

config vpn ipsec phase2-interface
    edit "HQTOBR01"
        set phase1name "HQTOBR01"
        set proposal aes256-sha256
    next
end
```
### 2.3 SD-WAN Zone Creation

```bash
# SD-WAN configuration
config system sdwan
    set status enable
    config zone
        edit "virtual-wan-link"
        next
    end
    config members
        edit 1
            set interface "HQTOBR01"
            set zone "virtual-wan-link"
        next
    end
end
```
## Phase 3: Routing Configuration

### 3.1 OSPF Setup

```bash
# OSPF configuration
config router ospf
    set router-id 3.3.3.3
    config area
        edit 0.0.0.0
        next
    end
    config network
        edit 1
            set prefix 5.2.0.0 255.255.255.0
            set area 0.0.0.0
        next
        edit 2
            set prefix 172.28.0.0 255.255.255.0
            set area 0.0.0.0
        next
    end
end
```
### 3.2 BGP Configuration

```bash
# BGP setup
config router bgp
    set as 65400
    set router-id 3.3.3.3
    config neighbor
        edit "10.10.1.2"
            set remote-as 65400
        next
    end
end
```
## Phase 4: Security Implementation

### 4.1 Firewall Policies
```bash
# Basic firewall policy
config firewall policy
    edit 1
        set name "SD-WAN-Traffic"
        set srcintf "virtual-wan-link"
        set dstintf "port3"
        set srcaddr "all"
        set dstaddr "all"
        set action accept
        set schedule "always"
        set service "ALL"
    next
end
```

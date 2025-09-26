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


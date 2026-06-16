## OpenVPN Server Setup  
**Objective** Enable remote access to my homelab from my PC on a seperate network

**Overview** This document outlines the steps that I took to configure OpenVPN on my ASUS RT-AC88U router running Asuswrt-Merlin firmware. The goal was to enable secure access to my homelab network while connected to a seperate ISP network.

**Tools Used:**
- ASUS RT-AC88U With Merlin Firmware
- OpenVPN Server (Built into Merlin)
- OpenVPN GUI Client (Windows)

## Network Architecture
**Primary Network (Spectrum)**
- Subnet: 192.168.1.X/24
  
**Lab Network (ASUS RT-AC88U)**
- Subnet 192.168.2.X/24
  
**VPN Tunnel**
- Subnet 10.8.0.X/24


## Step 1: Access the VPN Settings
Navigate to VPN -> VPN Status in the Merlin Dashboard. All VPN services will show they're stopped by default.
![VPN Settings](https://raw.githubusercontent.com/Frank-Atwood/Cyber-Projects/main/home-lab/vpn-setup/screenshots/Screenshot_56.png)

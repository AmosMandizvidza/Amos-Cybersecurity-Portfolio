
# Network Security Lab

Beginner–Intermediate Cybersecurity & Networking Project

This project demonstrates core network security configurations using Cisco Packet Tracer.
The lab uses basic network equipment to showcase how security can be applied on real Cisco devices, including router hardening, SSH secure access, ACL firewall rules, VLAN segmentation, and switch port security.

# Topology Diagram

(Save and include the network diagram image in your repo — the one I generated for you.)

Router (Cisco 2911)
        |
Switch (Cisco 2950T)
   ┌────┴─────┬─────┐
 PC1       PC2     PC3

# Lab Objectives

This lab demonstrates how to:

  1. Harden a Cisco Router

Encrypt all passwords

Configure SSH remote access

Disable insecure services

Set login banners

Restrict administrative access

 2. Apply Firewall Rules (ACLs)

Permit only specific subnets

Block unauthorized traffic

Control access to the router

 3. Configure Switch Port Security

Limit allowed MAC addresses

Use sticky MAC learning

Prevent rogue device connections

4.  VLAN Segmentation

Separate user groups

Improve security boundaries

5. Logging & Monitoring

Configure Syslog

Enable security-related logs

Monitor interface violations

🛠️ Devices Used
Device	Model	Purpose
Router	Cisco 2911	Secure gateway, ACLs, SSH
Switch	Cisco 2950T	VLANs, port security
PCs (3)	Generic	Network hosts
🔧 Router Configuration (Cisco 2911)
! Encrypt passwords
service password-encryption

! Set hostname
hostname R1

! Disable DNS lookup
no ip domain-lookup

! Create admin user
username admin privilege 15 secret Admin@123

! Configure domain
ip domain-name lab.local

! Generate RSA key for SSH
crypto key generate rsa
1024

! Enable SSH v2
ip ssh version 2

! Secure VTY lines
line vty 0 4
 transport input ssh
 login local
 exec-timeout 5 0

! Console line security
line console 0
 password cisco123
 login
 exec-timeout 5 0

! Secure privileged mode
enable secret StrongPassword!

! Add security banner
banner motd #
⚠️ UNAUTHORIZED ACCESS PROHIBITED!
All activity is monitored.
#

! Example ACL (Allow PC1 network only)
access-list 10 permit 192.168.1.0 0.0.0.255
access-list 10 deny any

! Apply ACL to VTY access
line vty 0 4
 access-class 10 in

🔧 Switch Configuration (Cisco 2950T)
! Set hostname
hostname SW1

! Disable unused ports
interface range fa0/10 - 24
 shutdown

! Enable port-security on PC ports
interface fa0/1
 switchport mode access
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation restrict
 switchport port-security mac-address sticky

interface fa0/2
 switchport mode access
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 switchport port-security mac-address sticky

interface fa0/3
 switchport mode access
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky

📁 Repository Structure
Network-Security-Lab/
│
├── diagram.png
├── NetworkSecurityLab.pkt
├── router-config.txt
├── switch-config.txt
└── README.md

✅ Skills Demonstrated

This project proves hands-on knowledge in:

Cisco router & switch configuration

SSH secure administration

ACL firewall implementation

Port security & network hardening

Network segmentation

Documentation & diagramming

Using Packet Tracer for cybersecurity labs

📘 How to Use This Lab

Clone the repository

Open the .pkt file in Cisco Packet Tracer

Review configs in the config/ folder

Modify rules to test different security scenarios

Use the lab as part of a cybersecurity portfolio

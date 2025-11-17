Network Security Lab – Packet Tracer (Beginner Level)

This lab demonstrates basic network security configurations using Cisco Packet Tracer, including router hardening, SSH secure remote access, ACL firewall rules, and switch port security.

1. Topology

Devices you will use in Packet Tracer:

1 Router (R1)

1 Switch (SW1)

2 PCs (PC1, PC2)

1 Server (Web Server)

(Create this topology in Packet Tracer before starting.)

2. IP Addressing Plan
Device	Interface	IP Address	Subnet Mask	Default Gateway
Router	G0/0	192.168.1.1	255.255.255.0	—
PC1	NIC	192.168.1.10	255.255.255.0	192.168.1.1
PC2	NIC	192.168.1.11	255.255.255.0	192.168.1.1
Server	NIC	192.168.1.100	255.255.255.0	192.168.1.1
3. Router Security Configuration (R1)
3.1 Set Basic Security
enable
configure terminal
hostname R1
no ip domain-lookup
service password-encryption

3.2 Configure Local User Login
username admin privilege 15 secret Cyber@123
enable secret Admin@123

3.3 Configure SSH Only (Disable Telnet)
ip domain-name amos.local
crypto key generate rsa modulus 1024
line vty 0 4
transport input ssh
login local

3.4 Apply Basic Firewall ACL

Only allow internal network to access the router:

access-list 10 permit 192.168.1.0 0.0.0.255
line vty 0 4
access-class 10 in

4. Switch Security Configuration (SW1)
4.1 Set Hostname
enable
configure terminal
hostname SW1

4.2 Configure Port Security

Apply on Fa0/1 for PC1:

interface fastEthernet 0/1
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation restrict
exit


Repeat same for port Fa0/2 for PC2.

5. Server Configuration

On the server GUI:

Enable HTTP

Enable DNS

Set IP → 192.168.1.100

6. Security Testing
✔ 6.1 Test Connectivity

From PC1:

ping 192.168.1.1
ping 192.168.1.100

✔ 6.2 Test SSH Login

From PC1:

ssh -l admin 192.168.1.1


If login works, SSH is correctly configured.

✔ 6.3 Test Port Security

Disconnect PC1 cable from Fa0/1

Plug PC1 into Fa0/3

SW1 should show:

Port violation

Restrict/block traffic

✔ 6.4 ACL Test

Try to SSH from an IP outside the 192.168.1.0/24 subnet.
It should be blocked.



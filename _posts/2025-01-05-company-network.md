---
title: "Network Configuration"
date: 2025-01-05 00:00:00 +0800
categories: [NETWORKING]
tags: [CISCO, NETWORKING, ROUTING AND SWITCHING, SUBNETTNG, LAN SETUP, TOPOLOGY, NETWORK DESIGN, NETWORK ADMIN]
---

# Company Network

This company is a fast-growing in Puerto Rico with more than 2million customers globally. The company is intending to open a branch near the locally village in Puerto Rico. Thus, the company requires young IT graduates to design the network for the branch. The network is intended to operate separately from the HQ network.

Being a small network, the company has the following requirements during implementation:

1. One router and on switch to be used. 
2. 3 departments (Admin/IT, Finance - HR & Customer Service -  Reception).
3. Each department is required to be in different VLANS.
4. Each department is required to have wireless network for the users.
5. Host devices in the network are required to obtain IPV4 automatically.
6. Devices in all the departments are required to communicate with each other.

Assume the ISP gave out a base network of 192.168.1.0, you as the young network engineer who has been hired, design and implement a network considering the above requirements.

# Network Topology

![image](https://github.com/user-attachments/assets/13d52aca-49db-4000-8886-72b1a3aec5b8)


# Subnetting

There are 3 department so we need 3 different network.

This will give us:
- Subnet Mask of 255.255.255.192
- /26
- 4 networks
- 64 host (ID - Broadcast = 62 hosts)

1st Subnet
- Network ID
	- 192.168.1.0
- Broadcast
	- 192.168.1.63
- Hosts Range
	- 192.168.1.1 to 192.168.1.62

 2nd Subnet
- Network ID
	- 192.168.1.64
- Broadcast
	- 192.168.1.127
- Hosts Range
	- 192.168.1.65 to 192.168.1.126

3rd Subnet
- Network ID
	- 192.168.1.128
- Broadcast
	- 192.168.1.191
- Hosts Range
	- 192.168.1.129 to 192.168.1.190

4th Subnet
- Network ID 
	- 192.168.1.192
- Broadcast
	- 192.168.1.255
- Hosts Range
	- 192.168.1.193 to 192.168.1.254

## Additional Info

Base Network: 192.168.1.0

No. of subnets = 3

No. of subnets = 2^n == No. of borrowed bits

2^n = 3 //// 2^2= 4

4 borrowed bits

Class C = 255.255.255.0 = 11111111.11111111.11111111.11111111

Network requirements: 11111111.11111111.11111111.11000000

/26

255.255.255.192

# Devices

![Pasted image 20250104233221](https://github.com/user-attachments/assets/69fe24f7-5c5d-459b-aeff-c1aa6ed257e4)


#Configurations

## VLAN

Configuring VLAN on the switch

- Click switch
- CLI
- enable
- conf t
- int rang {}
- switchport mode acc (to configure VLAN)
- switchport access VLAN
- *creating VLAN*
- Repeat steps for the other VLAN's
- do wr
- Done configuring VLANs

![Pasted image 20250105002316](https://github.com/user-attachments/assets/31efb065-cca3-4464-af77-f35dc7f0f1ba)


## Wireless Access Points

- Click AP
- Config
- Port 1
- Change SSID
- WPA2
- Password
- Repeat steps

![Pasted image 20250105002713](https://github.com/user-attachments/assets/471292e0-f27c-4392-a5b9-aeb8babd59e9)


## Trunking

**Trunk Port**: A trunk port is a network port configured to carry traffic for multiple VLANs. Unlike a regular access port, which typically carries traffic for a single VLAN, a trunk port can carry traffic for many VLANs simultaneously.

- int {interface number}
- switchport mode trunk
- do wr

  ![Pasted image 20250105003555](https://github.com/user-attachments/assets/b6a407c1-18bf-43bf-919c-b51f9293a0ef)


  ## Router

- Router if off as default
- en
- conf t
- int {interface number}
- no sh (no shutdown)
- do wr

![Pasted image 20250105003920](https://github.com/user-attachments/assets/193bbde6-f38b-460a-8088-6641b885b06b)


## Intern-VLAN

Inter-VLAN Routing refers to the process of routing network traffic between different VLANs (Virtual Local Area Networks) within a network. Since devices in different VLANs cannot communicate directly with each other (due to VLAN isolation), inter-VLAN routing enables communication between these VLANs by routing the traffic through a router or a Layer 3 switch.

### Creating Sub-Interface
 - en
 - conf t
 - int {interface}.{VLAN number}
	 - int gig 0/0/0.10
- encapsulation dot1Q {VLAN number}

Now lets assign this sub-interface as the default gateway for this VLAN

- ip address and subnet mask
- exit
- repeat steps for other VLAN

![Pasted image 20250105005646](https://github.com/user-attachments/assets/447eafa0-94d9-41de-8438-44def75a60c7)


## DHCP 

I will configure DHCP in the router. 

- click router
- service dhcp

Now we want to create dhcp pools

- dhcp pool {Example Pool}
	- ip dhcp pool Admin-Pool
	- This pool represents the Admin VLAN

Assign network address to the pool

- network {network id} {subnet mask}
	- network 192.168.1.0 255.255.255.255

Create default gateway which is going to be the sub-interface on the VLAN
- default-router {sub-interface ip}
	- default-router 192.168.1.1

- Repeat step for dns server
	- dns-server {sub-interface ip}
- domain-name {example.com}
- do wr

Now the devices on this VLAN will get IP automatically. Repeat steps for the other VLANs

![Pasted image 20250105011607](https://github.com/user-attachments/assets/8a9a6bbc-a640-4420-b5bb-75aa969dd097)


Change IP configuration of the devices. enable DHCP.

# Adding Devices To Test AP

## Smartphone
- Click smartphone
- Config
- Wireless0
- SSID
- Authentication
- Review dhcp 

![Pasted image 20250105012615](https://github.com/user-attachments/assets/4739745f-78c9-4307-8afc-589fedb0125c)


## Laptop

To connect laptop, the device needs a wireless module.

- Turn off laptop
- remove existing module
- insert WPC300N module
- Turn on

Connecting the laptop to the access point
- Click on laptop
- Desktop
- PC Wirless
- Connect
- Choose correct SSID

![Pasted image 20250105013549](https://github.com/user-attachments/assets/ec968ed7-0656-4646-89ba-619272570504)


## Tablet

- Click on tablet
- Config
- Wireless0
- SSID
- Authentication
- review connection and DHCP

![Pasted image 20250105013753](https://github.com/user-attachments/assets/f9b0a577-adb1-450a-a533-d7db751e84bc)


Now to finish the configuration test that the devices can communicate with each other.


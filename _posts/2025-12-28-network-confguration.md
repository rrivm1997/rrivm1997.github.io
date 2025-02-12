---
title: "Network Configuration"
date: 2024-12-28 00:00:00 +0800
categories: [NETWORKING]
tags: [CISCO, NETWORKING, ROUTING AND SWITCHING, SUBNETTNG, LAN SETUP, TOPOLOGY, NETWORK DESIGN, NETWORK ADMIN]
---

# Network Configuration

I will be creating a basic Cisco network configuration. It will be composed of four (4) computers, two (2) switches, and one (1) router.


# Computers

Computers are a general-purpose computer designed for use by an individual. It can refer to desktops, laptops, and other computing devices used for personal tasks such as word processing, browsing the internet, and gaming.

![Pasted image 20241228164753](https://github.com/user-attachments/assets/b5ec143e-7774-4408-a7f7-afb7db03513d)


# Switches

In computer networking, a **switch** is a device that connects multiple devices (such as computers, printers, and servers) within a local area network (LAN). It manages data traffic by forwarding data packets to the correct destination device based on its MAC (Media Access Control) address.

![Pasted image 20241228170133](https://github.com/user-attachments/assets/5b77da68-a169-4bc7-9edd-585f2708ff20)


# Router

A network router is a device that forwards data packets between computer networks, typically between a local area network (LAN) and the internet. Routers serve as the traffic directors of a network, ensuring that data travels efficiently from one network to another.

![Pasted image 20241228171322](https://github.com/user-attachments/assets/a821be92-4cb5-4b63-b29a-9b8ae4d7b2e6)


# Connecting PC To Switch

The computers are going to be connected to the switches with Copper Straight-Through. 

```
A Copper Straight-Through Cable refers to a type of twisted-pair copper cabling that is typically used to connect network devices, such as computers, routers, switches, and hubs. This cable is primarily used for Ethernet connections.
```

 **FastEthernet01** (often written as **FastEthernet0/1**) is a term commonly used in networking, particularly when referring to **Ethernet ports** on network devices like routers and switches. It denotes a specific interface or port that is part of a network device's hardware.

Here's what you need to know about **FastEthernet01**:

### **Fast Ethernet**

- **Fast Ethernet** refers to **Ethernet technology** that supports data transmission speeds of **100 Mbps** (megabits per second). It is a step up from the original **10 Mbps Ethernet** (often referred to as 10Base-T).
- **FastEthernet0/1** is typically used to refer to one of the network ports on a device that supports this speed. In the context of modern networks, **Gigabit Ethernet** (1 Gbps) and **10 Gigabit Ethernet** (10 Gbps) are more common, but Fast Ethernet is still in use, especially in smaller or older networks.

![Pasted image 20241228174521](https://github.com/user-attachments/assets/d83cad20-87a2-4a07-877c-44787bb2fd4f)


# Connecting Switch To The Router

The switches are going to be connected to the switches with Copper Straight-Through. 

**Gigabit Ethernet** (GigE) is a widely used networking technology that supports **1 Gbps** speeds, allowing fast, reliable data transfer in modern networks. It operates over both **copper (Cat5e, Cat6)** and **fiber optic cables** and is commonly used in switches, routers, and network cards to provide high-speed connectivity. It is ideal for environments with high network traffic, such as offices, data centers, and homes with high-bandwidth needs.

![Pasted image 20241228175054](https://github.com/user-attachments/assets/4caa0646-2376-46f9-a4fe-7911f20e41a3)


# Configuration

There are red light in the cables between the switch and the router meaning there is no established connection.

## Configuring The Router Ports

Clicking the router and going to CLI mode:

![Pasted image 20241228175543](https://github.com/user-attachments/assets/815b4aa6-1b4d-49be-b991-0af1bd7b6c51)

I see the following question:
```
Would you like to enter the initial configurgation dialog? [yes/no]:
```
`No`

Now I am in user executing mode. 

I will type:
- enable 

Now I am in privilege mode.

I will type:
- configure terminal

Now I am in the group global configuration mode.

#### Configuring The Interface

I will type:
- interface {interface name}. In this case `interface g0/0`
- Assign ip address with subnet mask
- No shutdown

The port has been configured.

![Pasted image 20241228180548](https://github.com/user-attachments/assets/321605e1-8e1b-48ec-bf7e-faf20f0d802e)

Green Light meaning connection established.

![Pasted image 20241228180655](https://github.com/user-attachments/assets/6d164138-f5a0-4ced-9523-abf989020416)

Now I will configure the other interface by doing the same steps shown above.

*NOTE:*
```
When assigning IP ADDRESS, two different networks need to be configure for it to work.
```

![Pasted image 20241228181059](https://github.com/user-attachments/assets/a07c4bfd-3244-4979-b31d-08585495b94d)

Connection established.

![Pasted image 20241228181144](https://github.com/user-attachments/assets/35940825-c754-460b-b3c4-bed21e11140c)

## Configuring The PC

I will assign IP address to the pc as follow:
- Click PC
- Desktop
- IP Configuration
```
IPv4 address will be 192.168.1.10
Subnet mask 255.255.255.0

For the Default Gateway I will type the IP of the exiting router which is 192.168.1.1.
```

![Pasted image 20241228181942](https://github.com/user-attachments/assets/abcf1104-7761-4f0d-b3a7-5a40e0cdb8e9)

I will apply the setting to the other PC as required.

![Pasted image 20241228182156](https://github.com/user-attachments/assets/08c9dbbe-832c-4b4a-967a-c1b93a779faa)

**Now I am going to test the connections**


# Sending Messages

## A Simple PDU

```markdown
In networking, a **PDU (Protocol Data Unit)** is a unit of data that is transmitted across a network at various layers of the OSI (Open Systems Interconnection) model. Each layer adds its own header (and sometimes trailer) to the data, which results in the creation of a PDU at that layer.
```

In a simple **PDU message**:

- **Application Layer**: "Hello, how are you today?".
- **Transport Layer**: "Segment" with transport info (e.g., ports, sequence).
- **Network Layer**: "Packet" with IP headers.
- **Data Link Layer**: "Frame" with MAC addresses.
- **Physical Layer**: "Bits" representing the data.

I send a successful PDU message from:
- PC0 to router.
- PC2 to router.
- PC0 to PC2.

![Pasted image 20241228182745](https://github.com/user-attachments/assets/464b69cf-1658-4899-86b6-6a13a87b138f)

![Pasted image 20241228182903](https://github.com/user-attachments/assets/cefce326-f89c-4b2d-b50c-dc2a52680f5b)

![Pasted image 20241228183122](https://github.com/user-attachments/assets/d709cc6e-0e63-4d43-9399-b8073eb90887)


# Connection Established




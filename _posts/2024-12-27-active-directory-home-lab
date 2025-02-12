---
title: "Active Directory Home Lab"
date: 2024-12-27 00:00:00 +0800
categories: [ACTIVE DIRECTORY, HOME LAB]
tags: [ACTIVE DIRECTORY, WINDOWS SERVER, DOMAIN CONTROLLER, VM, NETWORKING, DHCP, DNS, POWERSHELL]
---

# Active Directory Home Lab

# Network Diagram

![image](https://github.com/user-attachments/assets/9b7e53f3-814a-49fb-a1e6-2f4b225e0298)

## High Level Overview

- Download and install Oracle VirtualBox to run our virtual machines.
- Download Windows 10 ISO and Server 2019 ISO.
- Create our first virtual machine wichh is going to be our Domain Controller which is going to house Active Directory.
  -  This virtual machine will have two network adapters:
     -  One for external connection to the internet.
     -  One private network that the client will connect to.
- Install server 2019 in the virtual machine and assign ip addressing to the internal network.
    - External network will get ip addressing for our home router.
- Name the server.
- Install Active Directory and create our domain.
- Configure NAT and Routing so the clients on the private network can reach the internet through the domain controller.
- Create a Dynamic Host Configuration Protocol (DHCP) so when we create our Windows 10 machine it can get automatically ip address.
- Run a PowerShell script to creak +1K users. (https://github.com/rrivm1997/AD_PS_USRS)
- Create another virtual machine and install windows 10 on it and it will be connected to the private virtual box network
- Name the machine Client1 and join it to the domain and then we are going to log into it with one of our domain accounts. 

# Windows Server 2019 

I will be creating the first virtual machine:
![image](https://github.com/user-attachments/assets/c4cd816c-9dd2-476f-824d-6884d9abc1b3)

Applying 2048 MB and 4 CPU.
![image](https://github.com/user-attachments/assets/195db44b-2600-4217-ba2e-80b691e72fc8)

Hard Disk defaults.
![image](https://github.com/user-attachments/assets/5350d727-336e-4b82-b1af-58fb1ede5c5e)

Summary.
![image](https://github.com/user-attachments/assets/d8d6267d-e103-415d-b952-0bc881fa7a4a)

Before adding the ISO, lets configure some settings.

Changing to bi-direction so that we can share clipboard and files withing host machine and virtual machine.
![image](https://github.com/user-attachments/assets/74f18517-ac8a-4edb-a5ce-5cd8cd6c2e23)

Since this is our Domain Controller we will want to add not NICs.
  - One dedicated for the internet.
  - One dedicated for the internal network.

Aapter 1 - NAT will connect to our house internet.
![image](https://github.com/user-attachments/assets/4626fb4c-5e20-449a-b60f-6a5961966a39)

Adapter 2 - Internal Network with the name 'intnet'.
  - Every Internal Network with the same name will be part of the same internal network.

![image](https://github.com/user-attachments/assets/a57e807a-1846-491c-89d8-209502e5fc13)

Lets power up the machine...

Since nothing is install, we'll get this pop up:
- ![image](https://github.com/user-attachments/assets/4bd9d27b-a5b4-4971-84ab-a4c4b45d216e)

Add the ISO and start the machine. 
- ![image](https://github.com/user-attachments/assets/7dadb075-1edf-4301-b5fd-e6d76180097d)

Click next.
- ![image](https://github.com/user-attachments/assets/af956645-57ba-4952-b54d-a78fecbd96b8)

Install Now.
- ![image](https://github.com/user-attachments/assets/b2cb5e0e-eff2-4530-9064-deaef0b73f78)

Select either of the Desktop experience. The other two will be command lines.
- ![image](https://github.com/user-attachments/assets/43217f4e-3af9-4ddb-81e2-cb08dd3861c6)

Accept terms.
- ![image](https://github.com/user-attachments/assets/fa9bb289-005f-47e7-bd2a-f0aa1842e982)

Choose Custom install.
- ![image](https://github.com/user-attachments/assets/68dd9872-ed23-42a4-8f05-f041453dbf15)
  
Clicking Next.
- ![image](https://github.com/user-attachments/assets/40348d76-6439-4a09-a09f-56b3d7162ba4)

Aaaaand Windows Server 2019 is installed. 
- ![image](https://github.com/user-attachments/assets/ee13dd4c-8e71-449a-93c2-28b3898ca12b)

# Lets make our experience better

On our Virtual Machine:

- Devices
- Insert Guest Addition CD image
- Open File Explorer
- This PC
- CD Drive (D:) VirtualBox Guest Additions
- Run VBoxWindowsAdditions-amd64
- Reboot later
- Shut VM down
- Start VM 

# Setting Our IP Addressing

Click on the bottom right the network icon.
![image](https://github.com/user-attachments/assets/8d4d98b0-4bf0-476a-bebf-b4def0da2fc1)

Network & Internet settings.
![image](https://github.com/user-attachments/assets/509d50ac-902f-4c50-84a8-90fd4b7fbd54)

Change adapter options
![image](https://github.com/user-attachments/assets/96d01c0d-c0ea-4936-93f2-a389c886ed21)

From here we need to find out which is our internet adapter and which is the internal adapter. We do this by:
  - Right click
  - Status
  - Details
  - IPv4 Address

Once I identify which adapter is which, I named them. 
![image](https://github.com/user-attachments/assets/0ee79b90-cfee-4cc2-81fe-8a12c9790b3f)

## Lets assigned the IP to our internal network
- Right click internal adapter
- Properties
- Click IPv4
- ![image](https://github.com/user-attachments/assets/c3378c23-4d9b-454a-8850-971dad253d33)

Now I will assigned the IP  and Subnet mask as we saw on the Network Diagram.
  - No gateway will be added because the DC will serve as the default gateway.
![image](https://github.com/user-attachments/assets/a11182d6-1713-4d6e-aed0-0044cab2c509)


## DNS Server

Once Active Directory is install it automatically install DNS so this server is going to use itself as the DNS server. 
- I can use the servers IP Address or the loop back address which is 172.0.0.1
![image](https://github.com/user-attachments/assets/2b332241-1965-4ad3-8e4a-8fbd2ba69462)


# Naming our PC
- Right Click Start Menu
- System
- Rename this PC
![image](https://github.com/user-attachments/assets/63827b4d-b610-4274-aa63-1619b16f56d3)

# Installing Active Directory Domain Services (AD DS)

Open Server Manager
   - Add roles and features
   - Next
   - Role-based or feature based installation
   - Select Server
   - Choose AD DS
   - Add features
   - Next
   - Install
![image](https://github.com/user-attachments/assets/ff299ac6-14d3-4a75-b8ab-36bc0fb7cd98)

We see a flag with a warning sign which is a notification. This indicates that we need to do our Post-deployment configuration. We install the software, but the domain has not been created yet.

Lets click it.
![image](https://github.com/user-attachments/assets/19bc4197-f323-4666-9ef2-99475b402ef2)

On the Deployment Config page, select Add new forest and give it a name.
![image](https://github.com/user-attachments/assets/392ad154-cca5-4002-af3d-aa5054a24ad3)

Click next until installation and reboot. 

# Creating Our Own Dedicated Domain Admin Account

We do this by:
- Click start.
- Windows Administrative tools.
- Active Directory Users and Computers.
![image](https://github.com/user-attachments/assets/95519cf8-b418-484e-9858-00f0893b1c48)

We see our newly created domain. In here, let's create an Organizational Unit to put our admin account in.
![image](https://github.com/user-attachments/assets/847f89be-ed3d-424c-862f-b863fffcece5)

Naming the new object.
![image](https://github.com/user-attachments/assets/5bac6f9d-748b-45c0-a025-71e0dad5a2d3)

Inside of the folder, I will create a new user.
- Right click.
- New.
- New user.
- Add the fields as suggested by the company.
![image](https://github.com/user-attachments/assets/6a192594-0652-47bb-bc1d-56a90eaa6476)

Account created. Now it needs to be changed to admin.
![image](https://github.com/user-attachments/assets/d3cb9c93-7ba7-4927-a17a-d494f096f3f6)

To do this:
- Right click user.
- Properties.
- Member Of.
- Add.
- Type Domain Admins.
- Check Names.
- OK.
![image](https://github.com/user-attachments/assets/390a0272-b696-415e-9204-b00f0c0481c7)

Lets log out an use our new account. 

On Other user I will input my new created account.
![image](https://github.com/user-attachments/assets/b664931a-da41-425a-9968-fd1fb2e67c8c)


# Installing Remote Access Server (RAS) and Network Address Translation (NAT)

This is to allow our Windows 10 Client to be in the private virtual network but still allow it to access the internet through the Domain Controller. 

## Install

- Open Server Manager.
- add roles and features.
- Next.
- Select our server.
- Next.
- Remote Access.
- Next.
- Select Routing.
- Next.
- Install.
![image](https://github.com/user-attachments/assets/a22aae42-72d3-421a-b4b0-3556defd2182)

After installation:
- Click tools
- Routing and Remote Access
![image](https://github.com/user-attachments/assets/bb2f8ec9-b22c-41fa-b091-106f87e73d37)

Now:
- Right click DC (local).
- Config and Enable.
- Next.
- NAT to allow internal client to connect to the internet. 
- Next.
- Choose the correct adapter to allow internet access.
- Finish

Now we see that the DC has an up green arrow so now its configured.
![image](https://github.com/user-attachments/assets/7bc2a2a8-a9ff-47d5-b817-3b449962558d)

# Configuring DHCP Server On Our DC With The Scope Information

This willa allow our Windows 10 client to get an IP adress and be able to browse the internet. 

## Installing

- Open Server Manager.
- Add roles and features.
- Next.
- Next.
- Choose server.
- DHCP Server.
- Next until install.

After instalaltion:

- Tools.
- DHCP.

Notice how the servers are red meaning they are down.
![image](https://github.com/user-attachments/assets/e51c6626-1757-4cff-8a5a-a27648bb06c8)

### Setting scope
- Right click server.
- New Scope.
- Next.
- Name.
![image](https://github.com/user-attachments/assets/debc63de-cdb0-4ea2-998a-b5d999bb1fc5)

Set scope
![image](https://github.com/user-attachments/assets/03036ddc-785e-4e4b-a44f-816389c26e81)

- Add exclusions if neccesary.

- Lease Duration will depend on use case. 

- Configure DHCP Options, YES.

- Default gateway will be our Domain Controller since we setted up our RAS/NAT there.
![image](https://github.com/user-attachments/assets/b445b691-f950-4a15-a651-8c6be11e0950)

- Domain Namde and DNS Servers.
   - AD on the DC automatically install DNS.
 
- Dont care about WINS Servers.

- Activate Scope.

- Finish.
 
Now we need to Authorize and Refresh our server.
  - Right click DC.
  - Authoriza.
  - Right click DC.
  - Refresh.
Now we see servers are green. 
![image](https://github.com/user-attachments/assets/0205e41a-c537-4352-88a5-80c9db45389e)

![image](https://github.com/user-attachments/assets/6b3701a0-93f1-4ca9-88e7-2b7db70bca7f)

# Accessing The Intenert With The DC
 - NOTE: THIS IS A LAB SO THIS CAN BE DONE. DO NOT DO THIS STEP ON A PROD ENVR.
 - I am doing this to make it easy on me and download the script.
![image](https://github.com/user-attachments/assets/b90a3def-0ac2-47a3-a2e6-b60e6c47a750)


# Creating Users With a PowerShell Script in AD

- Openning PowerShell ISE.
![image](https://github.com/user-attachments/assets/93116005-3346-4a06-8d38-86b1d7a94f95)

- Open the PowerShell script.
![image](https://github.com/user-attachments/assets/9187a475-7718-4063-96d7-56dbbe22e7d7)

## Enable execution of scripts

- Only do this on labs
  - Set-ExecutionPolicy Unrestricted.
  - Change directory to where the script was saved.
  - Run it.
![image](https://github.com/user-attachments/assets/15f064c1-346a-4a0b-9c39-f387785ea354)

All our users have been created.
![image](https://github.com/user-attachments/assets/5808b539-f238-4230-80a4-9daf14837f02)

![image](https://github.com/user-attachments/assets/0e95753d-336b-4044-a146-660751350cc6)

# Creating The Windows 10 Virtual Machine

I will do the same steps as I did with the Windows Server 2019 virtual machine. 

![image](https://github.com/user-attachments/assets/ecc4b9f9-821e-4358-adc8-5b4868a488c0)

Now lets make sure that the internet is working. 
- IPv4.
- Default Gateway.
- Ping.
- DNS resolve.
![image](https://github.com/user-attachments/assets/d93fee97-2ef8-461f-b3ce-bac71ff975d1)

## Additional Settings
- Change PC name
- Join Domain
- Restart
![image](https://github.com/user-attachments/assets/3ccee68e-6e2f-4e1a-b5e2-86875dec2ad1)

After restarting, log in using one of the accounts created by the script.
![image](https://github.com/user-attachments/assets/ab089c67-c596-40c0-92fc-6295f8f27af5)


# HOME LAB CREATED 



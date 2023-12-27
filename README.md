<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure (DC-1 & client-1)
- Check connectivity between Client 1 and Domain Controller
- Install Active Directory
- Join Client-1 to your domain (JordanWest.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create Additional Users and confirm ability to log into Client-1

<h2>Deployment and Configuration Steps</h2>
<h3>Setup Resources in Azure</h3>

- Create Domain Controller VM (Windows Server 2022) name "DC-1" in Microsoft Azure
![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/c082a50f-5eaf-4789-8075-69af0ac17e37)

- Create: Azure Virtual Machine
- Virtual Machine Name: DC-1
- Region: Which ever Region you use needs to be the same on DC-1 and Client-1
- Image: Windows Server 2022
- Size: 2vcpus, 16 GiB Memory
- Username & Password (take note of both)
- Review + Create
- Create
- (Take 10 minute break for the deployment of DC-1 to finish, we will use the same Resource Group and Virtual Network for Client-1)
- Select DC-1 VM
- Network Settings
- Select "Network interface/IP configuration"

![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/26d5f969-5d22-4fef-8ed8-f4ca9a105fa4)

- Take note that the Private IP Address is set to Dynamic
- Select ipconfig1

![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/86001b7c-1064-4124-b402-7398b5a22d62)

- Set Private IP address settings Allocation to Static
- Save

- Home
- Virtual Machines
- Create: Azure Virtual Machine
- Resource Group: DC-1_group (This resource group was created automatically when you created first VM)
- Virtual Machine Name: Client-1
- Region: Same as Region set in DC-1
- Image: Windows 10
- Size: 2vcpus, 16 GiB Memory
- Username & Password
- Check box "I confirm I have an eligible Windows10/11 license with multi-tenant hosting rights"
- Click Next
- Click Next
- Virtual Network: DC-1-vnet (this vnet was automatically created when we set up Dc-1)
- Review + Create
- Create

<h3>Ensure Connectivity between DC-1 and Client 1</h3>

- Using Remote Desktop log in to Client-1
![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/fc611c98-3283-49ca-8f54-91822d5bb2af)

- Use IP Address from Azure Portal
- Input Username and Password from Client-1 VM creation
- You can select no on all privacy settings
- WinKey + R
- cmd
- ping -t 10.0.0.4 (the static IP address for DC-1)
- You will recieve request timed out
- Log in to DC-1 via Remote Desktop
![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/0e3cb3ea-16bf-480f-bd20-5f3a0e6ed705)

- Type wf.msc into windows search bar
- Inbound Rules
- Sort by Protocol
- Scroll down to ICMPv4
- Enable both "Core Networking Diagnostics - ICMP Echo Request(ICMPv4-In)"

![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/8c52f05b-f960-4e3a-90a7-bb666668bd16)

- Return to Client-1 Remote Desktop to see that your ping is succeeding

<h3>Install Active Directory</h3>

- Log in to DC-1 via Remote Desktop
- In the Server Manger Dashboard select Add roles and features
- Next
- Role-based or feature-based installation
- Next
- Select a server from the server pool: DC-1
- Next
- Select Active Directory Domain Services
- Add Features
- Next
- Next
- Next
- Install
- AFter installation, select flag in top right corner with yellow indicator
- Promote this server to a domain controller
- Add a new forest
- JordanWest.com (whatever domain name you want)
- Input a password (DSRM we will not use)
- Next
- Next
- Once NetBIOS domain name autofills, select Next
- Next
- Next
- Install
- Once installation is complete server will automatically restart and disconnect you from Remote Desktop
- Log back in as JordanWest.com\labuser ("domain name\Username")

<h3>Create an Admin and Normal User Account in Active Directory</h3>

- In Server Manger select tools
- From the drop down menu select Active Directory Users and Computers
- Right-click JordanWest.com (name of your Domain Conttroller)
- Select New
- Organizational Unit
- Name it "_EMPLOYEES"
- Create another Organizational Unit named "_ADMINS"
- 


</p>
<br />

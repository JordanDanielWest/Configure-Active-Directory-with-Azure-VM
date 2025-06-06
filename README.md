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
- Virtual Network: DC-1-vnet (this vnet was automatically created when we set up DC-1)
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
- After installation, select flag in top right corner with yellow indicator
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
- Create another Organizational Unit name "_CLIENTS"
- Create another Organizational Unit named "_ADMINS"
- Create new employee named Jane Doe Inside "_ADMINS"

![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/aceecbd9-4c3b-4ded-a1b4-a175707b7809)

- User logon name: jane_admin
- Next
- Create password
- Chek "Password never expires"
- Next
- Finish
- Richt-click Jane Doe
- Properties
- Member Of
- Add
- Domain Admins
- OK
- Apply
- Log out and then log back in as jane_admin

<h3>Join Client-1 to your domain (JordanWest.com)</h3>

- From Azure Portal, set Client-1's DNS settings to the DC-1's Private IP Address
- First get DC-1 private IP address from Azure VM
![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/2d8d499d-064a-4529-9ee5-1f34a3bb9775)

- Go to Client-1 Network Settings
- Click Network interface/IP configuration

![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/3d035a75-c898-4d37-81db-ae5407c4b14b)

- DNS Servers
- Custom
- Input DC-1's Private IP Address

![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/2dcdef92-49ed-4992-8abe-1e10acc76422)

- Save
- Restart Client-1 from Azure
- Log in to Client-1 via Remote Desktop
- In Command Line use ipconfig /all to confirm DNS Server is same as DC-1's IP Address
![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/31725425-801b-4c91-9773-ea83cd575852)

- WinKey + X
- System
- Rename this PC
- Change
- Member of: Domain
- Enter domain name "JordanWest.com"
- Username: jordanwest.com\jane_admin (enter admin account we created)
- Enter Password
- Will recieve welcome message
- Client-1 will restart
- Log into DC-1 and confirm Client-1 shows up in Active Directory ussers and coomputer inside the "computers" container of the root domain

![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/bc9cc8ee-c09e-408a-a78d-a8881f61cfae)

- Move Client-1 into "_CLIENTS" folder for organizational purposes

<h3>Setup Remote Desktop for on-administrative users on Client-1</h3>

- Log into Client-1 as jordanwest.com\jane_admin and open system properties
- Remote Desktop
- Select users that can remotely access this PC
- Add "Domain Users"
- You can now log into Client-1 as a normal, non-administrative user

<h3>Create a list of additional users and attempt to log into Client-1 with one the</h3>

- Log into DC-1 as jane_admin
- Open PowerShell_ISE as administrator
- Create new file and paste contents of script into it
- [Script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
- Run Script
- When finished open Active Directory Users and Computers and observe the list has populated the _EMPLOYEES Organizational Unit
- Attempt to log into Client-1 with one of the accounts (take note of password in script)
- Done








</p>
<br />

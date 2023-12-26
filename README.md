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
- Which ever Region you use needs to be the same on DC-1 and Client-1
- Image: Windows Server 2022
- Username & Password (take note of both)
- Review + Create
- Create
- (Take 10 minute break for the deployment of DC-1 to finish, we will use the same Resource Group and Virtual Network for Client-1)
- Select DC-1 VM
- Network Settings
- Select "Network interface/IP configuration"
![image](https://github.com/JordanDanielWest/Configure-Active-Directory-with-Azure-VM/assets/96628562/26d5f969-5d22-4fef-8ed8-f4ca9a105fa4)



<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

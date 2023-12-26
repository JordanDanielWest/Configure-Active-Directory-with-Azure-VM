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
- Regions: Which ever Region you use needs to be the same on DC-1 and Client-1
- Image: Windows Server 2022
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
- 
- 


</p>
<br />

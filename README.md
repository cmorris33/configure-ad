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
- MAC OS 

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory 
- Joint Client-1 to domain
- Setup Remote Desktop for non-administrative users on Client-1


<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://imgur.com/XaDGQgW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
First we need to setup our resources in Azure. To create a resource group in Azure, sign in to the Azure portal, navigate to the Resource Groups page, click on "Add," provide the basic details such as subscription, resource group name, and region, click on "Review + create," and then click on "Create" to create the resource group. Once created, you can start adding Azure resources to the resource group for better organization and management. Afterwards we need to create our virtual machines.

</p>
<br />

<p>
<img src="https://imgur.com/RuLasq7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next thing would be to login to Client-1 and ping DC-1’s private IP address with ping -t <ip address> (perpetual). With doing this step we need to ensure that both the client and the domain controller are connected to the network properly. Next we are going to login to the Domain Controller and enable ICMPv4 in on the local Windows Firewall then check back at Client-1 to see the ping succeed. 

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to DC-1 and install Active Directory Domain Services. Promote as a DC: Setup a new forest as mydomain.com. Next, restart and then log back into the DC 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Active Directory Users and computers (ADUC) create two Organizational Units (OU). Then create a new employee with a username and password. Add the new employee to the "Domain Admins" Security Group. Log out/close the Remote Desktop connection to DC-1 and log back in as "mydomain.com\employee"
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To join Client-1 to your domain, first, from Azure portal, set Client-1's DNS settings to the DC's Private IP address. In Azure Portal, restart Client-1. Next login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart). Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the "computers" container on the root of the domain. Create a new OU and drag Client-1 into there. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To setup Remote Desktop for non-administrative users on Client-1, log into Client-1 as mydomain.com\employee and open system properties. Click "Remote Desktop". Allow "domain users" access to remote desktop. You can now log into Client-1 as a normal, non-admin user now. Normailly you would want to do this with Group Policy that allows to change many systems at once. 
</p>
<br />

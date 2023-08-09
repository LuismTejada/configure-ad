# Configuring On-premises Active Directory within Azure VMs
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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

Creating the domain controller will be the first step VM(Windows Server 2022) Name DC-1


After we will create a VM for a client the name will be”Client 1”. We will use the same Resources Group and Vnet that were previously created. 


Set Domain Controller's NIC Private IP address to be static.


Make sure that both VMs are in the same Vnet. You can check the topology with the network watcher.


Login to client-1 with Microsoft Remote Desktop and Ping DC-1 private IP address with pint -t which is a perpetual ping. 


The next step will be login to the Domain Controller and enable ICMPv4 on the local Windows firewall.


You have to go back to client-1 to make sure the ping succeeded. 


Login to Dc-1 and install Active Directory Domain Services.


Promote as a Domain controller


Next, you have to set up a new forest as anything that you remember. In my case, I decided to go for luistejada.com


Restart and log back in DC-1 as a user.


Now In Active Directory Users and Computers, create an organization unit name _EMPLOYEES and another called _ADMINS. 


Created a new employee you can do any random name in my case I went for “Jane Doe” and her username will be “jane_admin”. 


You have to add jane_admin to the Domain Admins Security Group. 


Log out from “luistejada.com\labuser” Close the connection to DC-1 and log back in with “luis tejada.com\jane_admin” Use jane_admin as your admin account from now on.

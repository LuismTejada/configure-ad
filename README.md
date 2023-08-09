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

<img width="1280" alt="Screen Shot 2023-08-09 at 12 40 52 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/8a8c190f-d578-4997-a752-5062ebcb88df">


After we will create a VM for a client the name will be”Client 1”. We will use the same Resources Group and Vnet that were previously created. 

<img width="1280" alt="Screen Shot 2023-08-09 at 12 43 57 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/0522f326-d941-406e-99af-161f1a4f0a5d">


Set Domain Controller's NIC Private IP address to be static.

<img width="1280" alt="Screen Shot 2023-08-09 at 12 49 06 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/26cad4c0-71dd-4471-9c26-06afc0c77ed6">


Make sure that both VMs are in the same Vnet. You can check the topology with the network watcher.

<img width="1280" alt="Screen Shot 2023-08-09 at 12 56 26 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/8f5e05b4-15e5-457c-9f07-9c8a0342eab5">


Login to client-1 with Microsoft Remote Desktop and Ping DC-1 private IP address with pint -t which is a perpetual ping. 

<img width="1280" alt="Screen Shot 2023-08-09 at 12 56 32 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/4694aafd-6776-4d37-b412-eae96482f4bd">

<img width="1280" alt="Screen Shot 2023-08-09 at 12 56 26 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/f2fbe87c-130c-4995-b490-00d3e45530b2">


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

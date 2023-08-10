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

<img width="1280" alt="Screen Shot 2023-08-09 at 7 12 07 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/0edefc6a-471a-466e-9880-26503aafdb11">


Login to client-1 with Microsoft Remote Desktop and Ping DC-1 private IP address with pint -t which is a perpetual ping.


<img width="1280" alt="Screen Shot 2023-08-09 at 7 20 37 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/20e62388-e6f0-4171-b817-cde1b325a60a">

The next step will be login to the Domain Controller and enable ICMPv4 on the local Windows firewall.

<img width="1280" alt="Screen Shot 2023-08-09 at 7 26 25 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/8a2b62df-04ab-45b9-830f-5ed087e9df2b">


<img width="1280" alt="Screen Shot 2023-08-09 at 7 26 36 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/ba634895-a8fb-4f33-b8c9-16b4c1355faf">

You have to go back to client-1 to make sure the ping succeeded. 

<img width="1280" alt="Screen Shot 2023-08-09 at 7 28 59 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/1387e3a7-4d6d-4dc3-9cef-1fc332293c5e">


Login to Dc-1 and install Active Directory Domain Services.


<img width="1280" alt="Screen Shot 2023-08-09 at 7 36 29 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/8c3db1f1-0bb9-44d7-828d-d8ca427fafd7">

Promote as a Domain controller

<img width="1280" alt="Screen Shot 2023-08-09 at 7 38 43 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/4590782e-654d-49ba-add7-5a7144565ef4">


Next, you have to set up a new forest as anything that you remember. In my case, I decided to go for luistejada.com

<img width="1280" alt="Screen Shot 2023-08-09 at 7 39 49 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/4d6b1d6d-f5b1-4c01-aaf0-8996e0fd50d8">


Restart and log back in DC-1 as a user.

<img width="1280" alt="Screen Shot 2023-08-09 at 9 13 56 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/baa89b99-3358-4365-b1a5-03d6263c08ab">

Now In Active Directory Users and Computers, create an organization unit name _EMPLOYEES and another called _ADMINS. 

<img width="1280" alt="Screen Shot 2023-08-09 at 9 22 21 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/38f581a9-e8f6-4c3f-aeea-9e6d6edcb2de">

<img width="1280" alt="Screen Shot 2023-08-09 at 9 21 43 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/4803b21b-2cd8-4620-8fd5-a5520dbb3981">

Created a new employee you can do any random name in my case I went for “Jane Doe” and her username will be “jane_admin”. 

<img width="1280" alt="Screen Shot 2023-08-09 at 9 28 17 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/39762b58-cd00-4902-a352-942857e92397">


You have to add jane_admin to the Domain Admins Security Group. 

<img width="1280" alt="Screen Shot 2023-08-09 at 9 29 54 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/0a5eadc8-e2f6-4be3-b5be-950c1af19c42">


Log out from “luistejada.com\labuser” Close the connection to DC-1 and log back in with “luis tejada.com\jane_admin” Use jane_admin as your admin account from now on.

<img width="1280" alt="Screen Shot 2023-08-09 at 9 33 26 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/9621ed86-aee2-448e-9bed-903655abea70">

Then you will have to go to the Azure Portal, set Client-1's DNS setting to the DC's Private IP address.

<img width="1280" alt="Screen Shot 2023-08-09 at 9 42 23 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/1cb0aa8b-d083-4f73-b1a2-135f6a08f2f9">

From the Azure Portal restart Client-1. Login to Client-1 as the original local admin (labuser) and join it to the domain. The computer will restart. 

<img width="1280" alt="Screen Shot 2023-08-09 at 9 54 38 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/33aa0148-aa8d-44ad-a4c8-119fbeebdc54">

Login to DC-1 as jane_admin. Open PowerShell_ise as an administrator. Create a new File and paste the contents of this script (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1 (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
) into it.

<img width="1280" alt="Screen Shot 2023-08-09 at 9 54 38 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/93f94c91-ded0-476a-94c9-e21534a2d49a">

After you copy and paste this script, you will run it and observe the account being created.

<img width="1280" alt="Screen Shot 2023-08-09 at 10 10 29 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/8d96f048-a03e-4f90-ab78-99fc9e3e5f60">

When the process is finally finish open Active Directory Users and Computer and observe the accounts in the appropiate OU and attempt to log in Clint-1 one of the accounts.

<img width="1280" alt="Screen Shot 2023-08-09 at 10 14 25 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/ec1276f7-a201-4023-bed0-426ffaf702d5">

<img width="1280" alt="Screen Shot 2023-08-09 at 10 35 40 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/e57327f5-f93f-4f45-a6da-a1c59629bbf8">

<img width="960" alt="Screen Shot 2023-08-09 at 10 33 00 PM" src="https://github.com/LuismTejada/configure-ad/assets/140201562/68d551f3-0a14-4111-bc39-a09c2955b9a2">

After everything is done make sure to delete the research group so you do not waste Azure credits.

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

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="592" alt="3 Install complete" src="https://github.com/DarianWells/Configure-Active-Directory/assets/132870202/e21fef55-f5f2-4224-ba55-7b216c9813ac">
</p>
<p>
Starting this lab by creating two virtual machines (VMs) in Microsoft Azure; one domain controller (DC-1) (Windows Server 2022) and one client PC (Client-1) (Windows 10). Established both VMs on the same virtual network. Assigned a static IP address and enabled ICMPv4 inbound traffic rules on the domain controller. Next, ensured that we are able to ping the domain controller from the client PC. Now that a connection has been established between both VMs, we are able to proceed with installing Active Directory on DC-1. 
</p>
<br />

<p>
<img width="960" alt="7 Admin account properties" src="https://github.com/DarianWells/Configure-Active-Directory/assets/132870202/d9d0e186-4f07-4750-84ab-b5a99dbd9a0a">
</p>
<p>
Installed Active Directory on DC-1. Once installed and a domain name has been created (I named the domain 'mydomain.com'), go to the 'Active Directory Users and Computers' and create two organizational units titles ' _EMPLOYEES' and '_ADMINS'. Created a new admin account by adding a new user under the '_ADMINS' folder (I just used my own name). Go to the account properties and make the user a member of the 'Domain Admins' security group. After that, log out of DC-1 and log back in using the new admin account (for example, the login I created was mydomain.com\d-wells).
</p>
<br />

<p>
<img width="960" alt="11 client-1 domain joined" src="https://github.com/DarianWells/Configure-Active-Directory/assets/132870202/f8f21406-2a7b-4028-b1e9-cbfd7ca0d585">
</p>

The next step was to join Client-1 to the domain. But before that, because Microsoft Azure VMs were used for this lab, the DNS server for Client-1 had to be changed to DC-1's private IP address. Once the DNS settings were changed, we are able to go into Client-1 and join it to the domain. Log into Client-1 as the admin user that was created on DC-1. While under the admin account, go to system properties and allow domain user access to remote desktop. Now all domain user accounts that are created will now be able to log into Client-1.

</p>
<br />

<p>
<img width="960" alt="12 creating new users using powershell script" src="https://github.com/DarianWells/Configure-Active-Directory/assets/132870202/a1506e2c-d233-4da6-a106-178fd0ac6afb">
</p>
<p>
Logged into DC-1 on the admin account and ran a script in Powershell ISE to create 1000 user accounts with a set password. Then, used the log in credentials of a few scripted user accounts to log into Client-1. 
</p>
<br />

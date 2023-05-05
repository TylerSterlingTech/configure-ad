<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

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
- Ensure Connectivity between the Client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory
- Join Client-1 to your the Domain Controller, Sterling.com
- Setup Remote Desktop for non-administrative users on Client-1
- Create 10,000 Additional Users and Log into Client-1 with a Generated User




<h2>Deployment and Configuration Steps</h2>


  
<h2>Setup Resources in Azure<h/2>
  
  
<p>
<img src="https://i.imgur.com/IXyyoKE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The first step is to create the domain controller virtual machine within Azure.
</p>
<br />

<p>
<img src="https://i.imgur.com/Qc5lsUT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The virtual machine is named DC-1, for domain controller 1. Windows Server 2022 is used. The resource group is automatically created, named DC-1_group 
</p>
<br />

<p>
<img src="https://i.imgur.com/OQL6jtT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The username and password are set for DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/imcku5L.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Similar to the resurce group, the virtual network is automatically created. "review + Create" is selected.
</p>
<br />

<p>
<img src="https://i.imgur.com/YnnqlGs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The DC-1 virtual machine has passed validation; "Create" is selected, creating the virtual machine.
</p>
<br />

<p>
<img src="https://i.imgur.com/w0P7TJ2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
DC-1's NIC private IP address is changed from dynamic to static.
</p>
<br />

<p>
<img src="https://i.imgur.com/41AxJJi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The Client-1 virtual machine is now being configured. The resource group is selected to be the same as the resource group for DC-1; Windows 10 is selected.
</p>
<br />

<p>
<img src="https://i.imgur.com/2tuVg24.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The Client-1 username and password are set.
</p>
<br />

<p>
<img src="https://i.imgur.com/JqG49nh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The same virtual network is selected for Client-1 as was for DC-1. "Review + Create" is selected.
</p>
<br />

  
<h2>Ensure Connectivity between the Client and Domain Controller<h/2>
  
  
<p>
<img src="https://i.imgur.com/MNlb2CK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To log in the Client-1, the Remote Desktop application an Client-1's public IP address are used.
</p>
<br />

<p>
<img src="https://i.imgur.com/W3RTjCD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The username and password set for Client-1 are used.
</p>
<br />

<p>
<img src="https://i.imgur.com/zIHKbFu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
A perpetual ping is attempted within Client-1, using the command prompt and DC-1's private IP address. It can be seen that there is not connectivity.
</p>
<br />

<p>
<img src="https://i.imgur.com/rqzpUja.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To enable connectivity, DC-1 must be accessed and ICMPv4 must be enabled.
</p>
<br />

<p>
<img src="https://i.imgur.com/FMfxF4Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To enable ICMPv4, Windows Defender Firewall with Advanced Security is utilized; "Inbound Rules" is selected in the near-top left corner.
</p>
<br />

<p>
<img src="https://i.imgur.com/hzCeBZr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The inbound rules are displayed.
</p>
<br />

<p>
<img src="https://i.imgur.com/nBH0QbE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The following two inbound rules are selected and enabled.
</p>
<br />

<p>
<img src="https://i.imgur.com/ZVsJ33v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Connectivity between Client-1 and DC-1 can now be witnessed within Client-1's command prompt. Control-C is utilized to discontinue the perpetual ping.
</p>
<br />

  
<h2>Install Active Directory<h/2>
    
    
<p>
<img src="https://i.imgur.com/RyYg4Uv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The server manager within DC-1 is displayed. "Add Roles and Feautures" is selected.
</p>
<br />

<p>
<img src="https://i.imgur.com/u2UgF3N.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Following the process of "Add Roles and Feautures", within "Server Roles", "Active Directory Domain Services" is selected before continuing.
</p>
<br />

<p>
<img src="https://i.imgur.com/z05AwLk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Active directory is being installed.
</p>
<br />

<p>
<img src="https://i.imgur.com/n28qlQg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Active directory has been installed, however, is still needs to be promoted to a domain controller. "Promote this server to a domain controller" is selected.
</p>
<br />

<p>
<img src="https://i.imgur.com/uFAhhEQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
"Add a new forest" is selected, and the root domain name is set to "sterling.com".
</p>
<br />

<p>
<img src="https://i.imgur.com/8AmsiZj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The password is set.
</p>
<br />

<p>
<img src="https://i.imgur.com/ZJwV2xn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The installation of the domain controller is configured.
</p>
<br />

<p>
<img src="https://i.imgur.com/v33cYAJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
DC-1 is restarted, and logged back into as the domaain controller log-in username and password.
</p>
<br />

  
<h2>Create an Admin and Normal User Account in Active Directory<h/2>
    
    
<p>
<img src="https://i.imgur.com/1wia3WR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
"Active Directory Users and Computers (ADUC), within DC-1, is displayed. The domain "sterling.com" can be seen.
</p>
<br />

<p>
<img src="https://i.imgur.com/CvJwLd8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To create an organizational unit, the process of "sterling.com --> new --> organizational unit" is followed. 
</p>
<br />

<p>
<img src="https://i.imgur.com/UPL1xt3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The organizational units of "_ADMINS" and "_EMPLOYEES" have been added.
</p>
<br />

<p>
<img src="https://i.imgur.com/1yiL8E0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To create a new employee, the process of "sterling.com --> _EMPLOYEES --> new --> user" is followed. 
</p>
<br />

<p>
<img src="https://i.imgur.com/GPWLbTP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The employee Jane Doe is configured, with the user logon name being set to "jane_admin".
</p>
<br />

<p>
<img src="https://i.imgur.com/C0i5U4v.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To add Jane to the "Domain Admins" security group, "Properties" is selected.
</p>
<br />

<p>
<img src="https://i.imgur.com/cgNGvTs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The "Domain Admins" group is selected for Jane.
</p>
<br />

<p>
<img src="https://i.imgur.com/rFZrfdF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Jane can now log in to the domain controller.
</p>
<br />
  
<h2>Join Client-1 to your the Domain Controller, sterling.com<h/2>

<p>
<img src="https://i.imgur.com/T9Ie3dw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Within the Azure portal, Client-1's DNS settings are set to DC-1's private IP address, 10.0.0.4.
</p>
<br />

<p>
<img src="https://i.imgur.com/ZYTnzj3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After the DNS configuration, Client-1 needs to be restarted.
</p>
<br />

<p>
<img src="https://i.imgur.com/YCQ6IYA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Within Client-1, Client-1 is being addedto the domain. The process of "System --> Rename this PC (advanced) --> Change" is followed. The domain is set to "sterling.com". Jane's admin account username and password are entered, and the virtual machine restarts.
</p>
<br />

<p>
<img src="https://i.imgur.com/6NPYcOM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Within ADUC in DC-1, it is verified that Client-1 has been successfully added to the domain, within the "Computers" folder.
</p>
<br />

<p>
<img src="https://i.imgur.com/Xztmr0M.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The "_CLIENTS" organizational unit is created, and Client-1 is moved into "_CLIENTS". 
</p>
<br />

<h2>Setup Remote Desktop for non-administrative users on Client-1<h/2>
  
<p>
<img src="https://i.imgur.com/fbqtGiu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After logging in to Client-1 as sterling.com\jane_admin, system properties is opened, "Remote Desktop" is selected, and "domain users" is given access to remote desktop. Client-1 can now be logged into with a non-administrative user.
</p>
<br />

<h2>Create 10,000 Additional Users and Log into Client-1 with a Generated User<h/2>
  
<p>
<img src="https://i.imgur.com/Q2q5vxD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After logging into DC-1 as Jane, PowerShell_ise is opened as an administrator.
</p>
<br />

<p>
<img src="https://i.imgur.com/KOKCvC3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
A new file is created, and the script is ran. The names being generated is displayed.
</p>
<br />

<p>
<img src="https://i.imgur.com/hKSA8J3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
The list of names are viewed in ADUC. 
</p>
<br />

<p>
<img src="https://i.imgur.com/g56PDzV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
A random username is selected from the list, and Client-1 is logged into with this username. 
</p>
<br />

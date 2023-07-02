# configure-ad
<p align="center">
<img src=https://imgur.com/JrJB2Yc.png" alt="Microsoft Azure logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>
For a Step by Step Demonstration, please watch the video.

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute]
<b>
- Step 1 (https://www.youtube.com/watch?v=54UxTzalEQ8)
<b/>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- Github

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Set up and Create Resources in Azure
- Step 2: Ensure Connectivity Between the Client and Domain Controller 
- Step 3: Install Active Directory 
- Step 4: Create an Admin/Normal User Account in AD
- Step 5: Join Client-1 in' your domain
- Step 6: Setup Remote Desktop for non-administrative users on Client -1
- Step 7: Create a Bunch of Additional Users and Attempt to Log Into Client-1 With One of the Users
- FINISH.

<h2>Deployment and Configuration Steps</h2>


<h2>Step 1: Set up and create resources in Azure </h2>

  - Create RG->Create VM (Windows Server 2022)-> Name DC1 
- Take note of the RG and Vnet that get created at this time
- Set DC NIC private IP to static-> Create the client VM (Windows 10) named - "Client11"-> Use RG and Vnet created before-> Ensure both VMS are in the same Vnet (check the topology with Network Watcher
</p>
<br />

<p>
<img src="https://imgur.com/ydcx5Lc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>


<p>
<h2>Step 2: Ensure Connectivity between the client and Domain Controller </h2>

  - Login to Client-1 with Remote Desktop and ping DC1 private IP address with ping-t <ip address>(perpetual ping)

- Login to the Domain Controller and enable ICMPv4 on the local windows Firewall

- Check back at Client-1 to see the ping succeed 


</p>
<br />
<p>
<img src="https://imgur.com/23t419z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  
</p>

<p>
<h2>Step 3: Install Active Directory Domain Services </h2>

  - Login to DC-1 and install Active Directory Domain Services

  - Promote as a DC: Setup a new forest as mydomain.com(remember)

  - Restart -> Log back into DC-1 as user


</p>
<br />

<p>
<img src="https://imgur.com/vcb6E8D.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<p>
<h2>Step 4: Create an Admin and Normal User Account in AD </h2>

  - In Active Directory Users and Computers (ADUC), create an Organizational United (Ou) called "_EMPLOYEES"
  - Create a new OU named "_ADMINS"
  - Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
  - Add jane_admin to the “Domain Admins” Security Group
  - Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
  - User jane_admin as your admin account from now on



</p>
<br />
<p>
<img src="https://imgur.com/jyhzPm2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<p>
<h2>Step 5: Join Client1 to Your Domain(mydomian.com) </h2>

  - From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
  - From the Azure Portal, restart Client-1
  - Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
  - Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
  - Create a new OU named “_CLIENTS” and drag Client-1 into there




</p>
<br />
<p>
<img src="https://i.imgur.com/npskx5n.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<h2>Step 6: Setup Remote Desktop for non-administrative users on Client-1 </h2>

  - Log into Client-1 as mydomain.com\jane_admin and open system properties
  - Click “Remote Desktop”
  - Allow “domain users” access to remote desktop
  - You can now log into Client-1 as a normal, non-administrative user now
  - Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)




</p>
<br />
<p>
<img src="https://imgur.com/750yoIv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<h2>Step 7: Create a bunch of additional users and attempt to log into client-1 with one of the users
 </h2>

  - Login to DC-1 as jane_admin
  - Open PowerShell_ise as an administrator
  - Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
  - Run the script and observe the accounts being created
  - When finished, open ADUC and observe the accounts in the appropriate OU
  - attempt to log into Client-1 with one of the accounts (take note of the password in the script)





</p>
<br />
<p>
<img src="https://imgur.com/IJBufgb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

FINISHED

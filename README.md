</p>

<h1>osTicket - Ticket Lifecycle: Intake Through Resolution</h1>
This walkthrough outlines the post-install configuration of the open-source help desk ticketing system osTicket.
In the last lab we installed all the prerequisites and installed as well as config everything for osTicket. Once again in case you took a break, open azure portal and recopy the ip address becuase it might’ve changed if you closed or shutdown the VM.
There will also be a video demonstration of this portion of the project in it's entirety in the YouTube link below in case of any hiccups along the process. For the short videos provided, you can simply click the video and it should open in a new tab for better guidance.
During Sev-A, Jane will not be able to see any newly created tickets until changes are made to her extended access. John will also have issues but his are being unable to close tickets. Both issues will be demonostrated on how to resolve in the videos provided.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (Microsoft Remote Access in the App Store for MAC users)
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Ticket Lifecycle Stages</h2>

- Intake
- Assignment and Communication
- Working the Issue
- Resolution

<h2>Lifecycle Stages</h2>

<p>
<img <img width="1439" alt="Azure services home" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/6318b253-ee4f-482e-bfec-33310016ae65">
</p>
<p>
Setup Resources in Azure
Create the Domain Controller VM (Windows Server 2022) named “DC-1”
Take note of the Resource Group and Virtual Network (Vnet) that get created at this time

<img width="1439" alt="Azure services home" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/1c0bff0c-960c-4f57-b844-35ef4bd31b41">
<img width="1439" alt="virtual machine" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/42322186-afc1-4ee5-9a31-d0eb68e90fca">
<img width="1439" alt="Create a virtual machine" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/d977aa36-0807-47a4-b26c-b6bdef886516">
<img width="1439" alt="Create a virtual machine 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/4dd602b4-3aa4-48e5-8e15-f2ab253c0397">
<img width="1439" alt="Create a virtual machine 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/da1dc744-d046-4594-b44e-7a7d3b96d92b">
<img width="1439" alt="Create a virtual machine 4" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/bb613c45-4427-4ce0-b16b-0d3da6dd28a8">

Set Domain Controller’s NIC Private IP address to be static
<img width="1439" alt="Create a virtual machine 5" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/98031ed2-d89b-4597-bfa8-af254caf1183">
<img width="1439" alt="Create a virtual machine 6" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/6c4e0327-1114-4444-9d0b-d53a29e53e24">

Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet that was created in Step 1.
Ensure that both VMs are in the same Vnet
<img width="1439" alt="Create a virtual machine 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/acbc6d7d-66ec-4ea9-9b9d-b33f88e097ab">
<img width="1439" alt="Create a virtual machine 7" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/a2035d74-b6b2-46a6-be5d-5c92bbf52c1c">

Ensure Connectivity between the client and Domain Controller
Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
Check back at Client-1 to see the ping succeed
<img width="1439" alt="Ensure connectivity" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/cfc6e9b3-8ba8-4b59-9cbd-b21558640df7">
<img width="1439" alt="Ensure connectivity 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/4b68df7f-b7ec-46a0-a901-39ea4b01bf7b">
<img width="1439" alt="Ensure connectivity 4" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/bc7dc252-3bdc-4cc2-a723-bd05d1867d30">
<img width="1439" alt="Ensure connectivity 5 1" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/76043cc7-8d4d-43c7-a476-54f9b4c964a2">
<img width="1439" alt="Ensure connectivity 6" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/7ace2cfd-3c47-49c0-92ab-ada98c04aee1">

Install Active Directory
Login to DC-1 and install Active Directory Domain Services
Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
Restart and then log back into DC-1 as user: mydomain.com\labuser
<img width="1439" alt="Install AD 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/1ae28470-b1c1-4bce-a550-5798d8d1d664">
<img width="1439" alt="Install AD 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/23393333-88aa-4576-8d21-d9de340aa8b2">
<img width="1439" alt="Install AD 5" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/93789432-58e2-4a3e-bde2-def2d1a9afe6">
<img width="1439" alt="Install AD 6" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/51f72203-7326-48da-a7d9-eca9c461e32d">
<img width="1439" alt="Install AD 7" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/4b5c4b3d-ff5b-411a-a5b4-4fc3dfb5f277">
<img width="1439" alt="Install AD 8" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/a313a416-ece6-430f-beb7-6fc38306a711">

Create an Admin and Normal User Account in AD
In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
Create a new OU named “_ADMINS”
Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
Add jane_admin to the “Domain Admins” Security Group
Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
User jane_admin as your admin account from now on


Join Client-1 to your domain (mydomain.com)
From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
From the Azure Portal, restart Client-1
Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
Create a new OU named “_CLIENTS” and drag Client-1 into there (Step is not really necessary, just for organizational purposes. I guess I skipped this in the lab!)


Setup Remote Desktop for non-administrative users on Client-1
Log into Client-1 as mydomain.com\jane_admin and open system properties
Click “Remote Desktop”
Allow “domain users” access to remote desktop
You can now log into Client-1 as a normal, non-administrative user now
Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)

Create a bunch of additional users and attempt to log into client-1 with one of the users
Login to DC-1 as jane_admin
Open PowerShell_ise as an administrator
Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
Run the script and observe the accounts being created
When finished, open ADUC and observe the accounts in the appropriate OU
attempt to log into Client-1 with one of the accounts (take note of the password in the script)

Finish.

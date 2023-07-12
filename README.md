</p>

<h1>Active Directory: Installation</h1>
This walkthrough outlines the install configuration of Microsoft Active Directory Domain Services. In short, we'll set up the enviroment in Azure, use a few commands inside of command land for familiarity, run powershell, and more. There will be more labs created later to help build intution with DNS and file permissions. For now we will focus on AD and the common uses of it. 
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (Microsoft Remote Access in the App Store for MAC users)
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022</b> (21H2)
- Windows 10</b> (21H2)

<h2>Setup Resources in Azure</h2>

- Create the Domain Controller VM (Windows Server 2022) named “DC-1”
- Take note of the Resource Group and Virtual Network (Vnet) that get created at this time

<img width="1439" alt="Azure services home" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/1c0bff0c-960c-4f57-b844-35ef4bd31b41">
<img width="1439" alt="virtual machine" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/42322186-afc1-4ee5-9a31-d0eb68e90fca">
<img width="1439" alt="Create a virtual machine" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/d977aa36-0807-47a4-b26c-b6bdef886516">
<img width="1439" alt="Create a virtual machine 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/4dd602b4-3aa4-48e5-8e15-f2ab253c0397">
<img width="1439" alt="Create a virtual machine 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/da1dc744-d046-4594-b44e-7a7d3b96d92b">
<img width="1439" alt="Create a virtual machine 4" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/bb613c45-4427-4ce0-b16b-0d3da6dd28a8">

<h2>Set Domain Controller’s NIC Private IP address to be static</h2>

<img width="1439" alt="Create a virtual machine 5" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/98031ed2-d89b-4597-bfa8-af254caf1183">
<img width="1439" alt="Create a virtual machine 6" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/6c4e0327-1114-4444-9d0b-d53a29e53e24">

<h2>Create the Client VM (Windows 10) named “Client-1”</h2>

- Use the same Resource Group and Vnet that was created in Step 1
- Ensure that both VMs are in the same Vnet

<img width="1439" alt="Create a virtual machine 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/acbc6d7d-66ec-4ea9-9b9d-b33f88e097ab">
<img width="1439" alt="Create a virtual machine 7" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/a2035d74-b6b2-46a6-be5d-5c92bbf52c1c">

<h2>Ensure Connectivity between the client and Domain Controller</h2>

- Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
- Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
- Check back at Client-1 to see the ping succeed

<img width="1439" alt="Ensure connectivity" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/cfc6e9b3-8ba8-4b59-9cbd-b21558640df7">
<img width="1439" alt="Ensure connectivity 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/4b68df7f-b7ec-46a0-a901-39ea4b01bf7b">
<img width="1439" alt="Ensure connectivity 4" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/bc7dc252-3bdc-4cc2-a723-bd05d1867d30">
<img width="1439" alt="Ensure connectivity 5 1" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/76043cc7-8d4d-43c7-a476-54f9b4c964a2">
<img width="1439" alt="Ensure connectivity 6" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/7ace2cfd-3c47-49c0-92ab-ada98c04aee1">

<h2>Install Active Directory</h2>

- Login to DC-1 and install Active Directory Domain Services
- Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
- Restart and then log back into DC-1 as user: mydomain.com\labuser

<img width="1439" alt="Install AD 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/1ae28470-b1c1-4bce-a550-5798d8d1d664">
<img width="1439" alt="Install AD 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/23393333-88aa-4576-8d21-d9de340aa8b2">
<img width="1439" alt="Install AD 5" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/93789432-58e2-4a3e-bde2-def2d1a9afe6">
<img width="1439" alt="Install AD 6" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/51f72203-7326-48da-a7d9-eca9c461e32d">
<img width="1439" alt="Install AD 7" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/4b5c4b3d-ff5b-411a-a5b4-4fc3dfb5f277">
<img width="1439" alt="Install AD 8" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/a313a416-ece6-430f-beb7-6fc38306a711">

<h2>Create an Admin and Normal User Account in AD</h2>

- In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
- Create a new OU named “_ADMINS”
- Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
- Add jane_admin to the “Domain Admins” Security Group
- Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
- User jane_admin as your admin account from now on

<img width="1439" alt="Post AD" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/c498709a-18e6-44a0-8003-7b2462354591">
<img width="1439" alt="Post AD 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/7f65002d-cc0a-4fe4-ae90-b5e9da5c69b3">
<img width="1439" alt="Post AD 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/3fbb3e5d-eba6-4fe2-b925-1f6c79614b65">
<img width="1439" alt="Post AD 4" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/73ae7040-c7ac-40c9-9347-5ac3bcef3d81">
<img width="1439" alt="Post AD 5" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/bfd9b567-9898-4354-bdaf-3d0398b2447f">
<img width="1439" alt="Post AD 6" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/c0c22811-8660-47a0-b820-8200ab3f62b9">
<img width="1439" alt="Post AD 7" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/513f6858-7370-4c7c-bfdc-948b4b876cbe">
<img width="1439" alt="Post AD 8" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/ab7970ab-4271-4b0a-a533-a7cbce62ae16">
<img width="1439" alt="Post AD 9" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/7adebc30-246f-4418-9692-138a688e85e4">
<img width="1439" alt="Post AD 10" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/4bbf5420-ec38-4fb8-937d-095e2ddc1a94">
<img width="1439" alt="Post AD 11" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/e71d2c3e-a908-4afd-af17-a2a40ac246cc">
<img width="1439" alt="Post AD 12" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/10ec3e48-ad03-46e7-acc9-69c191e3a325">

<h2>Join Client-1 to your domain (mydomain.com)</h2>

- From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
- From the Azure Portal, restart Client-1
- Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
- Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain

<img width="1439" alt="Join Domain 1" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/f6defb2f-e4b2-413b-acc8-cb037a6abb3c">
<img width="1439" alt="Join Domain 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/aeb1eb15-7a71-457d-962f-b1b077d5981d">
<img width="1439" alt="Join Domain 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/dbd5bb9f-e433-4d2b-ad4e-fa1e18c3333e">
<img width="1439" alt="Join Domain 4" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/02ba7a00-d380-45bb-873e-13a0dca96f22">
<img width="1439" alt="Join Domain 5" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/5a26baac-cc98-4d44-ba88-cd17209f5b7a">
<img width="1439" alt="Join Domain 6" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/27dbe6f2-7540-406d-bad1-ba46eae673fc">
<img width="1439" alt="Join Domain 7" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/7586ed32-d090-4e79-a41c-60fa8a5dfc58">
<img width="1439" alt="Join Domain 8" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/9e8b9d6d-390c-4998-9594-c139c1b7bdd2">

<h2>Setup Remote Desktop for non-administrative users on Client-1</h2>

- Log into Client-1 as mydomain.com\jane_admin and open system properties
- Click “Remote Desktop”
- Allow “domain users” access to remote desktop
- You can now log into Client-1 as a normal, non-administrative user now
- Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)

<img width="1439" alt="Allow Domain Users RDP" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/61de4141-9f48-4b24-b026-a9c69fb4bf0b">
<img width="1439" alt="Allow Domain Users RDP 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/31f63a30-e5f7-4e45-9526-f2803f83b034">
<img width="1439" alt="Allow Domain Users RDP 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/b5a7cfc5-a19a-4802-a59c-68280bb2d19b">
<img width="1439" alt="Allow Domain Users RDP 4" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/e262fc17-19ea-4e19-ac4a-4a41e5ddb402">
<img width="1439" alt="Allow Domain Users RDP 5" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/0f97a102-9775-475e-b660-b5f401dce277">

<h2>Create a bunch of additional users and attempt to log into client-1 with one of the users</h2>

- Login to DC-1 as jane_admin
- Open PowerShell_ise as an administrator
- Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
- Run the script and observe the accounts being created
- When finished, open ADUC and observe the accounts in the appropriate OU
attempt to log into Client-1 with one of the accounts (take note of the password in the script)

<img width="1439" alt="Create Additional Users" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/b7a7387a-b137-42cd-8021-27168d7f44a4">
<img width="1439" alt="Create Additional Users 2" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/f535dc42-d9ca-4d1e-ad45-d34d11326c0c">
<img width="1439" alt="Create Additional Users 3" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/7284c5dd-3ed6-429d-b72c-b6bfe075a4b6">
<img width="1439" alt="Create Additional Users 4" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/9e89b880-ffdc-4978-a101-9725c6047021">
<img width="1439" alt="Create Additional Users 5" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/d5cf9ec3-01c6-4013-84e9-ccb00ca35f6d">
<img width="1439" alt="Create Additional Users 6" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/86a51936-29e7-4117-97b1-e9029d21d54c">
<img width="1439" alt="Create Additional Users 7" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/01f84813-0b84-4672-905f-9895c7cfd6ac">
<img width="1439" alt="Create Additional Users 8" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/5111abcf-34ce-493d-b287-b74b24c90efc">
<img width="1439" alt="Create Additional Users 9" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/4eda7b02-e535-4799-be64-bc6bced900fb">

<h2>Make sure to clean up by deleting all resource groups to avoid ongoing costs</h2>

- Finish

<img width="1440" alt="Clean up" src="https://github.com/montrequonwheeler/active-directory-installation/assets/127397594/8ec9d160-b5c6-4b67-9091-93ac639d2cbf">


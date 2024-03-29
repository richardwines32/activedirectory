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

1) Setup Resources in Azure
2) Ensure Connectivity between the client and Domain Controller
3) Install Active Directory
4) Create an Admin and Normal User Account in AD
5) Join Client-1 to your domain (mydomain.com)
6) Setup Remote Desktop for non-administrative users on Client-1
7) Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>

1) Setup Resources in Azure: 
Create the Domain Controller VM (Windows Server 2022) named “DC-1”.
Take note of the Resource Group and Virtual Network (Vnet) that get created at this time.

<p>
<img width="1512" alt="Screenshot 2024-03-09 at 7 23 39 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/e46d3870-d75f-4288-8768-81d84db47418">
<img width="1512" alt="Screenshot 2024-03-09 at 7 25 48 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/5190f4a6-41e3-4cd2-9f11-495c81d1fd0a">

</p>
<p>


</p>
<br />
</p>
1A. Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group and Vnet.
<br />
<p>
</p>  
<img width="1512" alt="Screenshot 2024-03-09 at 7 31 53 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/17d03851-4f16-4c80-8b26-2c247fea884b">
<img width="1512" alt="Screenshot 2024-03-09 at 7 41 54 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/9fe9b92f-9ccc-479d-966b-12c1b7c185a8">

</p>
<p>

</p>
<br />

<p>
1B. Set Domain Controller’s NIC Private IP address to be static
<p>
<img width="1512" alt="Screenshot 2024-03-09 at 7 58 33 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/10741807-c4e1-427b-bc9e-3dae14c1f978">
</p>
<br />

<p>
2)Ensure Connectivity between the client and Domain Controller.  Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping).
</p>
<p>
Notice ping has timed out because DC-1's firewall is blocking it.
</p>
<p>
<img width="1512" alt="Screenshot 2024-03-09 at 8 24 50 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/e456a7c7-6b86-47db-91a9-da7c6082ec56">
</p>
<br />
<p>
2B. Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall.
<br />
</p>
<p>
 <img width="1512" alt="Screenshot 2024-03-09 at 8 35 59 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/dcf193d9-a6ac-495a-93e0-62226d907cdc">
 </p>

<br />
<p>
Notice the ping is now getting a response after configuring DC-1's firewall.
</p>
<p>
<img width="1512" alt="Screenshot 2024-03-09 at 8 36 11 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/7afbbdcb-9340-4ba4-bf70-ad26daac717a">
</p>

<p>
<br /> 
3. Install Active Directory.  Login to DC-1 and install Active Directory Domain Services.
</p>

<p>
<img width="1512" alt="Screenshot 2024-03-09 at 9 00 08 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/0de54554-c694-4c91-8da6-b56284c01846">
</p>
<p>
<br />  
3A.  Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
</p>


<p>
<img width="1512" alt="Screenshot 2024-03-09 at 9 00 08 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/3faf0c9f-78da-40ca-b655-00e44ae42eb3">
</p>
<p>
<br /> 
3B.  Restart and then log back into DC-1 as user: mydomain.com\labuser
</p>

<p>
<img width="1512" alt="Screenshot 2024-03-11 at 3 03 53 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/fbc843e7-24c8-40a9-8d4e-5434e9957f0a">
</p>
<p>
<br /> 
4.  Create an Admin and Normal User Account in AD.  In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”.
</p>


<p>
<img width="1512" alt="Screenshot 2024-03-11 at 3 25 57 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/160a9367-e5cb-4722-8c03-cca881f8067f">
</p>
<p>
<br /> 
4A.  Create a new OU named “_ADMINS”. 
</p>

<p>
<img width="1512" alt="Screenshot 2024-03-11 at 3 17 30 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/1e099d3d-5cd5-4312-b58a-f77e4387b4cf">
</p>
<p>
<br /> 
4B.  Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”.
</p>

<p>
<img width="1512" alt="Screenshot 2024-03-11 at 3 31 03 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/5128cb68-4ed1-4ca2-88a8-12ba6a3f6629">
</p>
<br />
<p>
4C.  Add jane_admin to the “Domain Admins” Security Group.
</p>


<p>
<img width="1512" alt="Screenshot 2024-03-11 at 3 37 39 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/b1ae6af1-2259-496a-bb87-938e8e52d033">
</p>
<br />
<p>
4D.  Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”.  Use jane_admin as your admin account from now on.
</p>

<p>
<img width="1512" alt="Screenshot 2024-03-11 at 3 47 16 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/a69a9724-896d-45e1-b719-02278d870e85">
</p>
<br />
<p>
5.  Join Client-1 to your domain (mydomain.com).  From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address.
</p>


<p>
<img width="1512" alt="Screenshot 2024-03-11 at 4 10 03 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/ec447b25-f01e-48e9-bf7b-3df3697770e7">
 </p>
 <br />
<p>
5A.  From the Azure Portal, restart Client-1.
</p>

<p>
<img width="1512" alt="Screenshot 2024-03-11 at 4 14 29 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/0ba597d4-e6f4-4b3c-9c53-7b20b9acb4e3">
</p>
<br />
<p>
5B.  Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart). 
</p>

<p>
<img width="1512" alt="Screenshot 2024-03-11 at 4 52 20 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/3f169bfd-813e-46a4-ae25-fc686ff95558">
</p>
<br />
<p>
6.  Setup Remote Desktop for non-administrative users on Client-1.  Log into Client-1 as mydomain.com\jane_admin and open system properties.  Click “Remote Desktop”.  Allow “domain users” access to remote desktop.  You can now log into Client-1 as a normal, non-administrative user now.  Normally you’d want to do this with Group Policy that allows you to change MANY systems at once.

<p>
<img width="1512" alt="Screenshot 2024-03-11 at 5 06 42 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/b5849186-e96d-402e-800d-ebf58a3f3c25">
</p>

<br />
<p>
7.  Create a bunch of additional users and attempt to log into client-1 with one of the users.  To do this login to DC-1 as jane_admin.  Open PowerShell_ise as an administrator.  Create a new File and use the script.

</p>
<p>
<img width="1512" alt="Screenshot 2024-03-11 at 5 22 23 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/972f4237-d836-48e8-997c-9ae9f4fad426">
</p>
<p>
<br /> 
7A.  Run the script and observe the accounts being created.
</p>
<p>
<img width="1512" alt="Screenshot 2024-03-11 at 5 30 29 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/d601d199-8f0f-4236-ae78-3afd19eb2a88">
</p>
<p>
<br /> 
7B.  When finished, open ADUC and observe the accounts in the appropriate OU. 
</p>

<p>
<img width="1512" alt="Screenshot 2024-03-11 at 5 33 41 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/ea1e2705-10dd-4994-83c1-fb49ffa67cc3">
</p>
<p>
<br /> 
7C.  Attempt to log into Client-1 with one of the accounts (take note of the password in the script).  Finish.
</p>
<p>
<img width="662" alt="Screenshot 2024-03-11 at 5 39 36 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/92cdb97d-f1bf-49ae-8c52-ec57a45c5b69">
</p>
<img width="1512" alt="Screenshot 2024-03-11 at 5 48 52 PM" src="https://github.com/richardwines32/activedirectory/assets/162821778/6d7489d2-dd56-47ef-bdaf-cd4344c1cc3c">



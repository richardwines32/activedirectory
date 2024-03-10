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
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

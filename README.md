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
- cmd/PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 11 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

1)	Sign up for free $200 credit on azure (requires credit card)
2)	Create windows server 2022 vm (DC-1/Domain controller)
3)	Create windows pro 11 vm (client-1) add virtual network from DC-1
4)	Connect DC-1 to remote desktop connection using public ip address, do the same for client-1 vm
5)	Ping DC-1 private ip address on Client-1 (notice it’s not returning data packets
6)	Configure network /firewall inbound rules on DC-1 to allow ICMP traffic.
7)	Change the DC-01 private ip address to static.
8)	Change Client-1 DNS to use DC-1 private ip (makes DC the go to guy to resolve DNS queries)
 	Two ways, either on azure by clicking the network interface and changing ip configurations or through the remote desktop connection and changing the ipv4 settings
9)	Install Active Directory Domain Services
10)	Add a forest. (mycompany.com)
11)	Create new admin user to use to sign into the client-1(mycompany.com\john_t)

CLIENT-1 SERVER:
- Log into client-1 using new admin (mycompany.com\john_t)
- Add client to DC-1 (domain controller) and restart the server.
- Enable remote desktop access for other domain users.
- Restart and sign in using the new domain admin user or new domain users created in Active directory.

DC-1 SERVER
- Add new ORGANIZATIONAL UNITS, add permissions
- Add new user that can log into client-1


<h2>Deployment and Configuration Steps</h2>

<p>
![azure-home](https://github.com/AndrewBugembe/configure-azure-ad/assets/129638683/282018ad-1985-43d6-aadb-3779b6d6de54)

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


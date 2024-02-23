<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure](https://www.youtube.com)

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
<img src="https://i.imgur.com/TaadLnt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create windows server 2022 vm (DC-1) that will be the Domain controller.
</p>
<br />

<p>
<img src="https://i.imgur.com/S0f2n9g.png"80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create windows pro 11 vm (client-1) add virtual network from DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/EuHqX0j.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
4)	Connect and access to both DC-1 and server vms using Remote desktop connection by way of their public ip addresses.
</p>
<br />

<p>
<img src="https://i.imgur.com/Pi1idDw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Ping DC-1 private ip address on Client-1 (notice it’s not returning data packets), that is because ICMP traffic is blocked on the DC-1 vm and the network security rules need to be configured to allow ICMP traffic and allow the server to be reacheable.
</p>
<br />

<p>
<img src="https://i.imgur.com/xW7OxhN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/nbyiimy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Configure network /firewall inbound rules on DC-1 to allow ICMP traffic; go to the azure interface of DC-1 vm, click networking tab and proceed to add inbound port rule where you can allow ICMP traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/B2iiZWv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/Lw4HQR6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Change the DC-01 private ip address to static. The static IP ensures that the DC’s network configuration remains stable and predictable. Dynamic IP addresses (assigned by DHCP) can change, leading to potential disruptions. DCs often serve as DNS servers within the AD domain. Clients and other servers rely on DNS to locate DCs for authentication and other services.
</p>
<br />

<p>
<img src="https://i.imgur.com/cRGSt3P.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Ping DC-1 private ip address again to confirm it can be reached.
</p>
<br />

<p>
<img src="https://i.imgur.com/SOJkKqz.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/6MdeFs1.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Change Client-1 DNS to use DC-1 private ip (makes DC the go to guy to resolve DNS queries)
- Two ways, either on azure by clicking the network interface and changing ip configurations or through the remote desktop connection and changing the ipv4 settings.
</p>
<br />

<p>
<img src="https://i.imgur.com/9CJi4F6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open server manager on DC-1, click 'Add roles and features' to install Active Directory Domain Services on DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/gPUq16U.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ccdOMnF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/iKZDcsH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Click role based installation, select server from sever pool, select 'Active directory domain services' from roles options, select 'Group Policy Management'.
</p>
<br />

<p>
<img src="https://i.imgur.com/XFP1CUm.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/eLYVqyq.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/PpomJyb.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/ncA9Oux.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After installation, open server manager and click Flag icon with caution sign in the right hand upper corner. There should be a statement 'Promote this server to a domain controller', click it and the add a new forest (mydomain.com). Once all the prerequisite checks pass, restart the server and login using your new domain name (mydomain\labuser)
</p>
<br />

<p>
<img src="https://i.imgur.com/Ghm9edM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/Wj5QuLB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/BBLtphY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/G9w2obj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After logging back into DC-1, create a new admin user to use to sign into the client-1(mycompany.com\john_t). The default built-in Administrator account has full access to the system hence creating a new admin user allows you to follow the principle of least privilege which enhances security.
</p>
<br />

<p>
<img src="https://i.imgur.com/CcdrWor.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/6wFAeIm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/RAmTquc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/K5qrPhR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/NzJNrVN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into client-1 using new admin user (mydomain.com\jose_r)), and Add client to DC-1 (domain controller:mydomain.com) and restart the server.
Log into DC-1 to check and confirm client-1 server was added to computers and the domain name
</p>
<br />

<p>
<img src="https://i.imgur.com/ulmTNZ4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/9rwXXEE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/YXeDcqq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into client server again (using admin user mydomain.com\jose_r) to enable remote desktop access for other domain users created on DC-1. This is mainly useful in an environment where people can share computers .
</p>
<br />

<p>
<img src="https://i.imgur.com/cKMrYxr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/v1G7dQW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/YBP6aZG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/gICkH2G.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/939xZBK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/2XTY2wI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/KxdiHL3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Add new ORGANIZATIONAL UNITS (e.g EMPLOYEES), add permissions , Add new user to the organizational unit , then change user group properties to belong to 'DomainUsers' so that user can log into client-1 and set a password that should be required to change on first login (to enhance security).
</p>
<br />



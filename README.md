<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)
- Notepad/Notes App (Needed for saving usernames and passwords)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/FY2B3Vq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
So for this section, login to both the client vm and DC vm with admin account: mydomain.com\jane_admin. Within the client vm attempt to ping a random name: "mainframe" and observe it to fail to ping. To do so from the start menu search for Windows Powershell, open the application. Once the application is opened type "ping mainframe" . This is to demontrate the understanding of DNS and how your computer goes about interacting with a hostname over a network. Three things your computer does when it is pinging a name or hostname is check Local DNS Cache. To see the local dns cache type "ipconfig /display dns".Then if it is not found it will check the Local Host File and then if nothing is found over there it check the DNS Server.  Now type "nslookup mainframe" and observe it fail. Now we are going to make mainframe pingable. To do so we will create a DNS A-record on DC for “mainframe” and have it point to DC's Private IP address(10.0.0.4). Go to dc vm and go to the start menu and search DNS and open appilcation. On the left panel click on dc-1. Expand the Foward Lookup Zones folder and within this folder hover over and right-click on mydomain.com and then clikc New Host (A or AAAA). Now fill in the following, Name: mainframe, IP Address: 10.0.0.4 and then click Add Host and then click Ok. Now go back to client vm and when you type ping mainframe, it will not fail and the IP Address will display. 

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

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (RDC/Windows App)
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- <a href="https://www.wireshark.org/">Wireshark</a> (Protocol Analyzer)
- Notepad/Notes App (Needed for saving usernames and passwords)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>List of Prerequisites</h2>

- Basic/General Understanding of Microsoft Azure
- Azure Subscription/Azure Account(Portal) created
- Resource Group created within your Azure portal
- Windows 10 Virtual Machine(Windows) created within your Azure portal with the resource group you've created previously
- Linux Virtual Machine(Ubuntu) created within your Azure portal within the resource group <strong>*When creating the linux VM(Ubuntu),under the Networking tab,  make sure to select the same Virtual Network as the one you used for the Windows VM(windows-vm-vnet). If it doesn't appear as an option to be selected, refresh page*</strong>

<h2>Actions and Observations</h2>
<p>
<img src="https://i.imgur.com/y9bwKCU.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Logon to windows vm. Install <a href="https://www.wireshark.org/">Wireshark</a> within windows vm by copy and pasting the url into the windows vm. After installation, open up wireshark. After that click/highlight Ethernet and then on the top left corner of the application, click on the blue shark fin icon to start packet capturing on wireshark. Afterwards, on the search bar filter for only icmp. As expected nothing is shown. After that login to the linux vm, 
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


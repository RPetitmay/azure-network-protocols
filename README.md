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
  <h3>Observe ICMP Traffic</h3>
<ol>
  <li>Log in to the Windows virtual machine (VM).</li>
  <li>
    Open a web browser within the VM and navigate to the following URL to download Wireshark:
    <a href="https://www.wireshark.org/">https://www.wireshark.org/</a>
  </li>
  <li>Download and install Wireshark by following the on-screen instructions.</li>
  <li>Once installed, launch Wireshark.</li>
  <li>In the main interface, locate and select the <strong>Ethernet</strong> interface.</li>
  <li>Click the <strong>blue shark fin icon</strong> in the top-left corner to start packet capture on the selected interface.</li>
  <li>In the display filter bar, type <code>icmp</code> and press <strong>Enter</strong> to filter for ICMP packets.</li>
  <li>Navigate to the <strong>Azure portal</strong>, go to the <strong>Overview</strong> section of your Linux VM, and copy the <strong>private IP address</strong>.</li>
  <li>Return to the Windows VM and open <strong>PowerShell</strong>.</li>
  <li>
    In PowerShell, ping the private IP address of the Linux VM using the following command:
    <br><code>ping &lt;linux-vm-private-ip&gt;</code>
  </li>
  <li>Switch back to Wireshark and observe the capture for ICMP packets corresponding to the ping requests and replies.</li>
  <li>
    Additionally, ping a public website (e.g., www.google.com) from PowerShell using the command:
    <br><code>ping www.google.com</code>
  </li>
  <li>Continue monitoring ICMP packet activity in Wireshark for both internal and external ping attempts.</li>
</ol>
</p>
<br />

<p>
<img src="https://i.imgur.com/vhOaoMk.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <h3>Configuring a Firewall Network Security Group</h3>
<ol>
  <li>Open <strong>PowerShell</strong> on your Windows VM if it is not already open.</li>
  <li>
    Execute a continuous ping to the Linux VM's private IP address by entering the following command:
    <br><code>ping &lt;linux-vm-private-ip&gt; -t</code>
  </li>
  <li>In the <strong>Azure portal</strong>, navigate to the <strong>Virtual Machines</strong> section and select your <strong>Linux VM</strong>.</li>
  <li>Click on the <strong>Networking</strong> tab, then select <strong>Network settings</strong>.</li>
  <li>Locate the <strong>Network Security Group (NSG)</strong> associated with the Linux VM (e.g., <em>linux-vm-nsg</em>) and click on it.</li>
  <li>Within the NSG settings, click on the <strong>Inbound security rules</strong> tab, then click <strong>Add</strong> to create a new rule.</li>
  <li>
    Configure the new inbound rule with the following values:
    <ol>
      <li><strong>Source</strong>: Any</li>
      <li><strong>Source port ranges</strong>: *</li>
      <li><strong>Destination</strong>: Any</li>
      <li><strong>Service</strong>: Custom</li>
      <li><strong>Destination port ranges</strong>: *</li>
      <li><strong>Protocol</strong>: ICMPv4</li>
      <li><strong>Action</strong>: Deny</li>
      <li><strong>Priority</strong>: 290</li>
    </ol>
  </li>
  <li>Click <strong>Add</strong> to apply the rule.</li>
  <li>Return to <strong>PowerShell</strong> on the Windows VM and observe that the ping requests now time out, indicating that ICMP traffic is being blocked.</li>
  <li>Go back to the <strong>Azure portal</strong>, navigate to the NSG's <strong>Inbound security rules</strong>, and delete the rule you just created.</li>
  <li>After the rule has been removed, return to <strong>PowerShell</strong> and observe that ICMP traffic has resumed and ping replies are being received.</li>
  <li>Press <strong>Ctrl + C</strong> in PowerShell to stop the continuous ping and end the Wireshark capture.</li>
</ol>
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




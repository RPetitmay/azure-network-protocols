<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (RDC/Windows App)
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
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
<img src="https://i.imgur.com/z5xTf4i.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h3>Capturing SSH Traffic from Windows VM to Linux VM using Wireshark</h3>
  <ol>
  <li>Log back into the <strong>Windows VM</strong> if you are not already signed in.</li>
  <li>Open the <strong>Wireshark</strong> application by searching for it from the <strong>Start Menu</strong>.</li>
  <li>Select the <strong>Ethernet</strong> interface by clicking or highlighting it, then start a packet capture by clicking the <strong>blue shark fin icon</strong> in the upper-left corner.</li>
  <li>In the display filter bar, type <code>ssh</code> and press <strong>Enter</strong> to filter for SSH traffic.</li>
  <li>Open <strong>PowerShell</strong> within the Windows VM.</li>
  <li>Locate the <strong>private IP address</strong> of your Linux VM by navigating to its <strong>Overview</strong> page in the <strong>Azure portal</strong>.</li>
  <li>
    In PowerShell, initiate an SSH connection by entering the following command:
    <br><code>ssh &lt;vm-username&gt;@&lt;private-ip-address&gt;</code>
    <br>Replace <code>&lt;vm-username&gt;</code> with your Linux VM's username and <code>&lt;private-ip-address&gt;</code> with the actual private IP.
  </li>
  <li>When prompted to continue connecting, type <code>yes</code> and press <strong>Enter</strong>.</li>
  <li>If you are not immediately prompted to enter a password, repeat the SSH command.</li>
  <li>When entering your password, note that no characters will appear—this is normal. After typing the password, press <strong>Enter</strong>.</li>
  <li>Once connected, you will have terminal access to the Linux VM from within the Windows VM.</li>
  <li>To verify the connection, type <code>id</code> to display the current user.</li>
  <li>Type <code>hostname</code> to display the Linux VM’s hostname.</li>
  <li>Optionally, type random characters or run commands to observe SSH traffic in Wireshark.</li>
  <li>When finished, type <code>exit</code> in PowerShell to terminate the SSH session.</li>
</ol>
</p>
<br />

<p>
<img src="https://i.imgur.com/YZPqtfG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <h3>Capturing DHCP Traffic on a Windows VM Using Wireshark and a Batch Script</h3>
<ol>
  <li>Log back into the <strong>Windows VM</strong>.</li>
  <li>Open <strong>Wireshark</strong> by searching for it in the <strong>Start Menu</strong>, then right-click and select <strong>Run as administrator</strong>.</li>
  <li>Start a packet capture by selecting the <strong>Ethernet</strong> interface and clicking the <strong>blue shark fin icon</strong>.</li>
  <li>In the Wireshark display filter bar, type <code>dhcp</code> and press <strong>Enter</strong> to filter the capture for DHCP traffic.</li>
  <li>Open the <strong>Notepad</strong> application by searching for it in the <strong>Start Menu</strong>.</li>
  <li>In Notepad, type the following two commands, each on a separate line:
    <ol>
      <li><code>ipconfig /release</code></li>
      <li><code>ipconfig /renew</code></li>
    </ol>
  </li>
  <li>Save the file as a batch script:
    <ol>
      <li>Click <strong>File</strong> &gt; <strong>Save As</strong>.</li>
      <li>In the <strong>File name</strong> field, enter a name ending in <code>.bat</code> (e.g., <code>dhcp.bat</code>).</li>
      <li>In the <strong>Save as type</strong> dropdown, select <strong>All Files</strong>.</li>
      <li>In the File Explorer address bar, enter <code>c:\ProgramData</code> to navigate to the ProgramData directory.</li>
      <li>Click <strong>Save</strong>.</li>
    </ol>
  </li>
  <li>Open <strong>PowerShell as Administrator</strong>.</li>
  <li>Navigate to the ProgramData folder by typing:
    <br><code>cd c:\ProgramData</code>
  </li>
  <li>Type <code>ls</code> and press <strong>Enter</strong> to verify the batch file is in the folder.</li>
  <li>Run the batch file by typing:
    <br><code>.\&lt;filename&gt;.bat</code>
    <br>Replace <code>&lt;filename&gt;</code> with the name of your file (e.g., <code>.\dhcp.bat</code>).
  </li>
  <li>Wait for the commands to complete. This may disconnect and reconnect your network and possibly sign you out of the VM.</li>
  <li>After signing back in, return to <strong>Wireshark</strong> and observe the captured <strong>DHCP traffic</strong> in the filtered view.</li>
</ol>
</p>
<br />

<p>
<img src="https://i.imgur.com/yubXcUi.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <h3>Capturing DNS Traffic Using Wireshark on a Windows VM</h3>
  <ol>
  <li>Log in to the <strong>Windows virtual machine (VM)</strong>.</li>
  <li>Open the <strong>Wireshark</strong> application by searching for it in the <strong>Start Menu</strong>.</li>
  <li>Begin a packet capture by selecting the <strong>Ethernet</strong> interface and clicking the <strong>blue shark fin icon</strong> in the upper-left corner.</li>
  <li>In the Wireshark display filter bar, type <code>dns</code> and press <strong>Enter</strong> to filter the capture for DNS traffic.</li>
  <li>Open <strong>PowerShell</strong> as an administrator.</li>
  <li>In the PowerShell window, type the following command and press <strong>Enter</strong>:
    <br><code>nslookup disney.com</code>
  </li>
  <li>After executing the command, observe that DNS query and response packets appear in Wireshark for <code>disney.com</code>.</li>
  <li>PowerShell will display the IP address associated with <code>disney.com</code>.</li>
</ol>
</p>
<br />

<p>
<img src="https://i.imgur.com/OzvWH9a.jpeg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <h3>Monitoring RDP Traffic Using Wireshark on a Windows VM</h3>
<ol>
  <li>Log in to the <strong>Windows virtual machine (VM)</strong>.</li>
  <li>Search for <strong>Wireshark</strong> in the <strong>Start Menu</strong> and open the application.</li>
  <li>Select the <strong>Ethernet</strong> interface by clicking or highlighting it, then start a packet capture by clicking the <strong>blue shark fin icon</strong> in the upper-left corner.</li>
  <li>In the Wireshark display filter bar, type <code>tcp.port == 3389</code> and press <strong>Enter</strong>.</li>
  <li>This filter displays traffic associated with the <strong>Remote Desktop Protocol (RDP)</strong>, which uses TCP port 3389.</li>
  <li>Observe the captured packets. You should see a continuous stream of RDP traffic, indicating an active or idle remote desktop session.</li>
</ol>
</p>
<br />




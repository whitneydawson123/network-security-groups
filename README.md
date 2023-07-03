<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Internet Control Messaging Protocol (ICMP) Traffic
- Secure Shell Protocol (SSH) Traffic
- Dynamic Host Configuration Protocol (DHCP) Traffic
- Domain Name System (DNS) Traffic
- Remote Desktop Protocol (RDP) Traffic

<h2>Actions and Observations</h2>

<p>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/692d02be-ee5c-4443-82cd-3b08482d36c9" height="80%" width="80%" alt="Step 1"/>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/1f339170-2020-4243-854a-1e0f804bbac2" height="80%" width="80%" alt="Step 2"/>
</p>
<p>
You are going to create a Resource Group in Azure. I named mine RG-Lab-1 and then you're going to create 2 virtual machines. One of them will be Windows 10 and the other is going to be Ubuntu Linux. 
</p>
<br />

<p>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/996fef7e-c828-4bf0-9374-9140f386351e" height="80%" width="80%" alt="Step 3"/>
</p>
<p>
Next, you're going to open the remote desktop, paste the public IP address of the Windows 10 VM into it, and enter your username and password. Then you're going to open Microsoft Edge and download and install Wireshark.
</p>
<br />

<p>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/59d09ffa-a95c-4a2a-a3d9-54b49319ee13" height="80%" width="80%" alt="Step 4"/>
</p>
<p>
Open Wireshark, press on the bluefin at the top right and search for ICMP traffic. This traffic will display the relay request and delivery, also known as ping. Open you Command Prompt (CMD) and enter ping and the private IP address of the Linux VM. Mine was 10.0.0.5. Then enter ping 10.0.0.5 -t. This command will keep pinging the server forever but we are going to block it with the firewall in the next step.
</p>
<br />

<p>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/06871109-dbda-479f-af8b-4d7735e331d3" height="80%" width="80%" alt="Step 5"/>
</p>
<p>
Go to your Azure portal, type in Network Security groups, and press the one that correlates to your Linux VM. For me that is VM-2. Go to Inbound Security Rules and block all ICMP traffic.
</p>
<br />

<p>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/b21e1aa9-ce89-43ae-8b64-889acdb34df8" height="80%" width="80%" alt="Step 6"/>
</p>
<p>
Go back to your Windows VM and you should start seeing a "request timed out" response.
</p>
<br />

<p>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/b1239641-73da-42c1-9c06-5e496dc3e48f" height="80%" width="80%" alt="Step 7"/>
</p>
<p>
Now, we are going to observe SSH traffic. Type SSH in the search bar of Wireshark. In the Command Line, we are going to ssh into the Ubuntu VM. In my case, I entered ssh labuser@10.0.0.5, pressed enter, yes, and entered my password. You can now see traffic populating in Wireshark.
</p>
<br />

<p>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/5fcc9fa5-f88a-4bc7-8a3b-3d7740e8605a" height="80%" width="80%" alt="Step 8"/>
</p>
<p>
Now, we are observing DHCP traffic. Type dhcp into Wireshark, open the command line, and type ipconfig /renew. You should see traffic populating in Wireshark.
</p>
<br />

<p>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/0743f185-a7d2-441b-bf64-07102837c2a5" height="80%" width="80%" alt="Step 9"/>
</p>
<p>
Now we are going to observe DNS traffic. Type dns in Wireshark, and use the command "nslookup www.google.com" in the command line. You should see traffic populating in Wireshark.
</p>
<br />

<p>
<img src="https://github.com/whitneydawson123/network-security-groups/assets/94804621/329b4821-94a1-43bb-989b-d381cfe362fa" height="80%" width="80%" alt="Step 10"/>
</p>
<p>
Now we are going to observe RDP traffic. Instead of typing in rdp in Wireshark, we are going to write tcp.port == 3389 in Wireshark. You should see traffic constantly flowing, showing a live stream of packets. This is because both VMs are connected via RDP and any interaction will be recorded. <br/>

We've reached the end of this project. Thank you for reading!
</p>
<br />

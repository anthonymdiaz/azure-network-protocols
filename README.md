<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Enhancing Network Security: Examining Traffic Between Azure Virtual Machines with NSGs</h1>
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

- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
- Observe ping requests and replies within WireShark

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
1. Create our Resources


  a. Create a Resource Group Within Azure
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
2. Create a Windows 10 Virtual Machine (VM) within Azure


  a. While creating the VM, select the previously created Resource Group
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. Create a Linux (Ubuntu) VM


  a. While create the VM, select the previously created Resource Group and Vnet 
</p>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
4. Observe ICMP Traffic

  
  a. Use Remote Desktop to connect to your Windows 10 Virtual Machine
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
5. Within your Windows 10 Virtual Machine, Install Wireshark
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
6. Open Wireshark and filter for ICMP traffic only
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
7. Observe ping requests and replies within WireShark by retrieving the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM </p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
8. From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9. Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM

  
  a. Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
10. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
11. Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
12. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)


  a. Stop the ping activity
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
13. Observe SSH Traffic

  
  a. Back in Wireshark, filter for SSH traffic only
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
14. From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
15. Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
16. Exit the SSH connection by typing ‘exit’ and pressing [Enter]
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
17. Observe DHCP Traffic

  
  
  a. Back in Wireshark, filter for DHCP traffic only
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
18. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)

  
  
  a. Observe the DHCP traffic appearing in WireShark
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
19. Observe DNS Traffic

  
  a. Back in Wireshark, filter for DNS traffic only
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
20 . From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are

  
  a. Observe the DNS traffic being show in WireShark
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
21. Observe RDP Traffic

  
  a. Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Observe the immediate non-stop spam of traffic. Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?

  
  - Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted
</p>
<br />

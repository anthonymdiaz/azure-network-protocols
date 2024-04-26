<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Enhancing Network Security: Examining Traffic Between Azure Virtual Machines with NSGs</h1>
In this tutorial / demonstration, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


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

1. Provisioning Virtual Machines

Deploying Virtual Machines in Azure: Windows 10 and Ubuntu Server

Set up two virtual machines on Azure—one running Windows 10 and the other Ubuntu Server. Customize names as per your preference, and for the Ubuntu Server, ensure to disable SSH and enable password authentication to create a username and password.

![Creating Virtual Machine Windows 10](https://i.imgur.com/TC2WeYr.jpg)

VM-2 Ubuntu Server

![Creating Virtual Machine Ubuntu Server](https://i.imgur.com/z8L3NWy.jpg)

2. Installing and Running Wireshark

Proceed to install Wireshark (Windows Installer 64-bit) on the Windows 10 virtual machine. Follow the default installation steps. During installation, Npcap will prompt for installation; proceed with default settings. After Npcap installation, Wireshark installation will resume automatically. Once installed, launch Wireshark on the VM. Click on 'Ethernet' and then select the blue fin icon located under 'File' to initiate packet capture. Observe the ongoing background traffic.

![Wireshark capturing packets](https://i.imgur.com/hRYo3PE.jpg)

3. Exploring Various Protocols


ICMP (Internet Control Messaging Protocol)

Launch Wireshark and filter for ICMP traffic by typing 'icmp' (no results initially). Navigate to the Azure Portal to locate the private IP address of the Ubuntu Server VM. Return to the Windows 10 VM, open Windows PowerShell, and execute the ping command with the obtained private IP address of the Ubuntu Server VM. Observe the traffic in Wireshark, noting the requests and replies. In PowerShell, monitor the sent packets and their success or loss.

![Ubuntu Server VM's Private IP Address](https://i.imgur.com/YxeS3EG.jpg)

Pinging Ubuntu Server VM's Private IP Address from Windows 10 VM using PowerShell

Execute the ping command in Windows PowerShell on the Windows 10 VM, substituting the private IP address of the Ubuntu Server VM. Monitor the output to observe the number of packets sent, received, and any loss.

![Pinging Ubuntu Server VM's Private IP Address from Windows 10 VM](https://i.imgur.com/WaTEtVt.jpg)

4. Restricting ICMP Traffic in Ubuntu's Network Security Group

a. On the Windows 10 VM, launch PowerShell and initiate a continuous ping by entering the command: ping (Private IP address of Ubuntu Server VM) -t.


b. In the Azure Portal, navigate to the Network Security Group associated with the Ubuntu Server VM. Click on the VM and then select "Inbound security rules."


c. Click "Add" to create a new rule. Choose ICMP from the list of protocols and ensure it is selected. Set the Action to Deny. Assign a priority before 300 to ensure precedence over other rules.


d. Return to PowerShell on the Windows 10 VM and observe the output indicating "Request timed out". In Wireshark, note the presence of only ping requests.


e. After observing the timeout, delete the rule to allow ping requests to resume.

![Pinging Ubuntu Server VM's Private IP Address from Windows 10 VM non-stop](https://i.imgur.com/likADaX.jpg)

Creating Rule to Deny ICMP in Ubuntu's Network Security Group (NSG)

![NSG Inbound Rule to deny ICMP](https://i.imgur.com/lfxfsvu.jpg)

Observing Ping Request Timeouts

![Ping request timing out because of new rule](https://i.imgur.com/46cwHyk.jpg)

5. Accessing SSH (Secure Shell) Port 22

a. Modify the Wireshark filter to display SSH traffic by entering "SSH" or "tcp.port == 22".


b. In PowerShell on Windows 10 VM, initiate an SSH connection to the Ubuntu VM by typing: ssh (Username of Ubuntu VM)@(Private IP address of Ubuntu VM). Follow the prompts, including typing 'yes' to confirm the connection and entering the password (note that characters typed for the password will not be visible).


c. Upon successful authentication, access the command prompt of the Ubuntu VM. Utilize Linux commands as desired.


d. To exit the SSH session and return to the command prompt of VM-1 (Windows 10), type 'exit' in the SSH session.


e. Close the SSH connection.


SSH Protocol

![SSH Protocol](https://i.imgur.com/OsrUIjq.jpg)

Using Linux Commands

![SSH Protocol with some Linux commands](https://i.imgur.com/VGwpgXv.jpg)

6. Monitoring DHCP Traffic

a. Open Wireshark and filter for DHCP traffic by typing "DHCP" into the filter field.


b. Note that initially, no DHCP traffic is displayed.


c. In PowerShell on the Windows 10 VM, initiate the command ipconfig /renew.


d. Observe Wireshark as DHCP traffic is generated in response to the IP address renewal request.


e. Renewing IP address in PowerShell to observe DHCP traffic

![Renewing IP address](https://i.imgur.com/5AMAZDf.jpg)

7. Monitoring DNS Traffic on UDP Port 53

a. Set the Wireshark filter to display DNS traffic and refresh the capture to clear any existing traffic.


b. In PowerShell on the Windows 10 VM, use the nslookup command to query the IP address of www.google.com.


c. Execute the command: nslookup www.google.com.


d. Observe the DNS traffic in Wireshark as the nslookup command resolves the IP address of www.google.com.


e. Utilizing nslookup to determine the IP address of www.google.com

![nslookup www.google.com to get IP address for google](https://i.imgur.com/OL4TPR7.jpg)

## Finished

To sum up, we've learned about different network protocols by using two virtual machines and Wireshark. We also saw how to block ICMP traffic between them using Network Security Group rules. Now that everything is set, you can continue exploring more traffic and experimenting with rules to better understand how it all functions.

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

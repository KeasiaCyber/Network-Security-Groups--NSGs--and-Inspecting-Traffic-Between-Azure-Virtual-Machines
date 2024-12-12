# Network-Security-Groups--NSGs--and-Inspecting-Traffic-Between-Azure-Virtual-Machines
<p align="center">
<img src="https://imgur.com/nd1IDzZ.png" alt="open"/>
</p>

In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Installation Steps</h2>


<p>
</p>
<p>
To explore Network Security Groups and network protocols, create two Azure VMs: one Linux and one Windows 10, each with two CPUs on the same VNET. On the Windows VM, download and install Wireshark. Open Wireshark, filter for ICMP traffic, and use the ping command to test connectivity to the Linux VM's private IP. You’ll see ICMP packets in Wireshark, which show network connectivity messages. 
<p>
We can inspect each individual packet and see the actual data that is being sent in each ping. the picture below demonstrates just that. 
</p>
<br />
<p>
In the next part of the lab, you will continuously ping the Linux machine from the Windows machine using the ping -t command. This sends ongoing ping requests until manually stopped. While the ping is running, switch to the Linux machine and block inbound ICMP traffic using its firewall. This will stop the echo replies from the Linux machine.
To block ICMP, create a new Network Security Group (NSG) on the Linux machine and configure it to block ICMP traffic. You can later re-allow the traffic by enabling ICMP in the NSG settings on the Azure portal.
  
<img src="https://imgur.com/Ee5ghJ8.png" height="80%" width="80%" alt="Two steps in one"/>
<img src="https://imgur.com/cL053oG.png" height="80%" width="80%" alt="Two steps in one"/>
</p>
<p>
Next, we'll use the Windows machine to SSH into the Linux machine. SSH provides command-line access to the remote system without a graphical interface. Set Wireshark to filter for SSH packets. When you run the command ssh labuser@10.0.0.5 in the Windows Command Prompt, Wireshark will immediately start capturing SSH packet activity.
</p>
<br />
<img src="https://imgur.com/kVmxJI8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now, we'll use Wireshark to filter for DHCP traffic. DHCP (Dynamic Host Configuration Protocol) operates on ports 67 and 68 to assign IP addresses to devices. On the Windows machine, run the command ipconfig /renew to request a new IP address. When you execute the command, Wireshark will capture and display the DHCP traffic.
</p>
<br />
<img src="https://imgur.com/TN8D64l.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we’ll filter for DNS traffic in Wireshark. DNS (Domain Name System) resolves domain names to IP addresses. To generate DNS traffic, use the command nslookup www.google.com. This command queries the DNS server to find the IP address for Google's domain, and Wireshark will capture the corresponding DNS packets.
</p>
<br />
<img src="https://imgur.com/KMQLkoy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Finally, we'll filter for RDP traffic in Wireshark. Use the filter tcp.port==3389 to capture Remote Desktop Protocol packets. Since RDP is actively used to connect to the virtual machine, you'll see a continuous stream of traffic in Wireshark.
</p>
<br />
<img src="https://imgur.com/EpSmEMv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

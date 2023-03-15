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

- Step 1: A-Record Exercise
- Step 2: Local DNS Cache Exercise 
- Step 3: CNAME Record Exercise


<h3>A-Record Exercise
</h3>

<p>
<img src="https://i.imgur.com/RP8k4ca.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/tCGYY7O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/rMZdUNE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
Connect/log into Client-1 as an admin (mydomain\jane_admin)
From Client-1 try to ping “mainframe” notice that it fails
Nslookup “mainframe” notice that it fails (no DNS record)
Create a DNS A-record on DC-1 for “mainframe” and have it point to DC-1’s Private IP address
Go back to Client-1 and try to ping it. Observe that it works

</p>
<br />

<h3> Local DNS Cache Exercise </h3>

<p>
<img src="https://i.imgur.com/sROPPR2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/zbTPFA1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/XxvVf7x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to DC-1 and change mainframe’s record address to 8.8.8.8
Go back to Client-1 and ping “mainframe” again. Observe that it still pings the old address
Observe the local dns cache (ipconfig /displaydns)
Flush the DNS cache (ipconfig /flushdns). Observe that the cache is empty
Attempt to ping “mainframe” again. Observe the address of the new record is showing up

</p>
<br />

<h3> CNAME Record Exercise </h3> 
<p>
<img src="https://i.imgur.com/oEIfOoY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to DC-1 and create a CNAME record that points the host “search” to “www.google.com”
Go back to Client-1 and attempt to ping “search”, observe the results of the CNAME record
On Client-1, nslookup “search”, observe the results of the CNAME record

</p>
<br />

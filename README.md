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

- Creating Environments
- Installing WireShark
- Viewing Traffic
- Experimenting with Azure Network Security Groups

<h2>Actions and Observations</h2>

### Creating the Environments

In order to begin, two Azure virtual machines needed to be created. One is a Windows 10 machine, which will be the one that will be mainly used. The other machine will be an Ubuntu machine that will be pinged to during the lab. Both of these will need to be placed in the same resource group for the process to work smoothly. Ideally, the Windows 10 machine will be made with enough processors to allow for smooth operation. They will both need to be within the same network and server locaiton. 
</p>
<br />

### Installing WireShark

Once both machines have been created and are ready for use, connect remotely into the windows machine. After logging in and setting it up, WireShark needs to be downloaded and installed. Once installed, it needs to be opened.
</p>
<br />

### Observing Traffic
With WireShark ready to be used, traffic to and from the Windows 10 virtual machine can be viewed and filtered for the various types of connection types. The first type of traffic to be observed is ICMP, which can be viewed when pinging the ubuntu VM. Pinging is done via the command prompt or PowerShell with the ping command, directing it to the IP of your desired computer. Other types of traffic that can be filtered and observed include:

- SSH
  This traffic requires that the other machine be connected into from Secure Shell. This requires a user to "log in" but without the user interface. Once the credentials are entered, SSH traffic can be observed when linux commands are used in the connection. Even so much as typing sends visible traffic. Some of the commands that can be used are "$id," "uname -a," and so on.
- DHCP
  This type of traffic is visible when a new IP address is assigned to your current VM using the "ipconfig /renew" command.
- DNS
  This type of traffic is visible when "dnslookup" is used to see what the IP address of a website is.
- RDP
  This type of traffic is constantly visible coming in through WireShark. This traffic documents quite literally everything that happens on the computer, from mouse movement to typing. This channel serves as a live stream of a computer, which will include all activity on that computer.
  
</p>
<br />

### Editing the Network Security Group

The different types of protocol traffic can be manually blocked in the security settings for a VM. The ubuntu machine will be used in this example. Before changing anything, note that ICMP traffic (a simple ping) can be sent with a reply. With this in mind, the Network Security Group of the Ubuntu VM is to be opened. There are already some rules present, but a new rule will be created. While creating this rule, ICMP specifically can be denied which is what will be done for this example. The priority of the rule must also be set first for this to be visible.
Once this rule is created, notice that any attempt to ping the Ubuntu VM will have the ping request time out. On WireShark, there will be many visible requests but no replies. If the ICMP denying rule is deleted or changed to have low priority, replies will be visible again. 

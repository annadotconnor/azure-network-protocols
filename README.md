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

- Create a Resource Group
- Create a Windows 10 VM and a Ubuntu VM
- Download Wireshark to your Ubuntu VM Client
- Ping traffic between VM Clients to observe your Virtual Network has successfully been created

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/nzGyGzR.png" alt="Create Resource Group">
</p>
<p>
Navigate to Microsoft Azure, click Resource Groups from the search bar. Choose a title for your Resource Group, and enter it in the field shown above. Your Resource Group will contain your Virtual Machines. 
</p>
<br />

<p>
<img src="https://i.imgur.com/c6AWstX.png">
</p>
<p>
Go to the search bar again, Click Virtual Machines. In the above screen you will select the Resource Group you created from the drop down menu. Name your Virtual Machine, and select the region local to your location.
</p>
<br />

<p>
<img src="https://i.imgur.com/0t9UaVH.png">
</p>
<p>
In the Image field, you will select your Operating System. For this lab we will be using Windows 10 and Ubuntu Linux. Select Windows 10 from the drop down menu as shown above. Choose the amount of RAM and CPUs you would like your Virtual Machine to have. You will notice the price increases as the amount of RAM and CPU cores you choose increases. It is recommended to choose 2 cores and around 16GB of RAM as we will be destroying both the Virtual Machines and the Resource Group at the end of this lab to ensure any charges will be nominal (usually less than a dollar of your $200 Free Azure Subscription credits). Choosing less is acceptable, but your Virtual Machine may not endure process workload as efficiently.
</p>
<br />

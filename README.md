<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we will observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



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
Go to the search bar, and click Virtual Machines. In the top right corner click Create, and choose Azure virtual machine. This will bring you to the above screen. From here you will select the Resource Group you created from the drop down menu. Name your Virtual Machine, and select the region local to your location.
</p>
<br />

<p>
<img src="https://i.imgur.com/0t9UaVH.png">
</p>
<p>
In the Image field, you will select your Operating System. For this lab we will be using Windows 10 and Ubuntu Linux. Select Windows 10 from the drop down menu as shown above. Choose the amount of RAM and CPUs you would like your Virtual Machine to have. You will notice the price increases as the amount of RAM and CPU cores you choose increases. It is recommended to choose 2 cores and around 16GB of RAM as we will be destroying both the Virtual Machines and the Resource Group at the end of this lab to ensure any charges will be nominal. Choosing less is acceptable, but your Virtual Machine may not endure process workload as efficiently.
</p>
<p>You will also need to choose a username and password. Please be sure to save these as we will need them once you are ready to login to your Virtual Machine. Check the licensing box at the bottom of this page, and click Next.</p>
<br />
<p>
<img src="https://i.imgur.com/WbelqLs.png">
</p>
<p>The next screen will bring you to Disks, please click next to get to the Networking screen shown above. You will see the name of your Virtual Machine has been used to create a Virtual Network. Please take note of this, as we will need to use the same Virtual Network for our Ubuntu Linux server. Scroll down and select Review + Create.</p>
<br>
<p>
 <img src="https://i.imgur.com/4uM2sWX.png"> 
</p>
<p>
 In the top left corner you should see "Validation passed". Please click Create to complete the setup process for your first Virtual Machine. When you reach the next screen you will see "Deployment in Process". It is highly advised you wait a few minutes before creating the next Virtual Machine. If you move on too quickly the machine may not have built your virtual NIC yet, and that will make it inaccessible to the following Virtual Machine. They must use the same Virtual Network.
</p>
<p>
 Once Deployment is complete, please go to the search bar and select Virtual Machines once again. You will repeat the steps above, with a few changes I will outline below.
</p>

<p>
  <img src="https://i.imgur.com/9SaYofJ.png"> 
 </p>
 <p>
 Please choose the same Resource Group you created prior from the drop down menu and name your second Virtual Machine. This will be your Ubuntu Server. Please go to the Image section, and choose Ubuntu Server from the drop down menu as shown above. Click Next on Disks, and remain on the Networking page. We will make changes.
 </p>
 <p>
  <img src="https://i.imgur.com/QOgPmsr.png"> 
 </p>
 <p>
  In the Virtual Network field open the drop down menu and select the vnet previously created by your first Virtual Machine. You will need to be sure this step is completed so your machines are able to communicate on the same Virtual Network. 
 </p>

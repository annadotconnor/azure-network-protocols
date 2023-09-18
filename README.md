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
- Observe Traffic between various Network Protocols

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/nzGyGzR.png" alt="Create Resource Group">
</p>
<p>
Navigate to Microsoft Azure, click Resource Groups from the search bar. Choose a title for your Resource Group, and enter it in the field shown above. Your Resource Group will contain your Virtual Machines. 
</p>
<br><br>

<p>
<img src="https://i.imgur.com/c6AWstX.png">
</p>
<p>
Go to the search bar, and click Virtual Machines. In the top right corner click Create, and choose Azure virtual machine. This will bring you to the above screen. From here you will select the Resource Group you created from the drop down menu. Name your Virtual Machine, and select the region local to your location.
</p>
<br><br>

<p>
<img src="https://i.imgur.com/0t9UaVH.png">
</p>
<p>
In the Image field, you will select your Operating System. For this lab we will be using Windows 10 and Ubuntu Linux. Select Windows 10 from the drop down menu as shown above. Choose the amount of RAM and CPUs you would like your Virtual Machine to have. You will notice the price increases as the amount of RAM and CPU cores you choose increases. It is recommended to choose 2 cores and around 16GB of RAM as we will be destroying both the Virtual Machines and the Resource Group at the end of this lab to ensure any charges will be nominal. Choosing less is acceptable, but your Virtual Machine may not endure process workload as efficiently.
</p>
<p>You will also need to choose a username and password. Please be sure to save these as we will need them once you are ready to login to your Virtual Machine. Check the licensing box at the bottom of this page, and click Next.</p>
<br><br>
<p>
<img src="https://i.imgur.com/WbelqLs.png">
</p>
<p>The next screen will bring you to Disks, please click next to get to the Networking screen shown above. You will see the name of your Virtual Machine has been used to create a Virtual Network. Please take note of this, as we will need to use the same Virtual Network for our Ubuntu Linux server. Scroll down and select Review + Create.</p>
<br><br>
<p>
 <img src="https://i.imgur.com/4uM2sWX.png"> 
</p>
<p>
 In the top left corner you should see "Validation passed". Please click Create to complete the setup process for your first Virtual Machine. When you reach the next screen you will see "Deployment in Process". It is highly advised you wait a few minutes before creating the next Virtual Machine. If you move on too quickly the machine may not have built your virtual NIC yet, and that will make it inaccessible to the following Virtual Machine. They must use the same Virtual Network.
</p>
<p>
 Once Deployment is complete, please go to the search bar and select Virtual Machines once again. You will repeat the steps above, with a few changes I will outline below.
</p>
<br><br>
<p>
  <img src="https://i.imgur.com/9SaYofJ.png"> 
 </p>
 <p>
 Please choose the same Resource Group you created prior from the drop down menu and name your second Virtual Machine. This will be your Ubuntu Server. Please go to the Image section, and choose Ubuntu Server from the drop down menu as shown above. Click Next on Disks, and remain on the Networking page. We will make changes.
 </p>
 <br><br>
 <p>
  <img src="https://i.imgur.com/QOgPmsr.png"> 
 </p>
 <p>
  In the Virtual Network field open the drop down menu and select the vnet previously created by your first Virtual Machine. You will need to be sure this step is completed so your machines are able to communicate on the same Virtual Network. 
 </p>
 <br><br>
<p>
  <img src="https://i.imgur.com/ND1nujv.png"> 
</p>
  <p>
   De-select SSH public key, and choose Password. Input a username and password. These can be the same as what you used for the first Virtual Machine. Click Next: Disks to get to the Networking page. 
</p>
<br><br>
<p>
   <img src="https://i.imgur.com/zWcudlx.png"> 
</p>
<p>
 On the Networking page you will see the Virtual Network field. Please be sure the Virtual Network you took note of from the creation of the Virtual Machine is chosen here. You may need to choose it from the drop down menu if it is now. If you are only given the option to create a new Virtual Network, please stop here, and begin the process to create your second Virtual Machine again. This means the deployment did not fully complete, and the Virtual NIC is not yet being recognized. If you do have this selected please click Review + Create. If your screen says Validation Passed in the upper left corner, click Create. 
</p>
<br><br>
<p>
 <img src="https://i.imgur.com/hovHNcz.png">
</p>
<p>
 We will use Remote Desktop to connect to our VMs. Please navigate to the search bar in Azure and select Virtual Machines. You should see both VMs you created listed here. Please click the first VM (Windows) you created. When the screen loads, on the right near the top you will see the Public IP address. If you hover your mouse next to this it will give you a copy option. Please do this now. 
</p>
<br><br>
<p>
 <img src="https://i.imgur.com/ChXfSTO.png">
</p>
<p>
 To open Remote Desktop please go to your Windows search bar and type Remote Desktop Connection. Click to open, and it should look similar to the image above. From here you will paste the IP address you copied for you VM. Click COnnect. If you Remote Desktop defaults to another Windows user account, click More Choices. Select another account. From here you will user the username and password credentials you created previously. Please enter these and connect to your VM. 
</p>
<br><br>
<p>
 <img src="https://i.imgur.com/ELrmM4Y.png">
</p>
<p>
 Once your VM loads it will go through some Windows startup questions. You can click through these. Open Microsoft Edge and proceed through the startup questions here as well. Once you are able, please navigate to <a href="https://www.wireshark.org/download.html">Wireshark</a> and select the Windows x64 Installer. Please be sure you are downloading this on your VM and not your native PC. 
                                                                                                                                                                                                                       
</p>
<br><br>
<p>
 <img src="https://i.imgur.com/AjL42yQ.png">
</p>
<p>
 Open the Wireshark Installer, and click Next. Click Noted, and proceed to click Next through the following screens, and finally Install. We will not be configuring any installation changes, all standard installation criteria can be left as is. Proceed through any remaining screens, and click Finish to complete. 
</p>
<br><br>
<p>
 <img src="https://i.imgur.com/kykfWq5.png">
</p>
<p>
 Type Wireshark into your Windows search bar, and open your newly stalled program. Once it loads, it should look similar to the image above. Click the line that says Ethernet so yours will appear selected in blue as well, and then click the blue Wireshark logo highlighted in the upper left corner. 
</p>
<br><br>
<h2>Observing ICMP Traffic</h2>
<p> 
 <img src="https://i.imgur.com/EIBa9aC.png">
</p>
<p>
 You will see traffic appear to display within Wireshark. We want to isolate this traffic to only show certail protocols. We will be filtering ping traffic with the Internet Control Message Protocol, otherwise known as ICMP. Please go to the top of the program, and type icmp into the search bar. This will filter our traffic to only show ping requests. 
</p>
<br><br>
<p>
 <img src="https://i.imgur.com/tm49fc3.png">
</p>
<p>
 Minimize your Windows VM, and navigate back to Azure. Click on your second VM (Ubuntu), and on the right side of the screen  you will see the Networking area. Hover to the right of the Private IP address, and copy. 
</p>
<br><br>
<p>
 <img src="https://i.imgur.com/WKICfEC.png">
</p>
<p>
 Please navigate back to your Windows VM, and type Powershell in the Windows search bar. Once opened, it should appear as above. 
</p>
<br><br>
<p>
 <img src="https://i.imgur.com/X4wdCoC.png">
</p>
<p>
 Type ping and enter the Private IP address of the second VM. You will see response in both PowerShell and Wireshark as traffic communicates between our Virtual Machines. At this point you can ping various websites on the internet and observe the ICMP traffic coming through wireshark, as well as PowerShell or your command line. 
</p>
<br><br>
<h2>Observing SSH Traffic</h2>
<br>
<p>
<img src="https://i.imgur.com/yVc3Zc4.png">
</p>
<p>
 Enter SSH into the Wireshark field above as shown. We will now observe SSH traffic in Wireshark as we use PowerShell to enter our second Virtual Machine. If you do not rememeber the Private IP of your second Virtual Machine, please copy this again now (Navigate back to Azure on the second VM screen to copy). 
</p>
<br><br>
<p>
<img src="https://i.imgur.com/EuYoO9Z.png">
</p>
<p>
 Go to PowerShell and type the command as seen above. Hit enter. You will be prompted for a password. This is the password you created along with your credentials for the second Virtual Machine. Please enter. 
</p>
<br><Br>
<p>
 <img src="https://i.imgur.com/Hv5MBGJ.png">
</p>
<p>
 If entered successfully, you will see something like this appear in PowerShell. Please observe the traffic changes in Wireshark as well, you will see various traffic coming through our SSH protocol. From this point you can enter various Linux commands into PowerShell and observe the responses in PowerShell as well as the traffic in Wireshark.
</p>
<br><Br>
<p>
<img src="https://i.imgur.com/Tp2vC80.png">
</p>
<p>
 To close the connection enter the "exit" command as shown above.
</p>
<br><br>
<h2>Observing DNS Traffic</h2>
<p>
 <img src="https://i.imgur.com/WfGwpwA.png">
</p>
<p>
 Enter DNS into the Wireshark field above as shown. To complete this lab we will be observing DNS traffic within Wireshark and PowerShell. 
</p>
<p>
 <img src="https://i.imgur.com/yffFyJS.png">
</p>
<p>
 <img src="https://i.imgur.com/DMNIIL5.png">
</p>
<p>
By using the nslookup command we can observe the DNS traffic within Wireshark and PowerShell. You can enter any websites you choose. I have completed a couple examples below. 
</p>

 

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
A project demonstrating how to observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 22.04

<h2>High-Level Steps</h2>
- Create Azure Resource Group
- Create Windows 10 and Ubuntu VM
- Install Wireshark on Windows 10 VM
- Generate the following network traffic(ICMP, SSH, DNS, DHCP, RDP)
- Observe traffic within Wireshark
- Enable/Disable traffic using Network Security Group
- Clean up lab once finished

<h2>Actions and Observations</h2>

<p>First we create our Resource Group and Virtual Machines</p>

  ![image](https://github.com/loog4/azure-networking/assets/80493463/5b8ccc2e-e0a7-48d5-bfb6-1baab981eb0d)
  ![image](https://github.com/loog4/azure-networking/assets/80493463/e33f8a46-0dd7-4012-8585-b99103f9f4eb)
  ![image](https://github.com/loog4/azure-networking/assets/80493463/d3e72cd1-0651-44ff-92a6-ff5881994911)


<p>Make sure to have the Windows VM create a new virtual network and subnet</p>

  ![image](https://github.com/loog4/azure-networking/assets/80493463/711816b0-7933-4497-b5a1-2f4efea11bee)

  
<p>For the Ubuntu VM we will use the virtual network created by the Windows VM</p>

  ![image](https://github.com/loog4/azure-networking/assets/80493463/4fcce80e-7ccd-4e2b-8d64-fed95ba9f19e)

<p>We then use the windows vm's virtual ip to remote into it using Remote Desktop Connection</p>
<p>(Make sure to use the username you set during setup to login)</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/d32e20a8-a39d-4ddd-9b9c-6fe91e537a40) <br/>
![image](https://github.com/loog4/azure-networking/assets/80493463/9e9e34a4-1d90-49ad-823d-ad0b5f3866a5)
![image](https://github.com/loog4/azure-networking/assets/80493463/c2d0fc9a-3221-4a3f-ad0e-aef1a538cd0d)

<p>Inside the Windows VM, install Wireshark</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/c9bb8629-b241-4381-95c4-9da9ca2a18b8)
![image](https://github.com/loog4/azure-networking/assets/80493463/512b4f11-7b82-46c7-aaa5-72e31f60b4e4)

<p>Once we have this all setup, we can begin observing network protocol traffic by clicking the blue fin on the top left</p>
<p>Starting of with ICMP, simply type on the search bar to filter the traffic</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/f4da2b68-d269-4607-b737-cf40eec68e52)

<p>Next we will ping our Ubuntu VM from our Windows VM and we can see traffic being sent in Wireshark</p>
<p>(Make sure to use the VM's <b>private</b> IP address and not the public one</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/cf0d933f-ae4b-4ba1-8415-c1886339adea)

<p>Go over to the Ubuntu VM's Network Security Group and create a new rule to deny ICMP requests</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/b0c6447b-5bf1-4495-99dc-518e1393a852)


<p>Pinging the VM again will result in timeouts</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/3553d86b-a4ee-4705-97f6-92ec087a0af9)

<p>From this exercise we know now enough to observe traffic of any network protocol.</p>

<h2>SSH traffic</h2>
<p>In our Windows VM, login to the Ubuntu VM using powershell and ssh</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/06d93282-0dae-46f0-a210-5fea5d651d74)

<h2>DHCP traffic</h2>
<p>On Command Prompt, issue the Windows VM a new IP address using the command 'ipconfig /renew'</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/fb725c1e-d2c8-4cf8-87b6-2b96fd066920)


<h2>DNS traffic</h2>
<p>Go back to Command Prompt and use the command 'nslookup' to generate DNS traffic</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/b94f03f8-396f-458b-bc76-cd92e5442688)


<h2>RDP traffic</h2>
<p>When we filter for RDP traffic (tcp.port == 3389), there will a nonstop stream of traffic. This is because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/d53812c7-5abe-464b-a734-24695610b89a)


<p></p>That concludes the Lab and make sure to clean up everything created in Azure to avoid accruing unneccessary costs</p>

![image](https://github.com/loog4/azure-networking/assets/80493463/199977dd-67eb-497f-91b5-e6bbd6bd29e7)



In this lab, I worked on creating an Active Directory filled with 1,000 randomly generated users!

This is the topology of the network that I created using Oracle VirtualBox. I created two different systems, the Domain Controller or DC running Windows Server '19, and a client computer running Windows 10.
![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/5818a48c3259ea3d70878a236985e88f0cf7c252/Screenshots/Active%20Domain%20Screenshots/Screenshot_1.png)

---
To start off the lab, I needed to create a new VM to run the DC on VirtualBox. To do this I allocated 4 processors and 2 GB of ram and used the Windows Server '19 ISO for the OS. I set up two NICs one connected to the internet, and another to connect to the internal network.

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/5818a48c3259ea3d70878a236985e88f0cf7c252/Screenshots/Active%20Domain%20Screenshots/Screenshot_2.png)

Once I configured the VM I booted it up and configured the Ethernet IPv4 properties. Here I set the ip address to 172.16.0.1, subnet mask to 255.255.255.0 and manually configured the DNS to the loopback address. Doing so makes the computer use itself as the DNS address.

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/5818a48c3259ea3d70878a236985e88f0cf7c252/Screenshots/Active%20Domain%20Screenshots/Screenshot_3.png)

## In this lab, I worked on creating an Active Directory filled with 1,000 randomly generated users!

This is the topology of the network that I created using Oracle VirtualBox. I created two different systems, the Domain Controller or DC running Windows Server '19, and a client computer running Windows 10.
![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/5818a48c3259ea3d70878a236985e88f0cf7c252/Screenshots/Active%20Domain%20Screenshots/Screenshot_1.png)

---
To start off the lab, I needed to create a new VM to run the DC on VirtualBox. To do this I allocated 4 processors and 2 GB of ram and used the Windows Server '19 ISO for the OS. I set up two NICs one connected to the internet, and another to connect to the internal network.

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/5818a48c3259ea3d70878a236985e88f0cf7c252/Screenshots/Active%20Domain%20Screenshots/Screenshot_2.png)

Once I configured the VM I booted it up and configured the Ethernet IPv4 properties. Here I set the ip address to 172.16.0.1, subnet mask to 255.255.255.0 and manually configured the DNS to the loopback address. Doing so makes the computer use itself as the DNS address.

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/5818a48c3259ea3d70878a236985e88f0cf7c252/Screenshots/Active%20Domain%20Screenshots/Screenshot_3.png)

Next, we need to download Active Directory Domain Services or ADDS. 

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/a748adf7b7a28305b557eb1e937fcdb053f0ec0a/Screenshots/Active%20Domain%20Screenshots/Screenshot_4.png)

Once we installed ADDS onto the system we need to configure a new domain name. For this lab I just used the name "mydomain.com". 

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/a748adf7b7a28305b557eb1e937fcdb053f0ec0a/Screenshots/Active%20Domain%20Screenshots/Screenshot_5.png)

I made an Administrator account for myself in the AD, using the "Active Directory Users and Computers" application to do so. Giving myself Admin permissions over the system allows me to control all the users that are added. Allowing me to create user groups for teams. Say within my company we have three tiers of employees, T1, T2, and T3, all with increasing permissions as you get promoted. Each group T1, T2, and T3, have different permissions than the last, T1 having the lowest and T3 having the highest, right up to under Admin permissions. Giving myself Admin permissions to the AD I will later create 1,000 random employeees and will be able to group each random employee into a group with a set of permissions. 

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/a748adf7b7a28305b557eb1e937fcdb053f0ec0a/Screenshots/Active%20Domain%20Screenshots/Screenshot_6.png)

After setting up my Admin permissions, I need to set up Routing. Setting up routing allows all computers on the local network to route through one public IP address. Setting this up simplifies network administration, as you only need to make changes to security rules or access policies through the public IP rather than each individual device within the netowrk. Doing everything through one public IP address also makes it a lot cheaper for the company setting it up, since there's a limited amout of IPv4 addresses out there buying a single public IP costs an arm and a leg. 

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/a748adf7b7a28305b557eb1e937fcdb053f0ec0a/Screenshots/Active%20Domain%20Screenshots/Screenshot_8.png)

After setting up Routing, we still need to set up the DHCP server so the internal users can access the internet. To do this I'll set up the DHCP server on the Domain Controller. I configured a scope for the DHCP Server to assign IP addresses to users computers from the range 172.16.0.100/24 to 172.16.0.200/24. The subnet mask for this is 255.255.255.0/24. The lease duration defaults to 8 days, I changed the lease duration to 3 days for this lab. The default gateway that I'm going to assign to this is the internal NIC of the DC which is 172.16.0.1. 

---

After setting up routing, and the DHCP server we are ready to add in our users. Using a first and last name generator I randomly generated a list of 1,000 names. Below is a snippet of the top bunch of names, I included my name on the top "Trey Atwood" to add another easily findable user later on. 

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/a748adf7b7a28305b557eb1e937fcdb053f0ec0a/Screenshots/Active%20Domain%20Screenshots/Screenshot_11.png)

Next using Powershell ISE I used a script file to create the users into the Active Directory. 

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/a748adf7b7a28305b557eb1e937fcdb053f0ec0a/Screenshots/Active%20Domain%20Screenshots/Screenshot_10.png)

Breaking down this script from the top, I hardcoded all the users passwords to "Password1" for simplicity, and pulled the list of names from the .\names.txt file I created with the randomly generated names. The line starting with "New-ADOrganizatoinalUnit" creates a new group in the AD called _USERS. Lastly the foreach loop at the end, runs for each user in the names.txt file. The variable $n represents the current user that is being examined. In this case the first name is mine "Trey Atwood". The first line in the loop $first = $n.split(" ")[0].ToLower takes the space out between my name, makes it lowercase, and ignores what's after the space, so instead of "Trey Atwood" it's now "trey". The next line saves my last name, it once again splits it at the space between Trey and Atwood and saves my last name as "atwood". The third line starting with the $username variable creates the username. This works by taking my $first name which is stored as "trey" and taking the character between the 0 and 1 column, which is just "t", it then concatenates it with my full last name. Creating the username tatwood for me. That process is repeating 1,000 more times until each name in the names.txt file is accounted for. 

To check to see if everything worked as it should we can go back to Active Directory Users and Computers and check to see if the new group _USERS is there.

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/a748adf7b7a28305b557eb1e937fcdb053f0ec0a/Screenshots/Active%20Domain%20Screenshots/Screenshot_12.png)

As you can see from the image, I searched the AD for users with the name "Atwood" in them and you can see my admin account that I made for myself and the account that I made using powershell for a user. To the left you can see all the other users that were created, it's not showing all 1,000 on one screen but you can see the top of the list!

---
## Creating the Windows Client

Following roughly the same settings as I used for the DC Client I set up the Windows Client that is running Windows 10 for the users. The only setting that I changed is the network settings, which I set the NIC to attach to the internal network. Following all the Windows setup steps I configured the OS and the systems ready to use. 

Here's where I ran into a hiccup, when I went to check to see if I was connected to the network I didn't have a default gateway when I checked the IPConfig in the CMD. 

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/767e4ec6ab7ca462b66a01a83d7771046cd71b1d/Screenshots/Active%20Domain%20Screenshots/Screenshot%202025-11-06%20130821.png)

As you can see here it has the IPv4 Address and the Subnet Mask but no default gateway. This took me a while to figure out and some researching but I had found that I had forgot to confirm the Routing changes that I had made. So I had set up Routing but didn't actually set it with the IP. (oops)

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/04ff547e6823d78cb00fc62f393266ac5d2fc9af/Screenshots/Active%20Domain%20Screenshots/Screenshot%202025-11-06%20131158.png)

Checking the IPConfig again this time we have a Default Gateway! 🎉

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/2a1adabbfe68da7d07f0ea83a6240c32857654c2/Screenshots/Active%20Domain%20Screenshots/Screenshot%202025-11-06%20131503.png)

Just to make sure that it worked I pinged www.google.com, and got a response meaning we are connected to the internet! After fixing this I renamed the system that I created to Client1, and connected it to the domain I created (mydomain.com). I logged in using my user credentials "tatwood" and password "Password1", and checked the DC to see if there was an IP being leased and sure enough there it was!

![image](https://github.com/Frank-Atwood/Cyber-Projects/blob/70ad4ae7b556579bee13d599b7ea1880abce801a/Screenshots/Active%20Domain%20Screenshots/Screenshot%202025-11-06%20131852.png)

---

## Key Takeaways

From this project I had gotten some familiarity with setting up a new Active Directory, setting up Routing and a local DHCP Server and using a Powershell Script to create new users. It was frusterating to see that it didn't work at first, and most of the time nothing does! Being able to troubleshoot to see what my issue was when I didn't have a default gateway on my Windows Client system was fun to do more deep research about why my gateway wasn't showing up. In the end the little hiccup just made the completion just that much more satisfying. I look forward to have the opportunity to use these new skills that I learned in a real enviroment, and to be able to learn more past the basic functions of Active Directory. I'm excited to complete more labs in the future! 

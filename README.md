**Introduction: Practical Vulnerability Assessment** br
The report is a practical demonstration of offensive and defensive security techniques. The focus includes traffic analysis and malware identification, as well as port scanning and legitimate service verification. It shows a good understanding of tools like Wireshark, Nmap, WindowsPowershell, Windows task Manager and VirusTotal. It also shows an understanding of network troubleshooting commands.
1.	Network Vulnerability scanning: Packet Sniffing
Aim: To monitor data packets and capture the passwords, taking into consideration the different Protocols, actions requests such as POST or GET. Softwares used in Oracle VirtualBox:  I used Wireshark to analyse the packet with the IP: 10.0.2.15 which is on HTTP protocol.

1.	Kali Linux 
2.	Wireshark 

**Steps**
Slect the application icon on the top left of your Kali linux as marked in green on the screenshot 1 below. Using the search box as shown of the screenshot two to search for wireshark and open by clicking once on wireshark.


<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/266b547f-0b84-466f-b40e-c366b0107e6e" />

After opening the wireshark, the screen will show as captured below. In this case, we will be using eth0. As shown on the screen below as well, I was on tab 2. 

<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/f905e8f9-6372-4574-95b7-418336772d16" />


At this point, I swtched to tab 1 where I opened the firefox browser to search for the website I used for this simulation: www.techpanda.org (This is just for practical) 

 
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/181a3cd9-3d59-495a-9c6b-8e5af962c72e" />


After entering the website, the login page below opens. This is similar to a normal website that one can visit and try to login on daily basis. Here I entered wrong email address and password while we capture the traffic of login requests. Note that there are some actions which can be performed in the process of using the web and this is normally under the info column of of the logs captured as shall be seen in subsequent screenshots. However, in this case, I am concerned with Post and Get reguests. The login detail used include:
email address: gshddhhd@gmail.com
Password: thththth

 <img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/54cb8307-30e6-4f86-a5a9-fcfec6b70796" />

Outcome: Going back to wirshark, it has already captures some traffic. And I searched based on protocol, htt p for the IP: 10.0.2.15 The vulnerability of HTTP protocol made it possible to see the login detail of the IP user 10.0.2.15, as highlighted on the screenshot below. Knowing that the unsecure web protocaol was based on pot 80 which is HTTP and I made a POST by sending a login request, I can search for the HTTP protocol as shown below with a POST action under the info column.

 <img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/9de8f16d-cb28-4c9c-a5ef-e75c3fc53902" />


2. **Scanning of Hash value**
Hash Value: f02ce710874cd773c3c32730dc2536d14f4e419bf828d4a27664a24af5d4484f
Tools used: Virus total, 
Results, Type of Hash: SHA 256  

<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/76b4b18a-ea16-4886-aad3-1fc7aeed728b" />

Decision: It is a trojan malicious file because: 
a. The community vulnerability score ratio shows 42/64
b. the file hash valued has varied into four different types making it suspicious: like
1.  _f02ce710874cd773c3c32730dc2536d14f4e419bf828d4a2 7664a24af5d4484f.elf 
2. f02ce710874cd773c3c32730dc2536d14f4e419bf828d4a27 664a24af5d4484f.elf
3.  jmlvg.exe
4. Polar.ppc.elf
**Family**: the hash variant belongs to Condi malware family, a botnet which affects vulnerable network devices on Linux.

2.	**Nmap scan, WindowsPowerShell and Wndows Task Manger**

**Purpose**: To find out the open pots on my windows computer, why they are open and the service listening on those pots.
Tools: Nmap on Kali Linux, windows PowerShell and Windows task manager.
Processes:
1.	I scanned my IP to find out the pots that are open. For security reasons, I won’t add my IP address here: the result of the scan shows the following;
To run a scan, I used the following command; Nmap 192. 168.20.10 (random IP for this report).
**Outcome**: The result shows that many pots below are open. Looking at port 135/tcp as a case, I tried to find out the process that runs on pot 135.

 <img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/629dc4ad-c80a-4351-b279-6060d84205c9" />

To find out the services that are listening to 	all the pots, I entered the command; sudo netstat -tulpn (the columns showed but no data were populated). I also tried other commands such as; sudo ss -tulpn and netstat -tulpn but no result was showing. Then I moved to windows PowerShell since the IP I scanned was from a windows PC. 

**Next Step**: I ran the windows PowerShell as an administrator and entered the command; netstat -ano, to see the list of active connections. The list below shows that port 135/tcp has PID of 1592. The PID is process ID and it is useful in finding out which connection is attached to a specific service.

<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/5f6f8537-06b6-4804-a79b-e96918f8aeb7" />

TO find out the process that is running with the PID of 1592, I opened the windows task manager of my computer. On the task manager, I selected the details menu to see the processes that are running with their respective PID. The output of my search after pressing CTRL F and entering the PID 1592 is indicated below:

<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/49b39c35-9658-487a-9bbe-f28e66c2917d" />

The PID 1592 shows that the process is associated with the ID is swchost.exe, upon my research, I found that the service swchost.exe is a legitimate windows service.  As a result, the msrpc service as shown below is a legitimate windows service


**Implication**: Open ports could be a means for attackers to penetrate a computer. Although, swchost.exe  is legitimate,  other ports need to be protected by being closed to avoid being an exploited by an attacker.


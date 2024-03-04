<h1>Guarding Data in Transit</h1>

<h2>Description</h2>
File Transfer Protocol (FTP), is an application layer protocol designed for the transfer of files. It operates on port 21 and utilizes TCP for transmitting data. While it may not be as widely used as in the past, FTP remains in use today, making it crucial to understand its vulnerabilities for effective security measures.
<br />


<h2>Requirements</h2>

- <Metasploitable(VM1)</b> 
- <Kali Linux(VM2)</b>
- <NMAP</b>

<h2>Setup Instructions </h2>
Verify that both virtual machines (VMs) are configured to operate within the same network. Confirm their connectivity by conducting a mutual ping test.
Subsequently, proceed to download and install NMAP on your target machine, which in this context is a Kali Machine.
<br />

<h2>Steps</h2>
Perform a vulnerability scan on your target machine, which is Metasploitable, by executing the following command: <b>nmap -sV [target's IPv4 address]</b> Upon executing this command, you will receive scan results similar to those depicted in the "Nmap Scan Results" image. Notably, the results indicate that FTP is operational on port 21, with the version specified as vsftpd 2.3.4, and the state is marked as open.


<p align="center">
Scan Target Machine:  <br/>
<img src="https://imgur.com/TsNDJK2.png" height="80%" width="80%" alt="Disk Sanitization 
 Steps"/>
<br />
<br />
 
To further exploit this situation, initiate the MSFCONSOLE, a Metasploit framework. Once it's up and running, search for additional information related to vsftpd. The search results, as illustrated in the accompanying figure, will reveal that the exploit is located within the directory "exploit/unix/ftp/vsftpd."

<p align="center">
MSFCONSOLE Launch:  <br/>
<img src="https://imgur.com/2opHAxu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
 
Navigate into this directory using the command "use exploit/unix/ftp/vsftpd," and subsequently use "show options" to gather comprehensive details. The outcome will indicate the presence of two key parameters: RHOST (remote host) and RPORT (remote port). A closer examination reveals that RPORT has been configured with a value of 21, while RHOST remains unassigned, as depicted in the provided figure below.

<p align="center">
Exploit Directory: <br/>
<img src="https://imgur.com/hQn3bTn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 
To set the remote host to the IP address of the target machine, employ the command "Set RHOST 192.168.182.133." After successfully configuring the IP, execute the "exploit" command. The results, as indicated in the figure below, confirm that a shell has been successfully established following the exploit, and the shell is now accessible.

<p align="center"> 
Detail Analysis:  <br/>
<img src="https://imgur.com/Cic6ptc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 
To validate the acquired access, issue the command 'Whoami.' The outcome, illustrated in the accompanying figure, should display "root." This signifies that Kali has gained root-level access to the Metasploitable Target Machine, granting the capability to make alterations to the directory and execute privileged operations such as creating a directory. 

<p align="center"> 
Access Granted:  <br/>
<img src="https://imgur.com/sdFNHIb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>Key Takeaways: </h2>
While FTP serves as a valuable protocol, it also harbors vulnerabilities that malicious actors can exploit to elevate their privileges to root. This elevation of privileges can result in significant harm, potentially leading to the loss of revenue for companies or even jeopardizing data and lives if the targeted company offers services to healthcare facilities. Hence, administrators must remain vigilant about these vulnerabilities and proactively address them by implementing Intrusion Detection Systems (IDS) and Intrusion Prevention Systems (IPS).

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>

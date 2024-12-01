# Hacking a Windows Server via the Metasploit Framework 
## Description
This project involves hacking a vulnerable Windows Server 2008 R2 system using the Metasploit Framework (MSF). The goal was to exploit two main vulnerabilities, demonstrating each phase of the hacking process, and providing comprehensive documentation of the methods and findings.

## Lab Setup
The lab setup included a Windows Server 2008 R2 virtual machine used as the victim device and a Kali Linux virtual machine with the Metasploit Framework installed and used as the attacker machine. The main tool used to attack the Windows Server was the Metasploit Framework.

### The vulnerabilities explored
1. EternalBlue (MS17-010)
2. PsExec


## Step 1: CVE Research
I began my reconnaissance by searching for vulnerabilities related to Windows Server 2008 R2 on the CVE website. This research was essential to identify potential exploits that could be leveraged.

![cve](https://i.postimg.cc/QM68jhz2/0-went-to-cve-to-look-for-vulnerabilites-on-windows-server-2008.png)

- I found multiple vulnerabilities related to Windows Server 2008 R2. One significant finding was CVE-2017-0148, known as **EternalBlue.** This vulnerability targets the SMBv1 protocol, allowing for remote code execution.

- I reviewed the detailed CVE description of EternalBlue to understand its impact and method of exploitation. This vulnerability is dangerous because it allows attackers to send specially crafted packets to the target server, gaining unauthorized access.

![sec](https://i.postimg.cc/rppTn7pQ/0-1-found-out-about-the-eternal-blue-vulnerability-that-uses-smb.png)

## Step 2: Network Configuration

To prepare for the exploitation, I configured the network settings on both the attacker (Kali Linux) VM and the target (Windows) VM to ensure they were on the same network. This step was crucial for successful communication between the machines.

> Static IP address for the Kali Linux VM

![kali](https://i.postimg.cc/hj6K7McM/1-assigning-a-static-IPv4-address-to-the-kali-linux-vm-and-testing-the-connection-to-make-sure-it-w.png)

> Static IP address for the Windows Server

![fav](https://i.postimg.cc/Vvtm9MNw/2-assinging-a-static-ipv4-to-the-windows-vm-to-get-it-on-the-same-network-as-the-kali-linux-vm.png)

## Step 3: Scanning and Enumeration

Using Nmap, I scanned the target Windows VM to identify open ports and services. The scan revealed that port 445 (SMB) was open, indicating a potential entry point for the EternalBlue exploit.

![namp](https://i.postimg.cc/vBcQBCFc/3-performed-a-network-scan-on-the-windows-vm-and-found-that-smb-was-open-attack-vector.png)

## Step 4: Setting up PostgreSQL for Metasploit
Before launching Metasploit, I ensured that PostgreSQL was running, as it is required for Metasploit's database operations. The command 'sudo service postgresql start' was used to start the service.

![PostgreSQL](https://i.postimg.cc/4NzXmzMb/4-enabling-postgresql-a-relational-database-with-many-uses.png)

## Step 5: Configuring EternalBlue in Metasploit

I launched Metasploit Framework to set up and run the exploit for EternalBlue. This tool is a powerful open-source penetration testing framework that allows for a variety of exploitations and post-exploitation tasks.

- In Metasploit, I searched for the EternalBlue exploit module using the command 'search eternalblue'. This step helps in identifying the exact module needed for the exploitation.

![eteranlblue](https://i.postimg.cc/wxRqdKQr/6-seraching-the-msf-for-eternalblue-vulnerabilities-that-we-can-potentially-exploit.png)


Then I configured the EternalBlue exploit so it could effectively deliver the payload. I configured the exploit by setting the target IP address 192.168.183.130 (RHOST) and the listening port 4322 (LPORT) to prepare the payload. This setup ensures that the payload is sent to the correct target and listens for a reverse shell connection.

![static](https://i.postimg.cc/qvw0GppN/9-set-the-remote-host-s-ip-address-to-the-ip-address-of-the-windows-vm-so-the-payload-knows-where-t.png)

## Step 6: Exploiting EternalBlue 

With the exploit configured, I ran the 'exploit' command to execute the attack. Once successful, the payload was executed and I gained access to the Windows VM. The “meterpreter” session was created, which allowed me to have access to the Windows VM. I ran the command “sysinfo” to ensure that we did indeed have access to the right machine. I also ran the command “ipconfig” to get an overview of the network configuration of the Windows VM. I was able to verify that I indeed had access to the Windows Server 2008 R2 with the IP address 192.168.183.130.

![jh](https://i.postimg.cc/JhdL9KDm/10-exploiting-the-vulnerability.png)

![ad](https://i.postimg.cc/852VC5m0/10-1-proof-that-we-got-in-using-eternalblue.png)









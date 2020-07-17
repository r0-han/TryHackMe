# TryHackMe Kenobi
**Walkthrough on exploiting a Linux machine. Enumerate Samba for shares, manipulate a vulnerable version of proftpd and escalate your privileges with path variable manipulation.**

## Task-1 Deploy the vulnerable machine

2. Scan the machine with nmap, how many ports are open?<br>
Answer : 7 (*nmap ip*)

## Task-2 Enumerating Samba for shares

1. Using nmap we can enumerate a machine for SMB shares. Nmap has the ability to run to automate a wide variety of networking tasks. There is a script to enumerate shares! nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.79.73. SMB has two ports, 445 and 139. Using the nmap command above, how many shares have been found?<br>
Answer : 3 (*using above command*)

2. On most distributions of Linux smbclient is already installed. Lets inspect one of the shares. smbclient //<ip>/anonymous. Using your machine, connect to the machines network share. Once you're connected, list the files on the share. What is the file can you see?<br>
Answer : log.txt (*using above command*)

3. You can recursively download the SMB share too. Submit the username and password as nothing. smbget -R smb://<ip>/anonymous Open the file on the share. There is a few interesting things found. Information generated for Kenobi when generating an SSH key for the user. Information about the ProFTPD server. What port is FTP running on?<br>
Answer : 21 (*using above command*)

4. Your earlier nmap port scan will have shown port 111 running the service rpcbind. This is just an server that converts remote procedure call (RPC) program number into universal addresses. When an RPC service is started, it tells rpcbind the address at which it is listening and the RPC program number its prepared to serve. In our case, port 111 is access to a network file system. Lets use nmap to enumerate this. nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.79.73. What mount can we see?<br>
Answer : /var (*using above command*)

## Task-3 Gain initial access with ProFtpd

1. Lets get the version of ProFtpd. Use netcat to connect to the machine on the FTP port. What is the version?<br>
Answer : 1.3.5 (*nc ip 21*)

2. We can use searchsploit to find exploits for a particular software version. Searchsploit is basically just a command line search tool for exploit-db.com. How many exploits are there for the ProFTPd running?<br>
Answer : 3 (*searchsploit ProFTPd 1.3.5*)

5. What is Kenobi's user flag (/home/kenobi/user.txt)?<br>
Answer : d0b0*****************************

## Task-4 Privilege Escalation with Path Variable Manipulation

1. What file looks particularly out of the ordinary? <br>
Answer : /usr/bin/menu (*using command in desc*)

2. Run the binary, how many options appear?<br>
Answer : 3 (*/usr/bin/menu*)

4. What is the root flag (/root/root.txt)?<br>
Answer : 177b***************************** (*follow the given steps in #3 and then 'cat /root/root.txt'*)


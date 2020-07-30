# TryHackMe Attacktive Directory 
**99% of Corporate networks run off of AD. But can you exploit a vulnerable Domain Controller?**

## Task-3 

* First ran nmap scan and got the answers for all questions of Task-3. Command used was '*nmap -sV -A -v ip*''

1. How many ports are open under 10,000? (Note it may take up to 5 minutes for all the services to start)<br>
Answer : 11

2. What tool will allow us to enumerate port 139/445?<br>
Answer : enum4linux

3. What is the NetBIOS-Domain Name of the machine?<br>
Answer : THM-AD

4. What invalid TLD do people commonly use for their Active Directory Domain? <br>
Answer : .local

## Task-4 Enumerate the DC Pt 2

* I didn't use Kerbrute as given in the description as it was not working in my kali. If you have your Kerbrute working fine then please see other writeup as I am going to enumerate users using 'GetNPUsers.py'. So I searched for GetNPUsers.py in my kali and then ran the following command to get list of users. For this I used the username list provided in the description. Just 'wget github_link_in_desc' for both username and password list.

* The command is '*python3 GetNPUsers.py -dc-ip IP -userfile userlist.txt -no-pass spookysec.local/*'. It will run for some time and will give the list of users - 'James','darkstar','paradox','administrator','backup','svc-admin','robin'. We will be provided with the hash of 'svc-admin'.

1. What command within Kerbrute will allow us to enumerate valid usernames?<br>
Answer : user-enum

2. What notable account is discovered? (These should jump out at you)<br>
Answer : svc-admin

3. What is the other notable account is discovered? (These should jump out at you)<br>
Answer : backup

## Task-5 Exploiting Kerberos

* After getting the hash we can crack it using hashcat. First find the mode of kerberos for hashcat to identify. Then type the command '*hashcat -m 18200 -a 0 passwordlist.txt --force*'. we didn't use rockyou as we have given a default password list to look for. After this we got password as 'management2005'.

1. We have two user accounts that we could potentially query a ticket from. Which user account can you query a ticket from with no password?<br>
Answer : svc-admin

2. Looking at the Hashcat Examples Wiki page, what type of Kerberos hash did we retrieve from the KDC? (Specify the full name)<br>
Answer : Kerberos 5 AS-REP etype 23

3. What mode is the hash?<br>
Answer : 18200

4. Now crack the hash with the modified password list provided, what is the user accounts password?<br>
Answer : management2005

## Task-6 Enumerate the DC Pt 3

* After getting the credentials we can log into smbclient as we have seen that port 139,445 is open. Type '*smbclient -L IP -U 'svc-admin'*' and it will prompt for a password. Type the password which we got from above results. Now we will see a share named 'backup' which we can access. Now type '*smblcient //IP/backup -U 'svc-admin'*' and login again with that password. 

* Now type 'ls' in the smb shell and you will get a 'backup_credential.txt' file .Type '*get filename*' and that file will be on your kali machine. Now see its content , it is a base64 encoded string. After decoding that it gives 'backup@spookysec.local:backup2517860'. 

1. Using utility can we map remote SMB shares?<br>
Answer : smbclient

2. Which option will list shares?<br>
Answers : -L

3. How many remote shares is the server listing?<br>
Answer : 6

4. There is one particular share that we have access to that contains a text file. Which share is it?<br>
Answer : backup

5. What is the content of the file?<br>
Answer : YmFja3VwQHNwb29reXNlYy5sb2NhbDpiYWNrdXAyNTE3ODYw

6. Decoding the contents of the file, what is the full contents?<br>
Answer : backup@spookysec.local:backup2517860

## Task-7 

* Now locate secretsdump.py file in your machine. For privesc type the command '*python3 secretsdump.py -just-dc backup@spookysec.local*' and it will ask for a password. Password is the last part in above answer after ':'. Then we get the hash for Administrator. The last part between two ':' is the administrator's hash. As ques 3 suggest we don't need to crack this password.

* Now we will use a tool 'evil-winrm' for privilege escalation. Type the command '*evil-winrm -i IP -u administrator -H hash_of_administrator*'. And we have access to administrator. 

1. What method allowed us to dump NTDS.DIT?<br>
Answer : DRSUPAI

2. What is the Administrators NTLM hash?<br>
Answer : e4876a****************

3. What method of attack could allow us to authenticate as the user without the password?<br>
Answer : Pass the Hash

4. Using a tool called Evil-WinRM what option will allow us to use a hash?<br>
Answer : -H

## Task-8 Flags

* Traverse through the respective directories to find flags.

1. svc-admin<br>
Answer : TryHackMe{K3rb3r0s_Pr3_****}

2. backup<br>
Answer : TryHackMe{B4ckM3Up******!}

3. Administrator<br>
Answer : TryHackMe{4ctiveD1rectory******} 
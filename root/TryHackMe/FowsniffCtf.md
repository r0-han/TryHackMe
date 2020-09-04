# Fowsniff CTF
**Hack this machine and get the flag. There are lots of hints along the way and is perfect for beginners!**

## Task-1

* Enumeration
 
** Start by doing nmap scan ( ' *nmap -sC -sV IP* ' ). We got ports - 22, 80, 110, 143 open.

1. Starting by enumerating port 80. It is a basic website which gives us hint - 'The attackers were also able to hijack our official @fowsniffcorp Twitter account'. 

** So on navigating to their twitter account, gave us a 'pastebin' link where we can se credentials of various users. Copy all these into a file and then go to https://crackstation.net/ to crack these hashes. You can get all the users in a separate file by typing command ( ' *awk 'BEGIN {FS="@"} { print $1 }' aboveSavedFile > user.txt* ' ) and hashes as (  ' *awk ' BEGIN {FS=":"} { print $2 } ' aboveSavedFile > hash.txt* ' ). Now crack these hashes and save all the passwords in a file called pass.txt.

* As we have password and user list, now we can brute force into pop3 login using metasploit module. Open 'msfconsole' and then type ( ' *use auxiliary/scanner/pop3/pop3_login* ' ) and then type 'options'. Now set these commands in metasploit - <br>
- set RHOSTS MACHINE-IP<br>
- set PASS_FILE pass.txt<br>
- set USER_FILE user.txt<br>
- set STOP_ON_SUCCESS true<br>
- run<br>
This confirms that we can login into pop3 using 'seina'.

** Now type ( ' *nc MACHINE_IP 110* ' ) and then type :<br>
- user seina<br>
- pass scooby****<br>
After successfully loggin in type : <br>
- LIST<br>
- RETR 1<br>
- RETR 2<br>

In 'Mail 1' we can see temporary ssh password and in 'Mail 2' we can see the name of user who sent the mail - 'baksteen'

2. Now login into ssh using the above temporary password and user.

** In the shell type 'groups' to list the groups baksteen is part of. We get 'users'. Now type ( ' *find / -type f -group users 2>/dev/null* ' ) to see what files can baksteen run. We see a file named 'cube.sh'. To see this file type ( ' *cat /opt/cube/cube.sh* ' ) and we see that this was just the header which we get when we are successfully looged in thru ssh.

** Now edit this file using any editor and then type the python3's reverse shell (as given in the room material)  in the end of the file. Now in another terminal start your nc listener and then log again to the ssh. Now you will get root login in nc shell.

## 7. What was seina's password to the email service?<br>
Answer : scooby****

## 8. Looking through her emails, what was a temporary password set for her?<br> 
Answer : S1ck3nBluff+***********

![flag](flag.png)
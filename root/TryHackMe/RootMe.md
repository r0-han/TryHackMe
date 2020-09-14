# RootMe 
**A ctf for beginners, can you root me?**

## Task-2 Reconnaissance

1. Scan the machine, how many ports are open?<br> 
Answer : 2  ( ' *nmap -sC -sV IP* ' )

2. What version of Apache are running?<br>
Answer : 2.4.29

3. What service is running on port 22?<br>
Answer : ssh

5. What is the hidden directory?<br>
Answer : /panel/  ( ' *gobuster dir -u http://IP -w directory-medium.txt* ' )

## Task-3 Getting a shell

* Go to the hidden directory and try to upload php file. This process shows error.So I tried with different extensions and luckily php5 worked. Now upload your php reverse shell with extension .php5 and go to /uploads/ and then click on your reverse shell.

1. user.txt<br>
Answer : THM{y0u_g0t_*_*****}

## Task-4 Privilege Escalation

1. Search for files with SUID permission, which file is weird? <br>
Answer : /usr/bin/python ( ' *find -type f -perm -u=s 2>/dev/null* ' )

3. root.txt<br>
Answer : THM{pr1v1l3g3_**********} ( ' *go to gtfobins and search for python suid. Then cat /root/root.txt* ' )
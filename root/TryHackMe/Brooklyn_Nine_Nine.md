# TryHackMe Brooklyn Nine Nine
**This room is aimed for beginner level hackers but anyone can try to hack this box. There are two main intended ways to root the box.**

* There are two ways of rooting this box as description says. Below is the First method.

## 1. Task-1 Deploy and get hacking

* Starting enumeration by nmap scan gave us port - 21,22,80. After going on the http port(80) it shows us a background image with some text at bottom. So I viewed its source code and in there was a comment 'Have you ever heard of steganography?'.

* After downloading the image I immediately tried 'stegsolve' to solve it. But it was showing that it was zlib compressed meaning it was password protected. So I used stegcracker (*stegcracker file.jpg*) to crack it and got the password as 'admin'. After decoding the file it gave us 'Holt' password. Credentials are 'holt:fluffydog12@ninenine'. 

* As we saw in nmap scan that port - '22', ssh is open. So we tried loggin into holt and we're successful. Type 'ls' after ssh login and you will see user.txt file.

1. User flag<br>
Answer : ee11cbb19052e40b07aac0**********

* Now for the root acces  as the hint says type 'sudo -l' and you will see that user can run '/bin/nano'. So go to https://gtfobins.github.io/ to search for sudo of nano. We got 'sudo nano<br>^R^X<br>reset; sh 1>&0 2>&0'. '^R^X' means 'ctrl+R and ctrl+X'. Type these commands and you will have root access.

2. Root Flag <br>
Answer : 63a9f0ea7bb98050796b64**********

* Below is the second method

## 2. Task-1 Deploy and get hacking

* In the above nmap scan we saw port - '21' , ftp open. So we can try 'anonymous' login thru ftp. Type '*ftp ip*' and then username and password as 'anonymous'. We have successfully logged in to ftp and now type 'ls'. You will see a .txt file. Type 'get file_name.txt' to get the file in local machine. Exit the ftp shell.

* Now see the content of file using 'cat'. From that we see a username as 'Jack'. For password cracking we can try hydra. Type '*hydra -l jake -P rockyou.txt ssh://ip*' We got password as '987654321'. Now log in ssh using the creds 'jake:987654321'.

* Now go to 'holt' directory using '*cd /home/holt*' and type 'ls'. You will see user.txt file.

* For root acces  type 'sudo -l'. We see user can run '/usr/bin/less' . Search for its sudo privilege on gtfobins(link given above). Now type the following commands 'sudo less /etc/profile<br>!/bin/sh' and you will have your root shell.
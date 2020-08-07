# TryHackMe Boiler CTF
**Intermediate level CTF**

## Task-1 Questions #1

* On enumeration nmap gave port - 21(ftp), 80(http), 55007(ssh) open. First I tried anonymous login on ftp server and got successful. In there was a hidden file . On reading that file it was a ROT13 encoded string which on decoding gave - 'Just wanted to see if you find it. Lol. Remember: Enumeration is the key!'.

* After that I ran gobuster and found out the cms name - 'joomla'. Then I searched for /joomla in the gobuster and got another interesting page - '_ files'. On this site was a base64 encoded string which on further decoding gave a hash which on cracking gave output - 'kidding'. It was a rabbit hole!.

* We also found out another page named - '_ test'. In that was a 'sar2html' page. I searched for it in google and found its exploit (RCE). After performing RCE on this and by typing 'ls' we see a 'log.txt' file. After viewing its content it gave us a password to 'basterd' user. So we can ssh login into it.

* Type 'ssh basterd@ip -p 55007' and then password. We are successfully logged in.

1.  File extension after anon login<br>
Answer : txt

2. What is on the highest port?<br>
Answer : ssh

3. What's running on port 10000?<br>
Answer : webmin

4. Can you exploit the service running on that port? (yay/nay answer)<br>
Answer : nay  (*as the current version is nearly latest*)

5. What's CMS can you access?<br>
Answer : joomla

7. The interesting file name in the folder?<br>
Answer : log.txt

## Task-2 Question #2

* After successfully logging to basterd we can see a backup.sh file which contains password to another user 'stoner'. So we can log in stoner using this password and there is a hidden file '.secret' file. This is the user flag.

* Now I searched for SUID using command 'find / -perm -u=s -type f 2>/dev/null' and got something interesting. We can elevate privileges using SUID of 'find'. You can see that on gtfobins. After running that command we have gained root shell. Now you can type 'cat /root/root.txt'

1. Where was the other users pass stored(no extension, just the name)?<br>
Answer : backup

2. user.txt <br>
Answer : You made it till here, **** ****.

3. What did you exploit to get the privileged user?<br>
Answer : find

4. root.txt <br>
Answer : It wasn't that hard. *** ** ?

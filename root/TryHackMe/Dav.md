# TryHackMe Dav
**boot2root machine for FIT and bsides guatemala CTF**

## Task-1 Dav

* Enumeration - After running nmap scan we find that only port 80 is open. Looking at port 80 gave us a default apache webpage.

* For sub-directory I used gobuster using command ( ' *gobuster dir -u http://IP -w common.txt* ' ) and we found a directory named 'webdav'. After looking at this directory a pop-up opened for username and password. So I searched on google for webdav and also default creds for that. I found a site ( http://xforeveryman.blogspot.com/2012/01/helper-webdav-xampp-173-default.html ) which gave us default creds. 

* After searching more about webdav, I found that we can use 'cadaver' to access webdav. Command used was ( ' *cadaver http://IP/webdav* ' ) and then type the above creds. 

* After successful login we can put a php rev shell on the server. You can refer ( https://github.com/pentestmonkey/php-reverse-shell ) for web shell. Change your IP and port accordingly. Now type ( ' *put php-reverse-shel.php* ' ) in the cadaver shell and start your nc simultaneously on the port described in reverse shell.

* After successfully getting the shell, we see that we have two users in /home directory - 'merlin' and 'wampp'. Go to merlin directory to see the 'user.txt' file.

1. user.txt<br>
Answer : 449b40fe93f78a938523b7**********

* Now for root, type 'sudo -l' to see for list of user privileges. We find that we can run '/bin/cat'. Now for root.txt type ( ' *sudo /bin/cat /root/root.txt* ' ).

2. root.txt <br>
Answer : 101101ddc16b0cdf65ba0b**********

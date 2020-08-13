# TryHackMe Bolt
**A hero is unleashed**

## Task-2 Hack your way into the machine!

* Started enumeration by using nmap and got three ports open - 22,80,8000. Port 80 was a defaut apache webpage but on port 8000 was 'Bolt CMS'. On moving to the site we can clearly see username as 'bolt' and its password as 'boltadmin123'. As port 22 was open so I thought of doing ssh login but was not successful. So after doing some search we can find a login page at 'http://ip/bolt' and the above creds make us log in successfully. After logging in we can see the CMS version below.

1. What port number has a web server with a CMS running?<br>
Answer : 8000

2. What is the username we can find in the CMS?<br>
Answer : bolt

3. What is the password we can find for the username?<br>
Answer : boltadmin123

4. What version of the CMS is installed on the server? (Ex: Name 1.1.1)<br>
Answer : Bolt 3.7.1

* After that search on google for 'bolt cms exploit' and you will find a authenticated RCE for its previous version. Now start your metasploit and search for 'bolt cms'. You will find an exploit named 'unix/webapp/bolt_authenticated_rce'. Select this module and set the options accordingly. After running the exploit you will be root. Now go to /home for flag.txt . 

5. There's an exploit for a previous version of this CMS, which allows authenticated RCE. Find it on Exploit DB. What's its EDB-ID?<br>
Answer : 48296

6. Metasploit recently added an exploit module for this vulnerability. What's the full path for this exploit? (Ex: exploit/....)<br>
Answer : /exploit/unix/webapp/bolt_authenticated_rce

7. Look for flag.txt inside the machine.<br>
Answer: THM{wh0_d035nt_l0ve5_b0l7_r****?}

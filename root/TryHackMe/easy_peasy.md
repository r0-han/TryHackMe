# TryHackMe Easy Peasy
**Practice using tools such as Nmap and GoBuster to locate a hidden directory to get initial access to a vulnerable machine. Then escalate your privileges through a vulnerable cronjob.**

**According to me this machine is a collection of enumeration, steganography and privesc. After lot of searching I used https://md5hashing.net/hash/ for cracking hashes.**

## Task-1 Enumeration through Nmap

* Ran this command for nmap enumeration - *nmap -A -v -T4 -p- ip*

1. How many ports are open?<br>
Answer : 3

2. What is the version of nginx?<br>
Answer : 1.16.1

3. What is running on the highest port?<br>
Answer : Apache

## Task-2 Compromising the machine

* For further enumeration ran gobuster for sub directory fizzing - *gobuster dir -u http://ip -w medium.txt -t 100*. From this got directory named -'hidden'. Again ran gobuster on this directory and got another directory named - 'whatever'.

* Opening that directory and viewing its page source gave us a base64 encoded string. Decode ot to get first flag.

1. Using GoBuster, find flag 1.<br>
Answer : flag{f1rs7_****}

* On Apache highest port viewing /robots.txt file we found a hash at 'User-Agent' heading. After decoding this it simply gave us flag2.

2. Further enumerate the machine, what is flag 2?<br>
Answer : flag{1m_s3c0nd****}

* Again ran gobuster for the whatever directory but didn't find anything. Then I switched to Apache port(highest port). Found a user agent in that and then intercepted the request with burp and then change the 'User-Agent' and then forward it. Then view its page source and you will find flag 3 there. 

3. Locate flag 3.<br>
Answer : flag{9fdafbd64c47471a8f54cd**********}

* Again ran gobuster for the /whatever directory but didn't find anything. Then I switched to Apache port(highest port). It was just apache webpage but on viewing its source page there was a base62 encoded string. After decoding, gave the hidden directory.

4. What is the hidden directory?<br>
Answer : /n0th1ng3ls3m***** 

* Moving forward to the hidden directory we saw a image with binary written on it. Then I went for the pages source and got another hash. As the hint suggests this is a 'GHOST' hash. After decoding it gave us a password. So I downloaded the image and tried steghide on that binary image. And we get credentials for a user named 'boring'.

5. Using the wordlist that provided to you in this task crack the hash. What is the password?<br>
Answer : mypassword**********

6. What is the password to login to the machine via SSH?<br>
Answer : iconvertedmypassword********

* After logging into the ssh on port 6498 we are logged in as 'boring' and can see the user flag. But as the hint says it is ROT13 encoded . After decoding it gave the user flag.

7. What is the user flag?<br>
Answer : flag{n0wits33ms******}

* For privesc I tried all the suid perms and sudo perms but couldn't find anything. Then I searched for cronjobs using '*cat /etc/crontab*' and we got a cronjob running named - '.mysecretcronjob.sh'. After viewing its content we can edit it to gain a nc reverse shell.Just edit the file in nano editor by putting your reverse shell with IP and port to listen. Now listen to the above port number and after some time you will get your flag. Now go to root directory and type 'ls -la'. You will see your root flag.

8. What is the root flag?<br>
Answer : flag{63a9f0ea7bb*********************}

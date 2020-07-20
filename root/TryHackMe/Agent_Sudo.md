# TryHackMe Agent Sudo
**You found a secret server located under the deep sea. Your task is to hack inside the server and reveal the truth.**

## Task-1 Enumerate

* Starting enumeration by nmap scan using command (*nmap -sV -A ip*) will show 3 ports open - 'ssh', 'ftp', 'http'. Also on going to the ip in browser it shows a message from 'Agent R'. Also it give us hint to change user-agent to access the site. So I used 'curl' to try different user-agents. I tried english alphabets 'A','B'... as the message is from 'R'.

* I used command 'curl -H http://<IP> "User-Agent: A" -L' but was unsuccessful so i moved to B and got the same message. On trying 'C', 'curl -H http://<IP> "User-Agent: C" -L' and got different message for 'chris'. So this is the agent name.Now on above context answers to below questions can be answered.


1. How many open ports?<br>
Answer : 3 

2. How you redirect yourself to a secret page?<br>
Answer : user-agent

3. What is the agent name?<br>
Answer : chris

## Task-3 Hash cracking and brute-force

* We saw in nmap scan that port 21 that is 'ftp' is open. So 'chris' must be the username for ftp server. To crack password I used hydra . The command for the same was (*hydra -l chris -P rockyou.txt ftp://<IP>*). After some time I got the password 'crystal' and logged in to the ftp server. 

* To log in ftp server just type 'ftp ip' and it will prompt you for a username and then password and we're successfully logged in. Type 'ls -la' to see item list in ftp server. We see 3 files. To get files in local machine just type 'get filename'. After successfully getting the 3 files exit the ftp server and now analyse these 3 files.

* First I saw the content of .txt file and inferred that it is a steganography phase. First I tried to see the content of .txt file but it was empty. Then I tried to extract data from .jpg file but it was password protected. So i used binwalk on png file to gather the hidden files using command 'binwalk -e file.png'. In that I found a zip password proteted file. To crack its password I used zip2john using command 'zip2john file.zip > hash.txt'. You should know how to use john to crack these kinds of files as it is very useful in CTFs. Now crack the hash using 'john hash.txt' and then type 'john --show hash.txt'. You will have your password as : 'alien'. 

* Now unzip the file using this password and now you can see the content of 'To_AgentR.txt' file. It gave a password in encrypted text. After analysing it was base64 encoded. So I typed 'echo "text" | base64 -d' in my terminal and got the password for the jpg file as 'Area51'.

* Now I used steghide to extract data from .jpg file using command 'steghide extract -sf file.jpg' and enter the password. We got a 'message.txt' file which on opening gave us a username as 'james' and password - 'hackerrules!'. These are the creds for our ssh shell. Now you can answer the below questions.  

1. FTP password<br>
Answer : crystal

2. Zip file password<br>
Answer : alien

3. steg password<br>
Answer : Area51

4. Who is the other agent (in full name)?<br>
Answer : james

5. SSH password<br>
Answer : hackerrules!

## Task-4 Capture the user flag

* Now login into ssh using above creds. Type 'ls -la' to see for items and we see a 'user_flag.txt' file. See its content as it is our user flag. Also there is a .jpg image in the james directory. To reverse search this image we have to get it on your local machine. On another terminal in your machine type 'scp james@room_ip:/home/james/file_name.jpg'. scp is used to transfer files remotely on a server. It will ask for a password which is same as of ssh password which we used above to login. Now we will have the file in our system.  Now reverse search this on google images and you will find your answer.

1. What is the user flag?<br>
Answer : b03d975e8c92********************

2. What is the incident of the photo called?<br>
Answer : Roswell alien *******

## Task-5 Privilege escalation

* Now we have to privesc it to get the root privileges. Just type 'sudo -l' in the james terminal. It will show that 'User james may run the following commands on agent-sudo:(ALL, !root) /bin/bash'. Now I searched for this on google and got the exploit with its CVE. This is where you can refer to exploit https://www.exploit-db.com/exploits/47502. So i typed the exploit which was - 'sudo -u#-1 /bin/bash'. And we have root privileges now. Now move to root directory and see its content. You will see a root.txt . See its content and answer for the questions is below : 

1. CVE number for the escalation (Format: CVE-xxxx-xxxx)  <br>
Answer : CVE-2019-14287

2. What is the root flag?<br>
Answer : b53a02f55b57********************

3. (Bonus) Who is Agent R?<br>
Answer : Deskel

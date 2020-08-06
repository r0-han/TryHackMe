# TryHackMe Bounty Hacker
**You talked a big game about being the most elite hacker in the solar system. Prove it and claim your right to the status of Elite Bounty Hacker!**

## Task-1 Living up to the title.

* After doing nmap scan , port 21 - ftp was open. So I tried anonymous login and was succcessful. After that I typed 'ls' to see the content in ftp shell. We got two txt files. Type 'get file_name' to get the file in your local machine. Type 'cat file_name' to see the file content. 

3. Who wrote the task list? <br>
Answer : lin

4. What service can you bruteforce with the text file found?<br>
Answer : ssh

5. What is the users password? <br>
Answer : RedDr4gonSynd1cat3 (*hydra -l lin -P locks.txt ssh://ip*)

* After getting the creds we can login to ssh. Type '*ssh lin@ip*' and then password. We are successfully logged in.

6. user.txt<br>
Answer : THM{CR1M3_*********}

* For sudo privileges type 'sudo -l' and it will show file which user can run. Now go to https://gtfobins.github.io/ and find the file here and then run its sudo command.

7. root.txt<br>
Answer : THM{80UN7Y_******} 
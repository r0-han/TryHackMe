# TryHackMe Lian_Yu
**A beginner level security challenge**

## Task-1 Find the Flags

* I first tried to find hidden directories through this command *gobuster dir -u http://ip -w directory-list-2.3-medium.txt -t 100* and found one 'island'. On viewing the page source i found the code word : 'vigilante'. I know this is a username for something but don't know what it was exactly. So after viewing hint for #2 I had to change my gobuster directory. I just wrote a simple python command to generate numbers between 1000-9999. Command is 'for i in range(1000, 10000); print i' and used this list for gobuster. Final command was *gobuster dir -u http://ip/island -w num.txt -t 100* . So I found answer to some of the questions below.

2. What is the Web Directory you found?<br>
Answer : 2100 

3. what is the file name you found?<br>
Answer : green_arrow.ticket (* On viewing page source i found this line 'you can avail your .ticket here but how'. So I again used gobuster, now with a file extension. The command is *gobuster dir -u http://ip/island/2100 -w directory-list-2.3-medium.txt -x .ticket* and found the answer.) 

* On viewing the page source i found a base encoded string and we were correct as per the given hint. I used cyberchef to decode this and found that this was a base58 encoding.

4. what is the FTP Password?<br>
Answer : !#th3****

* So we got ftp password, so i remembered that we have found a key in above step and thought this was the username. So i logged in ftp using command *ftp ip* and type the username 'vigilante' and the password in #4 and i was successful. So i types 'ls' and got three image files. I typed 'get file_name' to get the file in my local user. Also there was a hidden file named 'other_user' which showed 'slade'. After this I opened the files and there were nothing special. But one file named Leave_me_alone.png were distorted . So I corrected its headers (*you can see online how to correct ong headers*) and got something with 'password' in it. So i thought this could be something. Then I tried steghide on 'aa.jpg' and it asked for a password. So I typed the password gained in above step and was given a zip file and 'shado' file which is the answer to next question.

5. What is the file name with SSH password?<br>
Answer : sha**

* On viewing the content of above file we got a text 'M3tahuman'. It was clear that this was password for SSH. I logged in SSH thru command (*ssh slade@ip*) and typed the above password and we have gained the shell. Now 'cat' user.txt for the next question.

6. user.txt<br>
Answer : THM{P30P7E_K33P_53CRET5__*********_*****}

* After this I typed 'sudo -l' to see for root privileges and found the command that 'slade' can run. This command was '/usr/bin/pkexec'. So i ran 'pkexec' which was ELF file. After viewing its 'man' command it was clear that we can run '/bin/bash' with sudo. So I typed the command *sudo /usr/bin/pkexec /bin/bash* and got the root access. So i 'cat' the flag.

7. root.txt<br>
Answer : THM{MY_W0RD_I5_MY_B0ND_**_I_ACC3PT_****_CONTRACT_****_IT_WILL_**_COMPL3TED_OR_****_BE_D34D}
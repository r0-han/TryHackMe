# TryHackMe Blue
**Deploy & hack into a Windows machine, leveraging common misconfigurations issues.**

## Task-1 Recon

* I just did nmap scan (*nmap -A -sV ip*) and got the answers to the below questions. 

2. How many ports are open with a port number under 1000?<br>
Answer : 3 

3. What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)<br>
Answer : ms17-010

## Task-2 Gain Access

* After finding the CVE the next step was to fire up the metasploit and search for this cve. Command for the same is (*search ms17-010*). You will find a exploit having 'eternallue' in the end. Just type 'use exploit_name'. You will have that shell open.

2. Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)<br>
Answer : windows/smb/ms17_010_eternalblue

* Now type 'show options' in the metasploit shell and it will show some options regarding exploit. There is a value called 'RHOSTS' in front of which it is written 'yes'. It means it is mandatory to fill this field. Now RHOST is the victim's IP. Type command 'set RHOSTS ip' and click enter. Now type 'exploit'.

3. Show options and set the one required value. What is the name of this value? (All caps for submission)<br>
Answer : RHOSTS

## Task-3 Escalate

1. If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected) <br>
Answer : post/multi/manage/shell_to_meterpreter

* Type command 'use post/multi/manage/shell_to_meterpreter'. Now type sessions to list the current running sessions. Now follow the steps given in description.

2. Select this (use MODULE_PATH). Show options, what option are we required to change? (All caps for answer)<br>
Answer : SESSIONS

## Task-4 Cracking

* Type hashdump and you will see the listed users. Just copy the last hash of 'Jon' user. I used https://crackstation.net/ to crack hash.

1. Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? <br>
Answer : Jon

2. Copy this password hash to a file and research how to crack it. What is the cracked password?<br>
Answer : alqfna22

## Task-5 Find flags!

* Type "search -f 'flag* .txt'" in the meterpreter shell. It will show the location of all the flags.

1. Flag1? (Only submit the flag contents {CONTENTS}) <br>
Answer : access_the_*******

2. Flag2? Errata: Windows really doesn't like the location of this flag and can occasionally delete it. It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen.<br>
Answer : sam_database_elevated_******

3. flag3?<br>
Answer : admin_documents_can_**_********
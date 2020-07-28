# TryHackMe Injection

**Walkthrough of OS Command Injection. Demonstrate OS Command Injection and explain how to prevent it on your servers**

## Task-3 Blind Command Injection

1. Ping the box with 10 packets.  What is this command (without IP address)?<br>
Answer : & ping -c 10

2. Redirect the box's Linux Kernel Version to a file on the web server.  What is the Linux Kernel Version?<br>
Answer : 4.15.0-101 (*uname -r*)

3. Enter "root" into the input and review the alert.  What type of alert do you get?<br>
Answer : success

4. Enter "www-data" into the input and review the alert.  What type of alert do you get?<br>
Answer : success

5. Enter your name into the input and review the alert.  What type of alert do you get?<br>
Answer : error

## Task-4 Active Command Injection

1. What strange text file is in the website root directory?<br>
Answer : drpepper.txt

2. How many non-root/non-service/non-daemon users are there?<br>
Answer : 0 (*cat /etc/passwd*)

3. What user is this app running as?<br>
Answer : www-data (*whoami*)

4. What is the user's shell set as?<br>
Answer : /usr/bin/nologin (*cat /etc/passwd*)

5. What version of Ubuntu is running?<br>
Answer : 18.04.4 ('lsb_release -a')

6. Print out the MOTD. What favorite beverage is shown?<br>
Answer : Dr Pepper (*cat /etc/update-motd.d/00-header*)

## Task-5 Get The Flag!

1. Get the flag!<br>
Answer : 65fa0513******************** (*find / -name 'flag.txt' 2>/dev/null*)
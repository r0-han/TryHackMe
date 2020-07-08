# TryHackMe Mr Robot Ctf
** Based on the Mr. Robot show, can you root this box? **

## Task-1 Connect to our network
* Connect and deploy the machine

## Task-2 Hack the machine
* Before going further you should make a practice to do some recon like nmap and gobuster on the ip  as it will be helpful later

1. What is key 1?<br>
Answer : 073403c************************* (*just follow the hint given in the room. Hint is robots.txt file*)

* So after performing gobuster on this ip (*gobuster dir -u http://ip -w directory-list-2.3-medium.txt*) I found many directories some of them giving 200 response code.I tried each one of them and got something. But in the page 'license' I found something interesting. The page contains some text but if you scroll down you will see something interesting. A base64 encoded string. I used cyberchef (*most popular tool among ctf players*) to decode this and got the username:some_random_text. From my gobuster i also found one directory named wp-login which was just a login page. I thought credentials I got from above decoding can be applied there and i was right. We have successfully logged in. 
* You can also use hydra to decode username and password from the 'fsociety.dic' file but it will be very time consuming. 

* After that we have to find a way to gain root access to the server. Luckily we found one appearence editor column. Click on 404 which is a php template. Now we have to create a backdoor. Honestly I didn't know how to use metasploit so i referred to this link https://medium.com/@DRX_Sicher/writeup-mr-robot-ctf-1baf5f20e6f4. In this whole privesc is explained in detail.

* I'll tell in short what it is about. First we create a php reverse shell to gain access using msfvenom and them msfconsole to gain root access. After this we will navigate to /home/robot in shell to find answer for 2 question. But the permission is denied to look content of text file. So we will use crackstation to crack MD5 and then try to switch to robot directory using python command.Then we can look the content of the file.<br>
For the last part we have to play with nmap as nmap --interactive mode. After that we will gain its shell to navigate to root and get the answer for last question.

2. What is key 2?<br>
Answer : 822c7***************************

3. What is key 3?<br>
Answer : 04787***************************

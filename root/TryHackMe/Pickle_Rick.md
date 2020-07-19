# TryHackMe Pickle Rick
**A Rick and Morty CTF. Help turn Rick back into a human!**

* After deploying the machine I went to ip in my browswer and it's heading says Rick is sup4r cool. There was nothing special on the page so I moved to page source and found username : 'R1ckRul3s' there. It will be helpful to us in the future. Also I searched for robots.txt and got 'Wubbalubbadubdub'.

* Also I ran nmap and gobuster on the ip. nmap showed ssh service and gobuster showed just one directory 'assets'. I searched assets and it was just some files and images for the site. I thought there should me more than that. Then I remembered , on the room it's written - 'ctf', 'dirbuster', 'linux'. So I thought of of doing dirbuster and got some interesting pages. I found 'login.php' and 'portal.php'. 

* So I moved to login.php and it was a login portal. Remember we got a username in the beginning. So I thought for the password and saw the result of robots.txt. I tried those creds and I successful. After that it was a basic command pannel.

* so I typed 'ls -la' and we see a file named 'Sup3rS3cretPickl3Ingred.txt'. So I tried to open it with cat but was unsuccessful. So I typed 'less Sup3rS3cretPickl3Ingred.txt' and got the answer for #1 question.

1. What is the first ingredient Rick needs?<br>
Answer : mr. meeseek ****

* There was also one file named 'clue.txt'. so I typed 'less clue.txt' and got this - 'Look around the file system for the other ingredient.'. It was pretty clear that this challenge was purely based on linux.

* So I tried to navigate through directories thru 'cd' but was unsuccessful. So I typed 'ls -la /home' and got two users - 'rick' and 'ubuntu'.Then I typed 'ls -la /home/rick' and got the second ingredient. See its content using "less 'second ingredients'". 

2. Whats the second ingredient Rick needs?<br>
Answer : 1 jerry ****

* For the final question I searched for root privileges using 'sudo -l' and found that we can do anything with sudo command. SO I typed 'sudo ls -la /root' and got a file named '3rd.txt'. I typed 'sudo less /root/3rd.txt' and got the answer to last question.

3. Whats the final ingredient Rick needs?<br>
Answer : fleeb *****
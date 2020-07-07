# TryHackMe Vulnversity
** Learn about active recon, web app attacks and privilege escalation. **

## Task-1 Deploy the machine
* Deploy and continue

## Task-2 Reconnaissance

1. Scan this box: nmap -sV <machines ip><br>
Answer : Read and submit

2. Scan the box, how many ports are open?<br>
Answer : 6 (*nmap <IP>*)

3. Scan the box, how many ports are open?<br>
Answer : 3.5.12 (*nmap -sV 10.10.208.89 -p port_on_which_squid_proxy_is_running*)

4. How many ports will nmap scan if the flag -p-400 was used?<br>
Answer : 400

5. Using the nmap flag -n what will it not resolve?<br>
Answer : DNS (*nmap -h*) 

6. What is the most likely operating system this machine is running?<br>
Answer : ubuntu (*i tried nmap -O <IP>, as given in hint, but could not get anything. So i tried nmap -sV <IP> and got the answer*)

7. What port is the web server running on?<br>
Answer : ip_of_http_server from your nmap scan

8. Its important to ensure you are always doing your reconnaissance thoroughly before progressing. Knowing all open services (which can all be points of exploitation) is very important, don't forget that ports on a higher range might be open so always scan ports after 1000 (even if you leave scanning in the background)<br>
Answer : Read and submit

## Task-3 Locating directories using GoBuster

1. Lets first start of by scanning the website to find any hidden directories. To do this, we're going to use GoBuster.<br>
Answer : Read and submit

2. What is the directory that has an upload form page?<br>
Answer : /internal/ (*gobuster dir -u http://<IP>:3333 -w wordlist_locations*)

## Task-4 Compromise the webserver

1. Try upload a few file types to the server, what common extension seems to be blocked?<br>
Answer : .php (*i just bruteforced it as wappalyzer was not working*)

2. To identify which extensions are not blocked, we're going to fuzz the upload form.<br>
Answer : Read and submit

3. We're going to use Intruder (used for automating customised attacks).Run this attack, what extension is allowed?<br>
Answer : .phtml (*by using sniper attack  given in the description from the file web-extensions.txt which has common web extensions and can be easily found on google. After the sniper attack is completed you will see that one row will have different length than the others which  is our answer*)

4. Now we know what extension we can use for our payload we can progress.<br>
Answer : Read carefully and continue

* To gain reverse shell first download the php code from the given link in description and . Now open it in any editor and change the ip address to your tunnel address . You can see your tunnel address by typing (*ifconfig*) . Now save the file as .phtml as it is the only extension acceptable. Now navigate to the page where upload option is there. Upload this reverse shell as .phtml and navigate to the link given in description. You will see your shell uploaded there. Now connect to the reverse shell using netcat  by following command (*nc -lnvp port_no_in_reverse_shell*). Now click on the file in the link and you will see some activity on your terminial. You have gained access to reverse shell. Navigate to home command in the shell and there you will see your answer to next question

5. What is the name of the user who manages the webserver?<br>
Answer : bill

6. What is the user flag?<br>
Answer : 8bd7992************************* (*cat /bill/user.txt*)

## Task-5 Privilege Escalation

1. On the system, search for all SUID files. What file stands out?<br>
Answer : /bin/systemctl (*using the hint*)

2. Its challenge time! We have guided you through this far, are you able to exploit this system further to escalate your privileges and get the final answer?Become root and get the last flag (/root/root.txt)<br>
Answer : a58ff************************* (*honestly i was not able to do this and eventually had to look up for a solution on (https://unicornsec.com/home/tryhackme-vulnversity) . This guy have explained this privesc in detailed manner.*)
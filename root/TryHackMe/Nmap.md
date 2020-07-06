# TryHackMe Nmap
**Part of the Red Primer series, intro to scanning.**

## Task-1 Deploy!
* Just deploy the machine and continue

## Task-2 Nmap Quiz
* man pages along with grep are useful

1. First, how do you access the help menu?<br>
Answer : -h

2. Often referred to as a stealth scan, what is the first switch listed for a 'Syn Scan'?<br>
Answer : -sS

3. Not quite as useful but how about a 'UDP Scan'?<br>
Answer : -sU

4. What about operating system detection?<br>
Answer : -O

5. How about service version detection? <br>
Answer : -sV

6. Most people like to see some output to know that their scan is actually doing things, what is the verbosity flag?<br>
Answer : -v

7. What about 'very verbose'? (A personal favorite)<br>
Answer : -vv

8. Sometimes saving output in a common document format can be really handy for reporting, how do we save output in xml format?<br>
Answer : -oX

9. Aggressive scans can be nice when other scans just aren't getting the output that you want and you really don't care how 'loud' you are, what is the switch for enabling this?<br>
Answer : -A

10. How do I set the timing to the max level, sometimes called 'Insane'?<br>
Answer : -T5

11. What about if I want to scan a specific port?<br>
Answer : -p

12. How about if I want to scan every port?
Answer : -p-

13. What if I want to enable using a script from the nmap scripting engine? For this, just include the first part of the switch without the specification of what script to run.<br>
Answer : --script

14. What if I want to run all scripts out of the vulnerability category? <br>
Answer : --script vuln

15. What switch should I include if I don't want to ping the host?<br>
Answer : -Pn

## Task-3 Nmap Scanning
* Performing basic nmap scan

1. Let's go ahead and start with the basics and perform a syn scan on the box provided. What will this command be without the host IP address?<br>
Answer : nmap -sS

2. After scanning this, how many ports do we find open under 1000?<br>
Answer : 2 (*nmap <ip> -p-1000*)

3. What communication protocol is given for these ports following the port number?<br>
Answer : tcp

4. Perform a service version detection scan, what is the version of the software running on port 22?<br>
Answer : 6.6.1p1 (*nmap <ip> -sV -p 22 | grep tcp*)

5. Perform an aggressive scan, what flag isn't set under the results for port 80?<br>
Answer : httponly (*nmap <ip> -A -p 80 | grep h*)

6. Perform a script scan of vulnerabilities associated with this box, what denial of service (DOS) attack is this box susceptible to? Answer with the name for the vulnerability that is given as the section title in the scan output. A vuln scan can take a while to complete. In case you get stuck, the answer for this question has been provided in the hint, however, it's good to still run this scan and get used to using it as it can be invaluable. <br>
Answer : http-slowloris-check
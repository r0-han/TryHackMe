# Willow 

**What lies under the Willow Tree?**

## Task-1 Flags

### Enumeration

* Starting enumeration using nmap gave us 4 open ports - 22, 80, 111, 2049.

#### Enumeration on port 2049

* This port shows *nfs* service is open. So we can try to view the directories to mount in order to access some files. Command for the same is ***showmount -e ip***.<br>

* We see that we can mount directory */var/failsafe*. Command for the same is ***mount ip/var/failsafe /mnt/Willow*** . So now if we head over to */mnt/Willow* we can see *rsa_keys* file.

* In that we are given *Public Key Pair: (23, 37627) and Private Key Pair: (61527, 37627)* . So in RSA these are given as *Public Key: (e,n) and Private Key: (d,n)*. We will leave them here at this time.

#### Enumeration on port 80 

* If we see this page, the values there are hex and we can decrypt these on [cyberchef](https://gchq.github.io/CyberChef/). After decoding these values we get another message : *Hey Willow, here's your SSH Private key -- you know where the decryption key is!* along with some values.

* Now we can get our SSH key as we have the ciphertext and the values which we got from *rsa_keys* file. I used this [online rsa calculator](https://www.cs.drexel.edu/~jpopyack/Courses/CSP/Fa17/notes/10.1_Cryptography/RSA_Express_EncryptDecrypt_v2.html) to get the keys. Just put the required values and you will get the SSH key. Save this key in your local machine.

* As this is a ssh key we can use *ssh2john.py* to decrypt it. For this use the command ***python3 ssh2john.py above_key > keys.txt*** and then again use john to crack it using command ***john --wordlist=rockyou.txt keys.txt***. After this you will get the password for rsa keys.

* Now we can log into user *willow* using the command ***ssh -i above_key willow@ip*** and the password obtained from above step. 

### User Flag

* After logging in we can see a *user.jpg* file which we have to transfer on our local machine to view it. I used scp to transfer this ***scp -i above_key ip:user.jpg***. After this you can submit the user flag.

1. User flag 
* THM{beneath_the_weeping_//////_////}

### Root Flag

* Now for the privilege escalation type ***sudo -l*** which gave us *(ALL : ALL) NOPASSWD: /bin/mount /dev/*.

* So in */dev* directory we see a file *hidden_//////*. So we can mount this in the willow user itself. In the */mnt* directory we see another directory *creds* in which we can mount our file. For this use ***sudo /bin/mount /dev/hidden_******/mnt/creds***.

* In this we can see a file *creds.txt* and we got the password for user. SO we can simply switch to root using *su root* and password obtained from *creds.txt*.

* So we can see a *root.txt* file. On viewing its content it gave *This would be too easy, don't you think? I actually gave you the root flag some time ago.
You've got my password now -- go find your flag!*. It gives us some hint that we have got the flag before. So I searched for some time and view the *user.jpg* file again. We can try *steghide* using command ***steghide extract -sf user.jpg*** on this as we have root and willow password. So trying it with root password gave us the flag.

2. Root flag
* THM{find_a_red_////_//_the_g////}

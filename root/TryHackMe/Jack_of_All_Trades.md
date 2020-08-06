# TryHackMe Jack-of-All-Trades
**Boot-to-root originally designed for Securi-Tay 2020**

## Task-1 Flags

* On enumeration we saw that port - 22, 80 were interchanged. So if we try to access these pages on these ports we see an error which you can resolve by looking at https://blog.christoffer.online/2012-02-20-how-to-remove-firefoxs-this-address-is-restricted/. 

* After doing this we can successfully see the home page saying 'Welcome to Jack-of-all-trades!'. You can see some pictures and text on the homepage. So I then went to look something on its page source and found a base64 encoded string. After decoding this on cyberchef it gave us a username and password as 'Johny Graves:u?WtKSraq'. 

* Also you can see a /recovery.php above the string mentioned above. So after viewing this in the browser was a recovery page having login form. But if you will see its page source you will find an encoded string. So go to cyberchef and try to decode it with base32. After decoding it again give us hex values. Decoding that again gave us ROT13 cipher. If you play CTF regularly then this will be a piece of cake for you.

* After the final decoding you will get a url shortened link redirecting to stegosauria wiki. This gives us a hint that there is some steganography used. So I downloaded the dinosaur image from the homepage and tried to find something on it.

* So I tried steghide on this and entered the password which we got from above result. We got a text file saying that 'we are on the right path, but wrong image'. So I downloaded all the files from the webpage and tried steghide on all of them. Apparently it worked on 'header.jpg' file and we got a file named 'cms.creds' which have correct creds.

* So login to the recovery page and you will be shown with this - 'GET me a 'cmd' and I'll run it for you Future-Jack.' Means we can execute code with 'cmd' as a parameter.

* Type '?cmd=id'after the index.php and you will see yourself as 'www-data'. So I tried to view users using command 'ls -la /home' and found a directory jack and a password file.Type 'cat /home/password_file' to see its content. Save these passwords in a file in your local machine to perform hydra.

* Now we can try hydra as we have a user named 'jack'. Type 'hydra -l jack -P above_pass_list ssh://ip:80' and we got one password thru which we can login into ssh. Now type the command '*ssh jack@ip -p 80*'(as ports were changed). We are successfully logged in. 

* Type 'ls' and you will see a user.jpg file. Get this file into your local machine using command '*scsp -P 80 jack@ip:user.jpg .*'. Now view this file and it contains your user flag.

1. User Flag<br>
Answer : securi-tay2020__p3ngu1n-hunt3r-**************}

* For privesc type 'sudo -l' but we cannot as jack is not in sudoers. Now we will search for suid . Type '*find / -perm -u=s -type f 2>/dev/null*' and we will get a list of suid. Now search on gtfo bins for proper suid from above result. You will find one for 'strings'. Run the command as given in gtfobins and you will gain user shell. Now type ./strings /root/root.txt

2. Root Flag<br>
Answer : securi-tay2020_{6f125d32f38fb8ff9e720d**********}

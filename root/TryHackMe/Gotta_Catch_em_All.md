# TryHackMe Gotta Catch'em All
**This room is based on the original Pokemon series. Can you obtain all the Pokemon in this room?**

## Task-1 Can You Catch'em All?

* Started enumeration by doing nmap scan which gave port - 22,80 open. So starting with port 80 we saw a sample apache2 webpage. But if you will look its pages source it will show a different html tags above the comment 'Check console for extra surprise'. They seem credentails for port -22(ssh). Trying them and we are logged in successfully.

* After logging in we can see that we are 'pokemon' user. Now type 'ls -lAh * '. We can see a file named 'P0kEmOn.zip' and a directory named 'gotta'. First we will get the file 'P0kEmOn.zip' file in our terminal. You can use any method - curl, scp, wget. After getting the file unzip it. It will give a directory in which our we see hex values. Decode them to get first flag.

1. Find the Grass-Type Pokemon <br>
Answer : PoK****{Bulb*****}

* Now we will see the directory 'Gotta' which we got from above result. In that there are subdirectories which lead to a .cplusplus file which is only a ASCII text file. After seeing that we can see the user 'ash' creds. Log into 'ash' using these creds.

* After that I tried to go into ash directory but was denied. So I thought of escalating it using 'sudo -l' and we see that we can just type 'sudo su' to be user. After doing this we are 'root'.

* After that I tried to go into ash directory but couldn't find anything. So I started searching for files and ended up seeing the content of '/var/www/html' which give us a cipher. This is ROT-14 cipher. Decode it to get the flag.

2. Find the Water-Type Pokemon<br>
Answer : Squirtle_*****{Squi****}

* For fire type pokemon I searched everywhere but couldn't find anything. Then I searched for it using 'find / -type f -name '*fire*.txt' ' and got the file. After opening this file it gave us a base64 string which on decoding gave us our flag.

3. Find the Fire-Type Pokemon<br>
Answer : P0k****{Char******}

* In the home directory we saw another file named 'roots-pokemon.txt'. Now we can see it as we are root. This is answer to below question.

4. Find the Fire-Type Pokemon<br>
Answer : Pik****!
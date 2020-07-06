# Learn Linux

**This room will give you some idea about basics of linux**

## Task-1 to Task-5 read and submit

## Task -6 Section 2: Running Commands - Manual Pages and Flags
* using man pages

1. How would you output hello without a newline.<br>
Answer : echo -n hello 

## Task-7 Section 3: Basic File Operations - ls 
* using man pages

1. What flag outputs all entries.<br>
Answer : -a 

2. What flag outputs things in a "long list" format<br>
Answer : -l

## Task-8 Section 3: Basic File Operations - cat
* using man pages

1. What flag numbers all output lines?<br>
Answer : -n

## Task-9 * submit and continue 

## Task-10 Section 3: Basic File Operations - Running A Binary
* using man pages

1. How would you run a binary called hello using the directory shortcut . ?<br>
Answer : ./hello

2. How would you run a binary called hello in your home directory using the shortcut ~ ?<br>
Answer : ~ /hello

3. How would you run a binary called hello in the previous directory using the shortcut .. ?<br>
Answer :  ../hello

## Task-11  Binary - Shiba1 
* I recommend to do it yourself first

1. What's the password for shiba2<br>
Answer : ping**** (by running binary : ./shiba1)

## Task-12 su

1. How do you specify which shell is used when you login? <br>
Answer : -s

## Task-13 * Read and submit 

## Task-14 Section 4: Linux Operators: '>' 
<br>
Answer : echo twenty > test

## Task-15 to Task-17 Read and submit

## Task-18 Section 4: Linux Operators : "$" 

1.How would you set nootnoot equal to 1111<br>
Answer : export nootnoot=1111

2. What is the value of the home environment variable<br>
Answer : /home/shiba2

## Task-19 to Task-20 read and submit

## Task-21 Binary - shiba2 
* set the test1234 env variable to $USER by export test1234=$USER and then run ./shiba3<br>
Answer : happy******ises

## Task-22 to Task-23 read and submit 

## Task-24 Section 5: Advanced File Operations : chmod
* Just answer from above table

1. What permissions mean the user can read the file, the group can read and write to the file, and no one else can read, write or execute the file?<br>
Answer : 460

2. What permissions mean the user can read, write, and execute the file, the group can read, write, and execute the file, and everyone else can read, write, and execute the file.<br>
Answer : 777

## Task-25 Section 5: Advanced File Operations - chown

1. How would you change the owner of file to paradox<br>
Answer : chown paradox file

2. What about the owner and the group of file to paradox    <br>
Answer : chown paradox:paradox file 

3. What flag allows you to operate on every file in the directory at once?    <br>
Answer : -R 

## Task-26 Section 5: Advanced File Operations - rm 
* using man pages

1. What flag deletes every file in a directory<br>
Answer : -r

2. How do you suppress all warning prompts<br>
Answer : -f

## Task-27 Section 5: Advanced File Operations - mv

1. How would you move file to /tmp<br>
Answer : mv file /tmp

## Task-28 read and submit

## Task-29 Section 5: Advanced file Operations - cd && mkdir

1.  Using relative paths, how would you cd to your home directory. <br>
Answer : cd ~

2. Using absolute paths how would you make a directory called test in /tmp<br>
Answer : mkdir /tmp/tst

## Task-30 Section 5: Advanced File Operations ln
* Important regarding linux sys admin

1. How would I link /home/test/testfile to /tmp/test<br>
Answer : ln /home/test/testfile /tmp/test

## Task-31 Section 5 - Advanced File Operations: find

1. How do you find files that have specific permissions?<br>
Answer : -perm

2. How would you find all the files in /home<br>
Answer : find /home

3. How would you find all the files owned by paradox on the whole system<br>
Answer : find / -user paradox

## Task-32 Section 5: Advanced File Operations - grep
* One of the most usefull command

1. What flag lists line numbers for every string found?<br>
Answer : -n

2. How would I search for the string boop in the file aaaa in the directory /tmp<br>
Answer : grep boop /tmp/aaaa

## Task-33 Binary - Shiba3 
** This was interesting challenge and tough one wrt the previous two binaries **
* You have to find if there is a file called shiba4 and if exists find its location. Command for this - find / -name shiba4 2>/dev/null. You will find a secret directory  having a file shiba4
* Then check for test directory in home . Command for this - mkdir ~ /test. You will get an error that directory already exists hence no need to do anything.
* Create a file test1234 in test directory. Command for this - touch ~ /test/test1234. Now run the binary

1. What is shiba4's password<br>
Answer : test****

## Task-34 read and submit

## Task-35 Section 6: Miscellaneous : sudo

1. How do you specify which user you want to run a command as.<br>
Answer : -u

2. How would I run whoami as user jen?<br>
Answer : sudo -u jen whoami

3. How do you list your current sudo privileges(what commands you can run, who you can run them as etc.) <br>
Answer : -l

## Task-36 Section 6: Miscellaneous : Adding users and groups  

1. How would I add the user test to the group test<br>
Answer : sudo usermod -a -G test test

## Task-37 to Task-42 read and submit

## Task-43 Bonus Challenge - The True Ending
** Best task in the whole room. I recommend to first try yourself **

* First we check for sudo priveleges by using command - sudo -l. None of the users can use sudo
* Let's search for files, which each users have using command - find / -user shiba(1,2,3,4) -type f 2>/dev/null. We find an interesting file in shiba2 name /var/log/test1234.
* We will switch to shiba2 and see the file content by using command - su shiba2 and then cat /var/log/test1234.
* We got credentials for another user nootnoot:not******
* Switch to this user by - su nootnoot and type sudo -l to see its permissions
* We see that this user has full root privileges.
* Now simply cat the file using commmand - sudo cat /root/root.txt  and we will get the flag.

1. Finish this room off! What is the root.txt flag <br>
Answer : ad91****************************

**This was a basic privilege level escalation**
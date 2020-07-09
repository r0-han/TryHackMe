# TryHackMe The Find Command
* A learn-by-doing approach to the find command
* One of the most useful command in entire linux system

## Task-1 Start Finding
Answer : Read and submit

## Task-2 Be more specific

1. Find all files whose name ends with ".xml"<br>
Answer : find / -type f -name "*.xml" (*can be done with task description* )

2. Find all files in the /home directory (recursive) whose name is "user.txt" (case insensitive)<br>
Answer : find /home -type f -iname user.txt (*can be done with task description*)

3. Find all directories whose name contains the word "exploits"<br>
Answer : find -type d -name "*exploits*" (*can be done with task description and some basic regex*)

## Task-3 Know exactly what you're looking for
* Read the description very carefully and gather some knowledge about permission in linux file system

1. Find all files owned by the user "kittycat"<br>
Answer : find / -type f -user "kittycat"

2. Find all files that are exactly 150 bytes in size<br>
Answer : find / -type f -size 150c

3. Find all files in the /home directory (recursive) with size less than 2 KiB’s and extension ".txt"<br>
Answer : find /home -type f -size -2k -name "* .txt"

4. Find all files that are exactly readable and writeable by the owner, and readable by everyone else (use octal format)<br>
Answer : find / -type f -perm 644

5. Find all files that are only readable by anyone (use octal format)<br>
Answer : find / -type f -perm 444 

6. Find all files with write permission for the group "others", regardless of any other permissions, with extension ".sh" (use symbolic format)<br>
Answer : find / -type f -perm -o=w -name "* .sh"

7. Find all files in the /usr/bin directory (recursive) that are owned by root and have at least the SUID permission (use symbolic format)<br>
Answer : find /usr/bin -type f -user root -perm -u=s

8. Find all files that were not accessed in the last 10 days with extension ".png"<br>
Answer : find / -type f -atime -10 -name "* .png"

9. Find all files in the /usr/bin directory (recursive) that have been modified within the last 2 hours<br>
Answer : find /usr/bin -type f -min 120
 
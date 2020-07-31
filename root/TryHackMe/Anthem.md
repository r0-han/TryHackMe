# TryHackMe Anthem
**Exploit a Windows machine in this beginner level challenge.**

## Task-1 Website Analysis

2. What port is for the web server?<br>
Answer : 80

3. What port is for remote desktop service?<br>
Answer : 3389

4. What is a possible password in one of the pages web crawlers check for?<br>
Answer : UmbracoIsTheBest! (*robots.txt*)

5. What CMS is the website using?<br>
Answer : Umbraco

6. What is the domain of the website?<br> 
Answer : anthem.com (*from website*)

7. What's the name of the Administrator<br>
Answer : Solomon Grundy (*On the page 'a cheers to our IT department' there is a poem which is related with Solomon Grundy*)

8. Can we find find the email address of the administrator?<br>
Answer : SG@anthem.com (*On the page 'we are hiring there is an author Jane Doe whose email is JD@anthem.com which gives us a hint*)

## Task-2 Spot the flags

1. What is flag 1?<br>
Answer : THM{L0L_WH0_US3S_****} (*view page source of 'We are hiring' and search for THM*)

2. What is flag 2?<br>
Answer : THM{G!T_****} (*view page source and search for THM*)

3. What is flag 3?<br>
Answer : THM{L0L_WH0_***} (*ip/authors*)

4. What is flag 4?
Answer : THM{AN0TH3R_****} (*view page source of 'a cheers to our IT department' and search for THM*)

## Task-3 Final stage

* For privesc we will use 'rdesktop' as port 3389 is open. Type 'rdesktop ip' in your kali and windows 7 application will start running on your machine. Login using 'sg:UmbracoIsTheBost!' as we saw in the above results. After logging in  we can see a user file on desktop which is answer to outr first question.

2. Gain initial access to the machine, what is the contents of user.txt?<br>
Answer : THM{N00T_****}

* Now open your file manager in windows and click on 'view' on the taskbar and then select the checkbox 'hidden items'. After that go on your C drive and you will see a hidden folder named 'backup'. In there is a file named 'restore' which does not open as we don't have right privileges. Now right click the file and select properties and then security. Then click on 'edit' on Groups and username. Then add a user named 'SG' and you will see a user added in the Groups and username category. Select the checkbox with 'full control'. And now open the file. You will have your answer to below question. 

3. Can we spot the admin password?<br>
Answer : ChangeMeBaby1MoreTime

* For this switch the user and type these creds 'administrator:ChangeMeBaby1MoreTime' which we got from above result. You are logged in successfully and will see a root file on desktop which is the answer to below question.

4. Escalate your privileges to root, what is the contents of root.txt?<br>
Answer : THM{Y0U_4R3_****}
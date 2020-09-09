# WebAppSec 101
**In this room, we will walk through how to testing an application in the perspective of a hacker/penetration tester**

## Taks-2 Walking through the application

* Intercept the request in Burp for the home page of the site.

1. What version of Apache is being used?<br>
Answer : 2.4.*

2. What language was used to create the website?<br>
Answer : php

3. What version of this language is used? <br>
Answer : 5.5.*

## Task-4 Authentication

* Go to admin panel and try admin:admin.

1. What is the admin username?<br>
Answer : adm**

2. What is the admin password?<br>
Answer : adm**

3. What is the name of the cookie that can be manipulated?    <br>
Answer : sess*** ( ' *Intercept the request using burp* ' )

4. What is the username of a logged on user?<br>
Answer : bry** ( ' *Go to recenet section and explore* ' )

5. What is the corresponding password to the username?<br>
Answer : bry** ( ' *Follow the hint* ' )

## Task-5 Cross Site Scripting (XSS)
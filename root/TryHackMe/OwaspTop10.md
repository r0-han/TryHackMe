# TryHackMe Owasp Top 10
**Learn one of the OWASP vulnerabilities every day for 10 days in a row.**

## Task-6 [Day 1] Command Injection Practical 

1. What strange text file is in the website root directory?<br>
Answer : dr******.txt ( ' *ls* ' )

2. How many non-root/non-service/non-daemon users are there?<br>
Answer : 0 ( ' *cat /etc/passwd* ' )

3. What user is this app running as?<br>
Answer : www-**** ( ' *whoami* ' )

4. What is the user's shell set as?<br>
Answer : /usr/sbin/no***** ( ' *cat /etc/passwd* ' After ':' of user 'www-data') 

5. What version of Ubuntu is running?<br>
Answer : 18.0*.* ( ' *lsb_release -a*' ) 

6. Print out the MOTD.  What favorite beverage is shown?<br>
Answer : DR PE**** ( ' *cat /etc/update-motd.d/00-header* ' )

## Task-8 [Day 2] Broken Authentication Practical

1. What is the flag that you found in darren's account?<br> 
Answer : fe86079416a21a3c99937f********** ( ' *as described in room desc* ' )

3. What is the flag that you found in arthur's account?<br>
Answer : d9ac0f7db4fda460ac3ede********** ( ' *as described in room desc* ' )

## Task-12 [Day 3] Sensitive Data Exposure (Challenge) 

1. Have a look around the webapp. The developer has left themselves a note indicating that there is sensitive data in a specific directory. What is the name of the mentioned directory?<br>
Answer : /as**** ( ' *Follow the hint* ' )

2. Navigate to the directory you found in question one. What file stands out as being likely to contain sensitive data?<br>
Answer : weba**.** ( ' *from above result* ' )

3. Use the supporting material to access the sensitive data. What is the password hash of the admin user?<br>
Answer : 6eea9b7ef19179a06954ed********** ( ' *From supporting material* ' )

4. Crack the hash. What is the admin's plaintext password?<br>
Answer : qwerty**** ( ' *cracking the hash from https://crackstation.net/* ' )

5. Login as the admin. What is the flag?<br>
Answer : THM{Yzc2YjdkMjE5N2VjMzNhOT**********} ( ' *Using the creds to login page* ' ) 

## Task-14 [Day 4] XML External Entity - eXtensible Markup Language

* All answers are from supporting material.

1. Full form of XML<br>
Answer : eXtensible Markup Language

2. Is it compulsory to have XML prolog in XML documents?<br>
Answer : No

3. Can we validate XML documents against a schema?<br>
Answer : Yes

4. How can we specify XML version and encoding in XML document?<br>
Answer : xml prolog

## Task-15 [Day 4] XML External Entity - DTD 

* All answers are from supporting material

1. How do you define a new ELEMENT? <br>
Answer : !ELEMENT 

2. How do you define a ROOT element?<br>
Answer : !DOCTYPE

3. How do you define a new ENTITY?<br>
Answer : !ENTITY

## Task- 17 [Day 4] XML External Entity - Exploiting 

3. What is the name of the user in /etc/passwd<br>
Answer : fa**** ( ' *Using payload in support material*')

4. Where is falcon's SSH key located?<br>
Answer : /home/falcon/.ssh/****** ( ' *General location of id_rsa file* ' )

5. What are the first 18 characters for falcon's private key<br>
Answer : MIIEogIB********** ( ' *Read the above file* ' )

## Task-19 [Day 5] Broken Access Control (IDOR Challenge)

3. Look at other users notes. What is the flag?<br>
Answer : flag{five********e} ( ' *note=0* ' )

## Task-20 [Day 6] Security Misconfiguration

2. Hack into the webapp, and find the flag!<br>
Answer : thm{4b9513968fd564a87b28aa**********} ( ' *Google search 'Pensive Notes' according to given hint and then you will get a github link* ' )

## Task-21 [Day 7] Cross-site Scripting 

2. Go to http://IP/reflected and craft a reflected XSS payload that will cause a popup saying "Hello".<br>

* First go to 'IP' and then select Reflected XSS

Answer : ThereIsMoreToXSSThan******** ( ' *\<script\>alert("Hello")\</script\>* ' )

3. On the same reflective page, craft a reflected XSS payload that will cause a popup with your machines IP address.<br>
Answer : ReflectiveXs******** ( ' *\<script\>alert(window.location.hostname)\</script\>* ' )

4. Now navigate to http://IP/stored and make an account. Then add a comment and see if you can insert some of your own HTML. <br>
Answer : HTML_**** ( ' *\<h1\>alert("Hello")\</h1\>* ' )

5. On the same page, create an alert popup box appear on the page with your document cookies.<br>
Answer : W3LL_D0N3_**** ( ' *\<h1\>alert(document.cookie)\</h1\>* ' )

6. Change "XSS Playground" to "I am a hacker" by adding a comment and using Javascript.<br>
Answer :  websites_can_be_easily_defaced_******** ( ' *\<script\> document.getElementById("thm-title").innerHTML = 'I am a hacker'\</script
>* ' )

## Task-22 [Day 8] Insecure Deserialization

1. Who developed the Tomcat application?<br>
Answer : The Apache ******** ********** ( ' *Search google for Tomcat developer* ' )

2. What type of attack that crashes services can be performed with insecure deserialization?<br>
Answer : Denial ** ******* ( ' *Hint iss enough* ' )

## Task-24 [Day 8] Insecure Deserialization - Objects 

1. Select the correct term of the following statement: if a dog was sleeping, would this be:
A) A State B) A Behaviour <br>
Answer : A Behaviour

## Task-24 [Day 8] Insecure Deserialization - Deserialization

1. What is the name of the base-2 formatting that data is sent across a network as?   <br>
Answer : binary

## Task-25 [Day 8] Insecure Deserialization - Cookies

1. If a cookie had the path of webapp.com/login , what would the URL that the user has to visit be? <br>
Answer : webapp.com/login

2. What is the acronym for the web technology that Secure cookies work over?<br>
Answer : HTTPS

## Task-26 [Day 8] Insecure Deserialization - Cookies Practical 

1. 1st flag (cookie value) <br>
Answer : THM{good_old_base******} (  ' *Network tab under inspect element in firefox. Decode the base64 string given in sessionid* ' )

2. 2nd flag (admin dashboard)<br>
Answer : THM{heres_the_admi******} ( ' *Change the userType to admin and then refresh* ' )

## Task-27 [Day 8] Insecure Deserialization - Remote Code Execution

1. flag.txt <br>
Answer : 4a69a7f****** ( ' *Follow the steps in support material. After getting shell go to /home/cmnatic directory to get flag.txt* ' )

## Task-30 [Day 9] Components With Known Vulnerabilities - Practical

1. How many characters are in /etc/passwd (use wc -c /etc/passwd to get the answer) <br>
Answer : 16** ( ' *Got the exploit on https://www.nmmapper.com/st/exploitdetails/47887/42206/online-book-store-10-unauthenticated-remote-code-execution/. Download the python file and then run it giving the url - http://IP. After that type ' wc -c /etc/passwd '* ' )	

## Task-31 [Day 10] Insufficient Logging and Monitoring 

1. What IP address is the attacker using? <br>
Answer : 49.99.**.** ( ' *Most common occuring IP* ' )

2. What kind of attack is being carried out?<br>
Answer : Brute ***** ( ' *Follow the hint* ' )


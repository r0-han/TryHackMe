# TryHackMe Crack The Hash
**Cracking hashes challenges**
* Most of the hashes can be cracked with online tools but i recommend to use linux for cracking

## Task-1 Level 1

1. 48bb6e862e54f2a795ffc4e541caed4d<br>
Answer : ea** <br>
* This is an md5 hash as given in hint so we can use hashcat to crack this. Just type the command *hashcat -m 0 hash_to_crack rockyou.txt* and you will have your answer.

2. CBFDAC6008F9CAB4083784CBD1874F76618D2A97<br>
Answer : pas******** 
* This is SHA-1 and can be cracked by command (*hashcat -m 100 hash_to_crack rockyou.txt*)

3. 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032<br>
Answer : let****
* This is SHA-2 and can be cracked by command (*hashcat -m 1400 hash_to_crack rockyou.txt*)

4. $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom<br>
Answer : bleh 
* I have provided this password as it took a lot of time to crack it using command (*hashcat -m 3200 has_to_crack rockyou.txt*)

5. 279412f945939ba78ce0758d3fd83daa<br>
Answer : Eter****22 
* This is MD4 and can be cracked by command (*hashcat -m 900 hash_to_crack rockyou.txt*)

## Task-2 Level 2

1. F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85<br>
Answer : pau** 
* This is SHA-256 and can be cracked by command (*hashcat -m 1400 hash_to_crack rockyou.txt*)

2. 1DFECA0C002AE40B8619ECF94819CC1B<br>
Answer : n63u******** 
* This is NTLM and can be craced by command (*hashcat -m 1000 hash_to_crack rockyou.txt*)

3. Hash: $6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02 .Salt: aReallyHardSalt .Rounds: 5<br>
Answer : wak***
* This is basically a linux shadow file and can be cracked by command (*hashcat -m 1800 hash_to_crack rockyou.txt*)

4. Hash: e5d8870e5bdd26602cab8dbe07a942c8669e56d6. Salt: tryhackme<br>
Answer : 4816******** 
* This is basically HMAC-SHA1 and can be cracked by command (*hashcat -m 160 hash_to_crack:salt rockyou.txt*)

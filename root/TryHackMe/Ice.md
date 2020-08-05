# TryHackMe Ice
**Deploy & hack into a Windows machine, exploiting a very poorly secured media server.**

## Task-2 Recon

* For recon I used (*nmap -A -v ip*)

3. Once the scan completes, we'll see a number of interesting ports open on this machine. As you might have guessed, the firewall has been disabled (with the service completely shutdown), leaving very little to protect this machine. One of the more interesting ports that is open is Microsoft Remote Desktop (MSRDP). What port is this open on?<br>
Answer : 3389

4. What service did nmap identify as running on port 8000? (First word of this service)<br>
Answer : Icecast

5. What does Nmap identify as the hostname of the machine? (All caps for the answer)<br>
Answer : DARK-PC

## Task-3 Gain Access

1. Now that we've identified some interesting services running on our target machine, let's do a little bit of research into one of the weirder services identified: Icecast. Icecast, or well at least this version running on our target, is heavily flawed and has a high level vulnerability with a score of 7.5 (7.4 depending on where you view it). What type of vulnerability is it? Use https://www.cvedetails.com for this question and the next.<br>
Answer : Execute Code Overflow

2. What is the CVE number for this vulnerability? This will be in the format: CVE-0000-0000<br>
Answer :  CVE-2004-1561

4. After Metasploit has started, let's search for our target exploit using the command 'search icecast'. What is the full path (starting with exploit) for the exploitation module? This module is also referenced in 'RP: Metasploit' which is recommended to be completed prior to this room, although not entirely necessary.<br>
Answer : exploit/windows/http/icecast_header

6. Following selecting our module, we now have to check what options we have to set. Run the command `show options`. What is the only required setting which currently is blank?<br>
Answer : rhosts

## Task-4 Escalate

1. Woohoo! We've gained a foothold into our victim machine! What's the name of the shell we have now?<br>
Answer : meterpreter

2. What user was running that Icecast process? The commands used in this question and the next few are taken directly from the 'RP: Metasploit' room.<br>
Answer : Dark (*getuid*)

3. What build of Windows is the system?<br>
Answer : 7601 (*sysinfo*)

4. Now that we know some of the finer details of the system we are working with, let's start escalating our privileges. First, what is the architecture of the process we're running?<br>
Answer : x64 (*sysinfo*)

6. Running the local exploit suggester will return quite a few results for potential escalation exploits. What is the full path (starting with exploit/) for the first returned exploit?<br>
Answer : exploit/windows/local/bypassuac_eventvwr

10. Now that we've set our session number, further options will be revealed in the options menu. We'll have to set one more as our listener IP isn't correct. What is the name of this option?<br>
Answer : LHOST

14. We can now verify that we have expanded permissions using the command `getprivs`. What permission listed allows us to take ownership of files?<br>
Answer : SeTakeOwnershipPrivilege

## Task-5 Loot

2. In order to interact with lsass we need to be 'living in' a process that is the same architecture as the lsass service (x64 in the case of this machine) and a process that has the same permissions as lsass. The printer spool service happens to meet our needs perfectly for this and it'll restart if we crash it! What's the name of the printer service? Mentioned within this question is the term 'living in' a process. Often when we take over a running program we ultimately load another shared library into the program (a dll) which includes our malicious code. From this, we can spawn a new thread that hosts our shell.<br>
Answer : spoolsv.exe

4. Let's check what user we are now with the command `getuid`. What user is listed?<br>
Answer : NT AUTHORITY\SYSTEM

7. Which command allows up to retrieve all credentials?<br>
Answer : creds_all 

8. Run this command now. What is Dark's password? Mimikatz allows us to steal this password out of memory even without the user 'Dark' logged in as there is a scheduled task that runs the Icecast as the user 'Dark'. It also helps that Windows Defender isn't running on the box ;) (Take a look again at the ps list, this box isn't in the best shape with both the firewall and defender disabled)<br>
Answer : Password01! (*just type the last part of hash on crackstation*)

## Task-6 Post Exploitation

2. What command allows us to dump all of the password hashes stored on the system? We won't crack the Administrative password in this case as it's pretty strong (this is intentional to avoid password spraying attempts)<br>
Answer : hashdump

3. While more useful when interacting with a machine being used, what command allows us to watch the remote user's desktop in real time?<br>
Answer : screenshare

4. How about if we wanted to record from a microphone attached to the system?  <br>
Answer : record_mic

5. To complicate forensics efforts we can modify timestamps of files on the system. What command allows us to do this? Don't ever do this on a pentest unless you're explicitly allowed to do so! This is not beneficial to the defending team as they try to breakdown the events of the pentest after the fact.<br>
Answer : timestomp

6. Mimikatz allows us to create what's called a 'golden ticket', allowing us to authenticate anywhere with ease. What command allows us to do this? Golden ticket attacks are a function within Mimikatz which abuses a component to Kerberos (the authentication system in Windows domains),the ticket-granting ticket. In short, golden ticket attacks allow us to maintain persistence and authenticate as any user on the domain<br>
Answer : golden_ticket_create

 
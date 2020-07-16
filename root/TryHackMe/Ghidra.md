# TryHackMe Ghidra
**A crash course on the reverse engineering tool Ghidra**

* Before moving further I would suggest to get some basic knowledge about C and assembly language. 

## Task-4 It's your turn!

1. How many user created functions(including main) are there<br>
Answer : 2 (*main, fun1*) 

2. What is the first variable set to in the main function?<br>
Answer : a0 (*0xa*)

3. What is the first variable set to, in the function "fn1"?<br>
Answer : hello

4. If you provide the input "1", when you run the binary, what would the output be.(Note you can just run the binary to find this out, but that would defeat the whole purpose!).<br>
Answer : nice! (*After dissassembling you can see the C code and decode the output*)

## Task-5 Final Exam

1. What outputs the good job message?    <br>
Answer : goodjob (*After dissassembling you can see the C code and decode the output*)
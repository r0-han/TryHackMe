# TryHackMe CC:Steganography
**A crash course on the topic of steganography**

* According to me it is one of the most important room if you are a ctf player or a beginner in ctf. This room will give an idea about various ctf challenges and how to solve them. Most important, the tools used in them are highly recommended by ctf players.

* Download zip file and unzip file to continue in room

## Task-1 Intro
Answer : Read and submit

## Task-2 Steghide

* Below questions are answerd with *tool --help* page

1. What argument allows you to embed data(such as files) into other files?<br>
Answer : embed

2. What flag let's you set the file to embed?<br>
Answer : -ef

3. What flag allows you to set the "cover file"?(i.e  the jpg)<br>
Answer : -cf

4. How do you set the password to use for the cover file?<br>
Answer : -p 

5. What argument allows you to extract data from files?<br>
Answer : extract

6. How do you select the file that you want to extract data from?<br>
Answer : -sf

7. Given the passphrase "password123", what is the hidden message in the included "jpeg1" file.<br>
Answer : ping**** 
* This can be done using command (*steghide --extract -sf jpeg1.jpg*) and then providing password.

## Task-3 zsteg

1. How do you specify that the least significant bit comes first<br>
Answer : --lsb

2. What about the most significant bit?<br>
Answer : --msb

3. How do you specify verbose mode?<br>
Answer : -V

4. How do you extract the data from a specific payload?<br>
Answer : -E

5. In the included file "png1" what is the hidden message?<br>
Answer : noot****$
* This can be done using command (*zsteg png1.png*)

6. What about the payload used to encrypt it.<br>
Answer : b1,bgr,lsb,xy

## Task-4 Exiftool

1. In the included jpeg3 file, what is the document name<br>
Answer : Hel** **
* This can be done using command (*exiftool jpeg3.jpg*)

## Task-5 Stegoveritas

1. How do you check the file for metadata?<br>
Answer : -meta

2. How do you check for steghide hidden information<br>
Answer : -steghide

3. What flag allows you to extract LSB data from the image?<br>
Answer : -extractLSB

4. In the included image jpeg2 what is the hidden message?<br>
Answer : keke*****
* This can be done using the given hint and then traverse thru that directory and 'cat' the file

## Task-6 Spectrograms

1. What is the hidden text in the included wav2 file?<br>
Answer : Go**** 
* For this just follow the description

## Task-7 The Final Exam

1. What is key 1?<br>
Answer : supe****
* First deploy the machine and then download the file from site and then perform exiftool on this. It will give you a password. This is a hint as the stegano used is steghide. Now extract the password using above command mentioned in above task. Now enter the key and proceed to exam2.

2. What is key 2?<br>
Answer : fata****
* This can be done first by opening the file in sonic visualizer and then adding a spectrogram which will give us a link. As the last part of the url is somewhat confusing so here it is - 'KTrtNI5'. Now it will redirect you to a page and download the image from there. It will be an 'png' file so we can perform zsteg on it which will give us our key. Submit this key and proceed to final exam.

3. What is key 3?<br>
Answer : kill****
* This can be done by downloading the qrcode. As you can see the colors are somewhat faded.I used stegoveritas on this and got many qr codes from this. Eventually one of them will have our answer. Scan all of them and you will get your answer. Luckily i got mine in first attempt.
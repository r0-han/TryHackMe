# TryHackMe Shodan.io
* Learn about Shodan.io and how to use it for devices enumeration - is your coffee machine publicly accessible?
* Answers may vary

## Task-1 Introduction
Answer : Read and submit

## Task-2 Getting Started

1. What is Google's ASN number?<br>
Answer : AS15169 (*search on shodan according to given hint*)

2. When was it allocated? Give the year only.<br>
Answer : 2000

3. Where are most of the machines on this ASN number, physically in the world?<br>
Answer : United States (*topmost country*)

4. What is Google's top service across all their devices on this ASN?<br>
Answer : SSH (*from above search results*)

5. What SSH product does Google use?<br>
Answer : openSSH (*from above search results*)

6. What is Google's most used Google product, according to this search? Ignore the word "Google" in front of it.<br>
Answer : cloud (*from above search results*)

## Task-3 Filters
Answer : Read and submit

## Task-4 Google & Filtering

1. What is the top operating system for MYSQL servers in Google's ASN?   <br>
Answer : Microsoft server 2008 (*take help from description. Answer may vary*) 

2. What is the 2nd most popular country for MYSQL servers in Google's ASN?<br>
Answer : Singapore (*Answer may vary*)

3. Under Google's ASN, which is more popular for nginx, Hypertext Transfer Protocol or Hypertext Transfer Protocol(s)?<br>
Answer : Hypertext Transfer Protocol (*just change product:nginx*)

4. Under Google's ASN, what is the most popular city?<br>
Answer : Mountain View (*Click on topmost country to get the answer*)

5. Under Google's ASN in Los Angeles, what is the top operating system according to Shodan?<br>
Answer : Linux 3.x (*Click on Los Angeles to get answer. Asterisks may help*)

6. Using the top Webcam search from the explore page, does Google's ASN have any webcams? Yay / nay.<br>
Answer : Nay (*search for AS15169 webcam*)

## Task-5 Exploring the API & Conclusion
Answer : Read and submit
# TryHackMe Google Dorking
**This room will give an idea about SEO, robots.txt, google dorking and google related search**

## Task 1 - Ye Ol' Search Engine
* Nothing to do in this task. Just read the desc and 	submit.

## Task 2 - Let's learn About Crawlers
* ctrl+f will be your friend in this task

1. Name the key term of what a "Crawler" is used to do  \n
Answer : index

2. What is the name of the technique that "Search Engines" use to retrieve this information about websites?
Answer : crawling 

3. What is an example of the type of contents that could be gathered from a website?
Answer : keywords

## Task 3 - Enter: Search Engine Optimisation
* Just visit the given sites and answer the questions.

1. Using the SEO Site Checkup tool on "tryhackme.com", does TryHackMe pass the “Meta Title Test”? (Yea / Nay)
Answer : Yea

2. Does "tryhackme.com" pass the “Keywords Usage Test?” (Yea / Nay)
Answer : Nay

3. Use https://neilpatel.com/seo-analyzer/ to analyse http://googledorking.cmnatic.co.uk: What "Page Score" does the Domain receive out of 100?
* You have to do it by yourself as answer would be diiferent from mine.
Ansewer : 85/100 (Don't Copy)

4. With the same tool and domain in Question #3 (previous): How many pages use “flash” 
* I didn't find anything with the text 'flash' so answer would be 
Answer : 0

5.  From a "rating score" perspective alone, what website would list first? tryhackme.com or googledorking.cmnatic.co.uk Use tryhackme.com's score of 62/100 as of 31/03/2020 for this question.
Answer : googledorking.cmnatic.co.uk (Asterisks will give you the hint)

## Task 4 - Beepboop - Robots.txt
* Just by reading the desc you can answer the questions.

1. Where would "robots.txt" be located on the domain "ablog.com"
Answer : ablog.com/robots.txt

2. If a website was to have a sitemap, where would that be located?
Answer : /sitemap.xml

3. How would we only allow "Bingbot" to index the website? 
Answer : User-Agent:Bingbot

4. How would we prevent a "Crawler" from indexing the directory "/dont-index-me/"?
Answer : Disallow:/dont-index-me/

5. What is the extension of a Unix/Linux system configuration file that we might want to hide from "Crawlers"?
Answer : .conf (if you're familiar with linux you will know this)

## Task 5 - Sitemaps
* Just by reading the desc you can answer the questions.

1. What is the typical file structure of a "Sitemap"?
Answer : xml

2. What real life example can "Sitemaps" be compared to?
Answer : map (ctrl+f)

3. Name the keyword for the path taken for content on a website
Answer : route (hint = the word 'path'  and ctrl+f)

## Task 6 - What is Google Dorking? 
* Just read desc and answer the questions

1. What would be the format used to query the site bbc.co.uk about flood defences
Answer : site:bbc.co.uk flood defences

2. What term would you use to search by file type?
Answer : filetype

3. What term can we use to look for login pages?
Answer : intitle:login
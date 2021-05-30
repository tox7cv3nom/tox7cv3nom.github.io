---
layout: post
published: true
title: Authentication Token Leads To IDOR
tags:
  - bug hunting
comments: true
search: true

---



  
## Introduction
<div align="center">Here is the article how i was able to bypass authentication token and able to exploit idor and add any user to add events of website ..before coming on main topic that how i find the vulnerablity let me clear your core concepts about authorization tokens</div>

**Authorization tokens : They are used to authenticate user suppose a user partha visited a website and create their accounts authorization token verifies the user each time when partha logon in website web page gives him auth token ands when he logout then token get destroyed and each time when partha login to that website he gots a new token thats the work of auth tokens..it prevents from vulnerablities like idor,csrf and cors**

## Exploiting Vulnerablity

<div align="center">so that's the basic concept about authorization tokens.. now i tell my stort of getting idors i was really excited when i got a invitation program i decided to look at that program i saw there the site was implementing auth tokens for identifying users it creates a new token when user logged in each time and destroy the token when user logout from website after playing with request and response i saw there when the request was send with 'PATCH' method without auth token shows 401(unauthorized) response while the request with any other method without auth token it shows response 200 (ok).it means token not implemented properly :) i tried to change patch method to get but stil found 401 the other request other then 'patch' method are seems to be useless becoz there was no crucial data which i report to website so i decided to check every page which consist of GET or POST methods i fuzz every page there i saw there was option to register on event any one can register in event by uploading his/her resume and his name ..i quickly created another account on website and register my 2nd account on event and logout from my device and then i  open burp and change email id,name and id no. to mine first account and remove auth token and bingo! i got registered on that event from my account with the resume and information of other candidate due to idor</div> 

**Tip: eveytime check all request and response check website architecture i.e how token works,how the website is behaving on ur query i.e responses 200,401,302 etc. and most important never give up everything is vulnerable just think out of box :)**

any private program ?

send it to : <a href="mailto:nhibtaungamain@gmail.com">@mohit</a>

  </div>


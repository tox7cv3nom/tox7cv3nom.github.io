---
layout: post
published: true
title: How I Abuse Auth Token To Get Account Takeover Via Chained WithCsrf
tags:
  - bug hunting
comments: true

---

# Introduction
Well this is my another artcle in which i share my experience how i abuse and expoloit authenticity tokens and chain with csrf to get full account takover if you don’t know what authenticity tokens are , Here is my another <a href="https://tox7cv3nom.github.io/2020-07-28-authentication-token-bypass-leads-too-idor/">article</a> related to same issue chained to idor
They are unique tokens given to authentic user to prevent the vulnerablity like Cors,Csrf,Idor etc. Each user on web application have unique session and also have unique authenticity token


# Exploitation
So, let’s start about how i found this issue i was finding a vulnerablity in public program i just create a blueprint of the api,endpoints,requests in my mind i saw that it has a functionality of upload resume on tat program i uploaded a resume and capture the request i saw there was a authenticity token and user id i tried to test idor by changing username but authenticity token was there to prevent the issue but when i removes authenticity token and send request it gives me 500 error instead of 401 i was like:

since it gives 500 error instead of 200 ok i thught there is some misconfirgution of token then suddenly i saw there was the option of change of username and password i create second account as victim i captures the request of 1st account and change the password and capture the request and as attacker i change the email address and old password with vctim account and create a csrf payload (by removing auth token) and send to victim i.e 2nd account and viola password successfully changed means our csrf works!!!
but problem is that the application asks us for old password when we change password how we get old password o victim I suddenly started digging more and find out there is a option of login with 3rd party application like google,facebook,etc. i suddenly created two accounts 1st one is login with facebook and 2nd account with login with facebook and since there was no old password becoz there was no login based password to access facebook there was auth token so icreate poc of csrf and send to victim and viola!! account got takeover …



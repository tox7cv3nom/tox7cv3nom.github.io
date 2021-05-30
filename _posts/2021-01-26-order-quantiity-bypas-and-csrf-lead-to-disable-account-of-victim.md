---
layout: post
published: true
title: Csrf Leads To Disable Account Of Arbitrary User
tags:
 - bug hunting
 
comments: true

---

# Basic Overview Of Bug
in this article i will show how a csrf attack and cart rate limit bypass leads to ddos on victim account which leads to temprory ban of user account i was pentesting on private website it was a e-commerce website where you can buy and purchase goods after spending a litle bit time in recon i saw that there was no csrf token present at any webpage i tried to do csrf attack before i begin let's clear the concept of csrf and csrf tokens am not going deep its just a overview (that section is for newbies if you are leet you can skip this part) :-

**csrf stands for cross site request forgery in this attack any attacker can force user to do arbitrary action in victim's browser unintentinaly if you don't get this line let me explain suppose you are depositing in a bank's account online and there is no csrf token on this wesbite anyone can create a lookalike page of that bank and embbebd the request to withdraw money of 1000$ with a button of submit,click etc. to his account in that lookalike when uh open and click on that button (in same browser in which uh are doing work) transaction occurs and 1000$ gone to his account without the knowledge of victim now read that upper line hope it clear your concept about csrf**

csrf tokens are used to prevent csrf each time when session regenrate the csrf token automatically regenrate thats why its hard to bypass csrf token by guessing now lets come to main topic .. i was about to know that there is no csrf token present on that website then i tried to do csrf i capture the request of adding items to cart there was a permiter checkout = [value of items] i just change the value to 25k and guess what 25k items added in my cart that leads to order quantity bypass in cart

I was happy i quickly capture the requestand genrate csrf poc with the help of burp and send to my another account when i click on submit it was 1000 items added in cart of victim without knowing i can also remove the items as same steps but this was not enough to for a worthy report so i decided to give it more then a plan comes up in mind i modify the request and add around 10 crores items in victim's account with the exploit of csrf of which i made with burp and after adding 10crores items when victim (me in second tab) refresh the page i was not able to access my account that website banned victim account for doing appropriate things with lots of traffic it triggered banning of account :)

i reported this bug to company they were not providing bounty nor it was bug bounty program but still they fix the bug

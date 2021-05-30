---
layout: post
published: true
title: Regex Injection Leads To Dos Attack 
tags:
  - Programming
  - python3
comments: true

---

# Basic plot
In this article, I talk about how can be exploited regex to shut down the site for legitimate Users for a few hours or minutes depending on the capacity of the web application.

# Exploitation

I am assuming that you all know about regex and why it’s used if you don’t know then I will give a short explanation
Regex is used for searching, replacing a specific pattern or substring in a bunch of strings. it’s basically used for manupulating strings
for ex- if you have a lot of phone numbers of Australia,UK,India in a list but you want to extract only Indian phone number then you need to create a regex or pattern to find Indian phone number
Hope you all know what’s regex does some application uses regex for searching the user's phone number or password let’s consider a python code:

```
def check_password(password):
user = input(‘plz enter your password’)
if regex.match(user,password):
print(‘user created’)
else:
print(‘Username not be password’)
```

This is a sample code I wrote in python In this application is using a regex which is matching the password field with username in which it basically seeing for security purposes username can’t be a password In this point evil regex comes to play suppose we enter “^((ab)*)+$” in this, the application will search for all proceedings of a and ab it’s an evil regex it will find all possibilities of ab one by one and grouping results will be thousand and this leads to took unusual time for a web application to find the username and that leads to crash of browser or sometimes firewall or application This is why evil regex is dangerous
Mitigations To Prevent Redos
Regex is cute AF but sometimes it seems dangerous. For preventing this vulnerability web applications should prevent or limit input regex from users in their application by restriction of group parenthesis, a pattern repeated for more than one time. etc.

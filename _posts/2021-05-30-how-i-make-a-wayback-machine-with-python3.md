---
layout: post
published: true
title: making a wayback machine with python3
tags:
  - programming
  - python3
comments: true
---

# Requirements for writing code
In this tutorial i will show how we make a simple wayback machine with python 3 to extract arcieved url we will use classes and object i am assuming that you all are unsderstable with the concept of oops in python let’s start
first we need to import following modules:

~~~
import requests
import sys
~~~

Now let’s start writing our code :

~~~
class machine():
def __init__(self, limit, url):
self.url = “https://web.archive.org/cdx/search?url="+url+"&matchType=prefix&collapse=urlkey&output=text&fl=original&\
filter=&limit=”+str(limit)
here in the above code we create aclass named machine class is nothing just a blueprint of object..here is a function __init__ to create a objeet which has three arguments self,limit and url and then we are fetching the url from web archive website using request module if you wanna learn moree aboutc this module you can learn here now let’s jump back to our code
def post(self):
try:
headers = {
“User-Agent”: “Mozilla/5.0 (X11; U; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.131 Safari/537.36”}
request = requests.get(self.url, headers=headers)
results = request.text
return results
except KeyboardInterrupt:
print(‘[!]operation cancelled by user, exiting…’)
here we create a function name post then we create a user agent for browser for successfull connection and then we store the data in results and print the resaults on our terminal with try and except methodology if user press ctrl +c or stops thge tool he gots error operation cancelled instead of long errors on terminal now the main part of our code comes:
def main():
if len(sys.argv) < 3:
print(“[+]usage plzz enter two arguments”)
exit(0)
url = sys.argv[1]
limit = sys.argv[2]
back = machine(limit, url)
res = back.post()
for i in res.split():
print(i)
if __name__ == ‘__main__’:
main()
~~~

here we create a function main() in which we actually saying if arguments provide to command line is less thhen 3 then our program will print “plzz enter two arguments” then our program will get terminated here are our two main variables according to sys arguments
file name i.e scrap.py #argv[0]
url i.e xyz.com #argv[1]
limit i.e how much page we wanna scrap #argv[2]
then we create another two variable called back and res then we assign the class to variable name back then storing results in res and with the help of for loop we print out our main output and in next line we are just calling our main function the script is hosted at <a href="https://github.com/bing0o/Python-Scripts/blob/master/waybackmachine.py" target="_top">here</a>
i just modified it and made few changes..

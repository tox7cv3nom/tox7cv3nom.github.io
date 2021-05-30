---
layout: post
published: true
title: simple file descriptor challange
tags:
 - ctf
 
comments: true

---


# Introduction
when i saw the challenge there was two files fd and fd.c

```
$ ssh fd@pwnable.kr -p 2222
fd@pwnable.kr's password: guest
 ____  __    __  ____    ____  ____   _        ___      __  _  ____ 
|    \|  |__|  ||    \  /    ||    \ | |      /  _]    |  |/ ]|    \
|  o  )  |  |  ||  _  ||  o  ||  o  )| |     /  [_     |  ' / |  D  )
|   _/|  |  |  ||  |  ||     ||     || |___ |    _]    |    \ |    /
|  |  |  `  '  ||  |  ||  _  ||  O  ||     ||   [_  __ |     \|    \
|  |   \      / |  |  ||  |  ||     ||     ||     ||  ||  .  ||  .  \
|__|    \_/\_/  |__|__||__|__||_____||_____||_____||__||__|\_||__|\_|
                                                                   
- Site admin : daehee87.kr@gmail.com
- IRC : irc.netgarage.org:6667 / #pwnable.kr
- Simply type "irssi" command to join IRC now
- files under /tmp can be erased anytime. make your directory under 
fd@pwnable:~$ ls -la 
total 40 
drwxr-x---   5 root   fd   4096 Oct 26  2016 . 
drwxr-xr-x 115 root   root 4096 Dec 22 08:10 .. 
d---------   2 root   root 4096 Jun 12  2014 .bash_history 
-r-sr-x---   1 fd_pwn fd   7322 Jun 11  2014 fd 
-rw-r--r--   1 root   root  418 Jun 11  2014 fd.c 
-r--r-----   1 fd_pwn root   50 Jun 11  2014 flag 
-rw-------   1 root   root  128 Oct 26  2016 .gdb_history 
dr-xr-xr-x   2 root   root 4096 Dec 19  2016 .irssi 
drwxr-xr-x   2 root   root 4096 Oct 23  2016 .pwntools-cache 
fd@pwnable:~$
when i run ./fd in terminal it shows:
fd@pwnable:~$ ./fd
pass argv[1] a number
fd@pwnable:~$

```

it doesn’t ask for input and show output pass argv[1] is number for solving this issue i decide to break the program now let’s understand the intended behaviour o our program so the program was here :

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
char buf[32];
int main(int argc, char* argv[], char* envp[]){
if(argc<2){
printf(“pass argv[1] a number\n”);
return 0;
}
int fd = atoi( argv[1] ) — 0x1234;
int len = 0;
len = read(fd, buf, 32);
if(!strcmp(“LETMEWIN\n”, buf)){
printf(“good job :)\n”);
system(“/bin/cat flag”);
exit(0);
}
printf(“learn about Linux file IO\n”);
return 0;

}
```
# Exploitation

In this program a function is used called atoi it takes input as a string and produce output as integer if you wanna learn more about this function read from here
we can see here
int fd = atoi( argv[1] ) — 0x1234;
our input which we put in program is subtracted by 0x1234 then stored in a variable name fd and then
if(!strcmp(“LETMEWIN\n”, buf))
string comparision took place means if we can pass this string compare check we got our flag that is the main or crucial point of this game now we all know in linux 0 stands for stdin or input , 1 stands for stdoutor output and 2 stands for stderr we can bypass the string check by this concept
in previous function we saw our input is subtracted from 0x1234 what is the value of 0x1234 in decimal ? well just simply googling it or with help of python we came to know that it’s value is “4660" now what happens if gave input to program as 4660 according to program (input — 0x123i.e(4660 in decimal) our output will be 0 and as i said earlier 0 means stdin or input in linux now after giving 4660 as input the program will gave us a blank line where we could type “LETMEWIN” as a per program say and we got our flag
fd@pwnable:~$ ./fd 4660
LETMEWIN
good job :)
mommy! I think I know what a file descriptor is!!

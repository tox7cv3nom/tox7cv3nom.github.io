
This resarch paper is inspired from <a href="https://azeria-labs.com/heap-exploitation-part-1-understanding-the-glibc-heap-implementation/">azeria</a> If you wanna learn and understand more I will provide resources in comment section.

**Introduction of Heap and Memory**

As we all know Our memory consist of various data segments like *HEAP, STACK, DATA, BSS, GOT, PLT, TXT* as you can see in this architecture this is a memory region consist of those data segments

![alt text](https://cs-fundamentals.com/assets/images/code-data-segments.png)

*BSS & DATA*- conatins variables and pointers used in program

*TXT*- contains executable with  assembly

*PLT & GOI*- contains specific pointers

These all resdides in program code whereas Heap and stack are used for allocating region in memory and storinbg the local variable respectively These resarch paper is all about the Heap so we don't talk about stack in this article 

**Heap and memory curruption**

Heap is used by program to allocate region during program execution. the allocation took place with the help of malloc function when the program finises then the heap manager return the allocation back to heap with the help of function free. In other words malloc is used for allocating the region while free is used for free the allocated region 

Since, heap and stack are memory regions and the data which is stored and allocate in this region is provided by user as user input variable so user can overwrite eip registers, remote code execution, overflow the heap and stack etc. This all can be done by injecting payload in memory region  and it's called *Memory Curruption*. Memory curruption bug leads to modification of memory that leads to remote code execution, overflows etc.



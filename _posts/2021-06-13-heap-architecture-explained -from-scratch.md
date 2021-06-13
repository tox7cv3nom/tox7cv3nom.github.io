
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

**Strategies of Heap To Allocate Chunks**

  Basically heap works on four strategies to allocate a chunk to a region of memory I will depict all the four steps used by heap manager to allocate chunk. *CHUNKS* are the area of memory in heap whis is dynamically allocated via malloc. Now, the four steps are:


1.*Allocation from free chunks*
      This strategy says that if a previous chunk of memory if free by free function and that chunk is large enough to satisfy the request of allocation then heap will use that chunk The free chunks are located in the link list called *bins* whenever the heap manager needed allocation it searches in the bins for the free chunks that satisfy the request of allocation If they found the free chunk in bins then they extracted it from bins and mark the chunks as allocated That's how the strategy works 
      
2. *Allocation from top of heap*
    
 
  




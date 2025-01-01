### Program Running Area:
![[Pasted image 20241011161646.png]]
**Text Area**: This is where Binary Instructions Executed By the processor are Stored
**Data**:This is where non zero initialized  static variables are stored
**BSS** (Block Started by Symbol) : Contains zero-initialized static data. Static data uninitialized in program is initialized 0 and goes here.
**Stack:**:Function Calls , Static Data copy of base pointer
**Heap**:Runtime allocated Memory,Dyanmic Data

As you can see in the image, the stack and the heap grow in the opposite directions.  
Sometimes the data, bss and heap sections are collectively referred to as the “_data segment_”,  
the end of which is demarcated by a pointer named program break or **brk**.  
That is, _brk_ points to the end of the heap.

If I want to allocate more memory to heap i just have to increase the brk pointer
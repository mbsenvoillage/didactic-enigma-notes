Notes on https://www.youtube.com/watch?v=qcBIvnQt0Bw&list=PLiwt1iVUib9s2Uo5BeYmwkDFUh70fJPxX

# Introduction

- What is MIPS ?
  - Microprocessor without Interlocked Pipelined Stages is a family of reduced instruction set computer
- Why virtual memory ?

  - solves the problem with lack of ram
  - holes in address space (when quitting programs which leaves empty slots)
  - simultaneous programs writing over each other

- What is virtual memory ?

  - indirection
  - how does it solve the problems ?
  - page tables and translation

- Implementing virtual memory

  - where do we store the page tables ?
  - making translation fast

- Virtual memory and caches.

# Three problems with memory

- How does word size affect virtual address space ? >> On an n-bit machine, the VAS is 2n bytes large. So, on a 32-bit machine, the VAS 232 = 4 GiB large.
- What is virtual address space ? >> The virtual address space for a process is the set of virtual memory addresses that it can use. The address space for each process is private and cannot be accessed by other processes unless it is shared. A virtual address does not represent the actual physical location of an object in memory; instead, the system maintains a **page table** for each process, which is an internal data structure used to translate virtual addresses into their corresponding physical addresses. Each time a thread references an address, the system translates the virtual address to a physical address. [source](https://learn.microsoft.com/en-us/windows/win32/memory/virtual-address-space). It is the list of possible addresses.
- What if you don't have enough memory ?
- What if there are holes in the address space ? >> another way of calling memory fragmentation. When processes quit, they leave holes in the address space that are not contiguous. They might add up to a lot of memory, but separately they're quite small. The memory might be availabe for a process, but since it's split up it is not usable.
- How do you keep your programs secure aka how do you make sure one program does not overwrite data of another program ?
- If all programs have access to the same 32-bit memory space :
  - can crash if less than 4GB of RAM memory in the system
  - can run out of space if we run multiple programs (memory fragmentation)
  - can corrupt other program's data
- Virtual memory addresses all these problems :
  - all programs share the same memory space, but we can give each program its own virtual memory space >> each program's memory space (virtual) can be separately mapped to the RAM (physical) memory space. With a mapping, you no longer have to tie program memory space to RAM, it can also be linked to disk.

# What is virtual memory ?

- It is all about indirection (interfacing, mapping, abstraction)
- instead of one to one relation between process and memory, a map is used inbetween program address space and RAM address space.
  - Since there is no direct relationship, data can be moved around easily (for example to disk), and RAM memory can be freed up.
  - mapping allows to address the memory segmentation problem by providing each program its own mapping. Segmented memory can be presented as unified.

# How does virtual memory work ?

- virtual memory is based on the separation of memory spaces >> what the program sees is virtual memory, which is a proxy for physical memory (RAM in the computer)
- How does a program access memory ?
  - 1. program executes a load with a virtual address (ex: ld R3, 1024(R0))
  - 2. computer translates the address to the physical address in memory
  - 3. if the physical address is not in memory, the OS loads it from disk
  - 4. the computer then reads the RAM using the physical address and returns the data to the program.

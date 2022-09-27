# Computer Systems : A Programmer's perspective

## 1. A Tour of Computer Systems

ETTC: 4h  
TTC: 3h

### Summary

A **computer system** consists of hardware and systems software that cooperate to run application programs. **Information** inside the computer is represented as groups of bits that are interpreted in different ways, depending on the context. Programs are translated by other programs into different forms, beginning as ASCII text and then translated by **compilers** and **linkers** into binary executable files.  
**Processors** read and interpret binary instructions that are stored in **main memory**. Since computers spend most of their time copying data between memory, I/O devices, and the CPU registers, the storage devices in a system are arranged in a hierarchy, with the CPU registers at the top, followed by multiple levels of hardware cache memories, DRAM main memory, and disk storage. **Storage devices** that are higher in the hierarchy are faster and more costly per bit than those lower in the hierarchy. Storage devices that are higher in the hierarchy serve as **caches** for devices that are lower in the hierarchy. Programmers can optimize the performance of their C programs by understanding and exploiting the memory hierarchy.  
The operating system **kernel** serves as an intermediary between the application and the hardware. It provides three fundamental abstractions: (1) **Files** are abstractions for I/O devices. (2) **Virtual memory** is an abstraction for both main memory and disks. (3) **Processes** are abstractions for the processor, main memory, and I/O devices.  
Finally, **networks** provide ways for computer systems to communicate with one another. From the viewpoint of a particular system, the network is just another I/O device.

#### 1.1

- What is a computer system ?
  - hardware and software that run together to run applications
- What is a source program ?
  - source program is a human readable version of an application
- What is information ?
  - a sequence of bits (data object) that represent different things depending on the context

#### 1.2

- In what form does a source program must be translated for the machine to understand it ?
  - into low-level **machine-language** instructions
- In what form must a program be presented to be run by a computer ?
  - in the form of an **executable object program**, stored as a binary disk file.
- Who is responsible for the translation from source to program file ?
  - compiler
- What are the actors/phases of a compilation system, and what are their destination files ?
  - compilations systems are composed of four phases: preprocessor, compiler, assembler, linker.
    - **preprocessor** : replaces all #include with the actual content of the header file. Produces another C program with the `.i` extension.
      - what is a **header file** ? : A header file is a file with extension `.h` which contains C function declarations and macro definitions to be shared between several source files.
    - **compiler** : takes the preprocessor target file as source and produces and **assembly-language** program with the `.s` extension. Includes low-level machine-language instructions.
    - **assembler** : takes the compiler target as source and produces a **machine-language** instructions packaged as a relocatable object program, with the `.o` extension.
    - **linker** : merges all the references to file imports into the current file (fetches the precompiled object file for imports) and produces an executable.
- Why is assembly language useful ?
  - it provides a common output language for different compilers for different high-level languages.

#### 1.4

- Buses ?
  - Electrical conduits that transport data in chunks between hardware components.
- words and word size ?
  - words are the units of data (fixed-sized chunks of bytes) transported by buses (either 32 or 64)
- I/O devices ?
  - system's connection to the outside world (keyboard, mouse, screen)
- Main memory ?
  - temporary storage device that holds both a program and the data it manipulates while the CPU is executing the program.
- CPU ?
  - executes the instructions stored in main memory and pointed at by the PC (increments counter)
- PC ?
  - word-size storage device that points at (contains the address of) some machine-language instruction in main memory
- Register file ?
  - small storage device that consists of a collection of word-size registers, each with its own unique name
- ALU ?
  - The ALU computes new data and address values.

#### 1.5

- processor/memory gap ?
  - processor are easier to speed up than memory
- Why caching ?
  - making memory faster is hard, so caches hold information that the processor is likely to need in the near future
  - by exploiting locality, we manage to make memory fast (at least for some part of the data needed to run programs)
- Why is caching good ?
  - because moving data accross long distances is slow
- SRAM ?
  - for L1 and L2 caches
- DRAM ?
  - for main memory

#### 1.6

- What is the main idea of memory hierarchy ?
  - n+1 serves as cache for n

#### 1.7

- What are the main abstractions provided by an operating system ?
  - file, process, virtual memory
- What are the OS two main functions ?
  - protect hardware from misuse
  - provide simple interface to communicate easily with hardware devices
- What is a process ?
  - the abstraction for a running program
- What is context switching ?
  - the fact that the CPU switches between various ongoing processes.
  - state of processes is saved (that is the context) and retrieved when needed
- What is context with regards to a running process ?
  - value of PC, register file, contents of main memory
- What is a system call ?
  - when program requires action by the OS, it transfers control to kernel, through a system call. The kernel executes task and returns control back to program.
- What does the kernel manage ?
  - it manages the transition from one process to another
- What is a thread ?
  - an execution unit
- What is virtual memory ?
  - an abstraction for main memory (as if program had permanent and unrestricted access to it)
- What is a file and why is it clever ?
  - an abstraction for I/O. It is useful for developers who do not have to worry about how hardware implementation works. They just deal with one thing.
  - Every I/O device, including disks, keyboards, displays, and even networks, is modeled as a file. All input and output in the system is performed by reading and writing files, using a small set of system calls known as Unix I/O.

#### 1.8

- What is a network ?
  - systems connected to each other

#### 1.9

- What is concurrency ?
  - the fact that several tasks can run at the same time
- What is parallelism ?
  - the use of concurrency to speed up a system
- What is thread-level concurrency ?
  - where multiple programs are executed at the same time
- What is instruction level parallelism ?
  - where multiple instructions are executed at the same time

## Representing and Manipulating Information

ETTC: 10h

Binary representations of numeric values.
Non negative number encoding >> Unsigned encodings
Negative number encoding >> signed encodings (two's complement)
Real number encoding >> floating point encoding

### Information storage

ETTC: 2h

- What is the smallest addressable unit of memory ? >>
- How does a machine-level program view memory ? >>
- How is memory identified ? >>
- What is virtual address space ? >>
- What is a pointer ? >>
- What does the value of a pointer in C correspond to ? >>

#### 2.1.1 Hexadecimal notation

- What does a byte consist of ? >>
- What is a byte's range expressed in decimal, binary and hexadecimal representation ? >>
- Why hexadecimal notation ? >>
- How many values can an hexadecimal representation represent ? >>
- How do you signify an hexadecimal representation to C ? >>
- How do you convert binary to hexadecimal ? >>
- How do you convert decimal to hexadecimal ? >>
- How do you convert a power of two to hexadecimal ? >>

#### 2.1.2 Data sizes

- What does word size correspond to ? >>


#### 2.1.3 Addressing and byte ordering 

- What is the most significant bit ? >> The most significant bit (MSB) is the bit in a multiple-bit binary number with the largest value.
- What is a disassembler ? >>
- What is referencing and dereferencing ? >> 
- In what cases is byte ordering important to consider ? >>


### Integer representation

ETTC: 2h

### Integer arithmetic

ETTC: 2h

### Floating point

ETTC: 2h

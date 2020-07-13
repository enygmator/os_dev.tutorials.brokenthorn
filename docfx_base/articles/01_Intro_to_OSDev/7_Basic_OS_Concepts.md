# Basic Concepts of an Operating system

Looking back though our small trip to memory lane brings some important new terms with it. So far, we only gave "operating system" a small definition. The previous page should help us in defining a better, more descriptive definition of what an operating system is.

Since we now know what features most OSes have in common, to help define them better, lets put the above bolded terms into a list:

- Memory Management
- Program Management
- Multitasking
- Memory Protection
- Fixed Base Address
- Multi-user presence
- Kernel
- File System
- Command Shell
- Graphical User Interface (GUI)
- Graphical Shell
- Linear Block Addressing (LBA)
- Bootloader (From the previous tutorial)

## Memory Management

Memory Management refers to:

- Dynamically giving and using memory to and from programs that request it.
- Implementing a form of **Paging**, or even **Virtual Memory**.
- Insuring the OS Kernel does not read or write to unknown or invalid memory.
- Watching and handling **Memory Fragmentation**.

## Program Management

This relates closely with Memory Management. Program Management is responsible for:

- Insuring the program doesn't write over another program.
- Insuring the program does not corrupt system data.
- Handle requests from the program to complete a task (such as allocate or deallocate memory).

## Multitasking

Multitasking refers to:

- Switching and giving multiple programs a certain timeframe to execute.
- Providing a **Task Manager** to allow switching (Such as Windows Task Manager).
- **TSS (Task State Segment) switching. Another new term!**
- Executing multiple programs simultaneously.

## Memory Protection

This refers to:

- Accessing an invalid descriptor in protected mode (Or an invalid segment address)
- Overwriting the program itself.
- Overwriting a part or parts of another file in memory.

## Fixed Base Address

A "Base Address" is the location where a program is loaded in memory. In normal applications programming, you wouldn't normally need this. In OS Development, however, you do.

A "Fixed" Base Address simply means that the program will always have the same base address each time it is loaded in memory. Two example programs are the BIOS and the Bootloader.

## Multiuser

This refers to:

- Login and Security Protection.
- Ability of multiple users to work on the computer.
- Switching between users without loss or corruption of data.

## Kernel

The Kernel is the heart of the Operating System. It provides the basic foundation, memory management, file systems, program execution, etc. We will take a closer look at the kernel very soon, don't worry 😀

## File System

In OS Development, there is no such thing as a "file". Everything could be pure binary code (from the bootsector); from the start.

A File System is simply a specification that describes information regarding files. In most cases, this refers to Clusters, Segments, segment address, root directories, etc. the OS has to find the exact starting address of the file in order to load it.

File Systems also describe file names. There are **external** and **internal** file names. For example, the FAT12 specification states a filename can only be 11 characters. No more, no less. Seriously. This means the filename "KRNL.sys", for example, will have the internal file name `"KRNL    SYS"`.  
We will be using FAT12 and be discussing it in detail later.

## Command Shell

A Command Shell sits on top the Kernel as a separate program. The Command Shell provides basic input and output through the use of typing commands. The Command Shell uses the Kernel to help with this, and complete low level tasks.

## Graphical User Interface (GUI)

The Graphical User Interface (GUI) simply refers to the graphical interface and interactions between the Graphical Shell and the user.

## Graphical Shell

The Graphical Shell provides video routines and low level graphical abilities. It normally will be executed by the Command Shell. (As in Windows 1.0,2.0, and 3.0). Usually this is automatic these days, however.

## Linear Block Addressing (LBA)

Operating Systems have control over **every single little byte in memory**. Linear Addressing refers to directly accessing linear memory.
For example:

```armasm
mov ax, [0x09000]    ; There is no such thing as Access Violations in OS Development
```

This is a good thing, but is also a very bad thing. For example:

```armasm
mov bx, [0x7bff]       ; or some other address less then 7c00h
mov cx, 10
.loop1:
    mov [bx], 0x0       ; clear bx
    inc bx              ; go to next address
    loop    .loop1      ; loop until cx=0
```

The above code seems harmless. However, if the above code was found in a bootloader, the above code will overwrite itself by 10 bytes. Ouch. The reason is that bootloaders are loaded with a Fixed address of 0x7c00:0, and the above code starts writing from 07bffh: One byte before 07c00h.

## Bootloader

From the previous page, we know that the bootloader is loaded by the BIOS, and is the very first program to execute on power on.

The bootloader is loaded by the BIOS at absolute address **`0x7c00:0`**. After loading, the CS:IP (which you will learn about soon) is set to your bootloader, and the bootloader takes full control.

> [!IMPORTANT]
> A Floppy Sector is only 512 bytes in size. Remember that the bootloader has to fit in a single bootsector. What does this mean? The bootloader is very limited in size, and cannot exceed 512 bytes.

Most of the time, the bootloader will either just load and execute the kernel, or a **Second Stage Bootloader**.

## Conclusion

In the next section we will explore the creation of a stage 1 bootloader by delving into the theory and code behind the process of booting up a machine and executing the bootloader.

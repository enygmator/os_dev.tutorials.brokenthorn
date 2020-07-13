# Getting Setup for OS Development

In developing low level code, we will need specialized low level software to help us out. Some of these tools are not needed, however, they are highly recommended as they can significantly aid in development.

## NASM - The Assembler

The Netwide Assembler (NASM) can generate flat binary 16bit programs, while most other assemblers (Turbo Assembler (TASM), Microsoft's Macro Assembler (MASM)) cannot. During the development of the OS, some programs must be pure binary executables. Because of this, NASM is a great choice to use.

You can download NASM from [here](http://nasm.sourceforge.net/).

## Microsoft Visual C++

Because portability is a concern, most of the code for our operating system will be developed in C.  
During OS Development, there are some things that we must have control over that not all compilers may support, however. For example, say good bye to all runtime compiler support (templates, exceptions) and the good old standard library! Depending on the design of your system, you may also need to support or change more detailed properties: Such as loading at a specific address, adding your own internal sections in your programs' binary, etc.

The basic idea is that not all compilers out there are capable of generating operating system machine/binary code.

I will be using Microsoft Visual C++ for developing the system. However, it is also possible to develop in other compilers such as DJGPP, GCC or even Cygwin. Cygwin is a command shell program that is designed to emulate Linux command shell. There is a GCC port for Cygwin.

You can download Visual Studio [here](https://visualstudio.com/) and then select `Desktop development with C++` workload during it's installation.

## Tool for Copying the Boot Loader

The bootloader is a pure binary program that is stored in a single 512 byte sector. It is a very important program as it is impossible to create an OS without it. It is the very first program of your OS that is loaded directly by the BIOS, and executed directly by the processor.  
We can use NASM to assemble the program, but how do we get it on a floppy disk? We cannot just copy the file. Instead, we have to overwrite the boot record that Windows places (after formatting the virtual/real disk) with our bootloader.  
Why do we need to do this? Remember that the BIOS only looks at the bootsector when finding a bootable disk. The bootsector, and the "boot record" are both in the same sector! Hence, we have to overwrite it.

There are a lot of ways we can do this. Here, I will present two. If you are unable to get one method working on your system, our readers may try the other method.

> [!WARNING]
> Do Not attempt to play with the following software until I explain how to use it. Using this software incorrectly can corrupt the data on your disk or make your PC unbootable.

### PartCopy - Low Level Disk Copier

PartCopy allows the copying of sectors from one drive to another. PartCopy stands for "Partial copy". Its function is to copy a certain number of sectors from one location to another, to and from a specific address.

You can download it from [here](~/resources/OSDev_tools/pcopy02.zip).

### Windows DEBUG Command

Windows provides a small command line debugger that may be used through the command line. There are quite a bit of different things that we can do with this software, but all we need it to do is copy our boot loader to the first 512 bytes on disk.  
Go to the command prompt, and type **debug**. You will be greeted by a little prompt (-):

```powershell
C:\Documents and Settings\Michael>debug
-
```

Here is where you enter your commands. **h** is the help command, **q** is the quit command. The **w (write)** command is the most important for us.  
You can have debug load a file into memory such as, say, our boot loader:

```powershell
C:\Documents and Settings\Michael>debug boot_loader.bin
-
```

This allows us to perform operations on it. (We can also use debugs **L (Load)** command to load the file is we wanted to). In the above example, **boot_loader.bin** will be loaded at address 0x100.  
To write the file to the first sector of our disk, we need to use the **W (Write)** command which takes the following form:

```powershell
W [address] [drive] [firstsector] [number]
```

Okay... so let's see: The file is at address 0x100. We want the floppy drive (Drive 0). The first sector is the first sector on the disk (sector 0) and the number of sectors is ehm... 1.
Putting this together, this is our command to write **boot_loader.bin** to the boot sector of a floppy:

```powershell
C:\Documents and Settings\Michael>debug boot_loader.bin
-w 100 0 0 1
-q
```

## VFD - Virtual Floppy Drive

Weather you have a floppy drive or not, this program is very useful. It can simulate a real floppy drive from a stored floppy image, or even in RAM. This program creates a virtual floppy image, allows formatting, and copying files (Such as, your kernel perhaps?) directly using Windows Explorer.

You can download it from [here](http://sourceforge.net/projects/vfd/).

## Bochs Emulator - PC Emulator and Debugger

You pop in a floppy disk into a computer, hoping that it works. You boot your computer and look in awe at your greatest creation! ...Until your floppy motor dies out because you forgot to send the command to the controller in your bootloader.

When working with low level code, it is possible to destroy hardware if you are not careful. Also, to test your OS, you will need to reboot your computers hundreds of times during development.

Also, what do you do if the computer just reboots? What do you do if your Kernel crashes? Because there is no debugger for your OS, it is virtually impossible to debug.

The solution? A PC Emulator. There are plenty available, two of them being VMWare and Bochs Emulator. I will be using Bochs and Microsoft Virtual PC for testing.

You can download Bochs from [here](http://bochs.sourceforge.net/).

> [!NOTE]
> You do not need to know how to use the software I listed. I will explain how to use them as we start using them.

> [!TIP]
> If you would like to run your system on a real computer that does not have a floppy drive, it is still possible to boot from CD even though it is a floppy image. This is done through Floppy Emulation that which most of BIOSs support.  
> Simply get a CD burning software (I personally use MagicISO) that can create a bootable ISO from a floppy image. Then, simply burn the ISO image to a CD and it should work.

## The Build Process

There are a lot of tools listed above. To better understand how they can be useful, we should take a look at the entire build process of the OS:

- Setting everything up
  1. Use VFD to create and format a virtual floppy image to use.
  2. Set up Bochs Emulator to boot from the floppy image.

- The bootloader
  1. Assemble the bootloader with NASM to create a flat binary program.
  2. Use PartCopy or the DEBUG command to copy the bootloader to the bootsector of the virtual floppy image.

- The Kernel (And basically all other programs)
  1. Assembly and/or compile all sources into an object format (Such as ELF or PE) that can be loaded and executed by the boot loader.
  2. Copy kernel into floppy disk using Windows Explorer.

- Test it!
  1. Using Bochs emulator and debugger, using a real floppy disk, or by using MagicISO to create a bootable CD.

Some of the terms and concepts listed here may be new to you. Do not worry!😀 everything will be explained in the upcoming sections.

The purpose of this section is to create a stepping stone for the rest of the series. This page provides a basic introduction, and a listing of the tools we will be using. I will explain how to use these programs as we need to, so you do not need a tutorial on anything listed here besides what has been listed in the Requirements page.

We also have taken a look at the building process for developing an operating system. For the most part, its fairly simple, however it provides a way to see when the programs listed will be used.

In the next page we are going to go back in time from the first Disk Operating System (DOS) and take a little tour through history. We will also look at some basic OS concepts.

# About Operating Systems and their Development

Operating systems can be a very complex topic. Learning how operating systems work can be a great learning experience.

The purpose of this series is to teach the black art of Operating System (OS) Development, from the ground up. Whether you want to make your own OS, or simply to learn how they work, this series is for you.

## About Operating Systems

An Operating System provides the basic functionality, look, and feel, for a computer. The primary purpose is to create a workable Operating Environment for the user. An example of an Operating System is Windows, Linux, and Macintosh.

If you have never programmed before, computer programming is designing and writing software, or programs, for the computer to load and execute. However, the Operating System needs to be designed with this functionality.

An Operating System is not a single program, but a collection of software that work and communicate with each other. This is what I mean by "Operating Environment".  
Because Operating Systems are a collection of software, in order to develop an Operating System, one must know how to develop software. That is, one must know computer programming.

If you have never programmed before, take a look at the Requirements section below, and look no further. This section will have links to good tutorials and articles that could help you to learn computer programming with C++ and 80x86 Assembly Language.

## Knowledge Requirements for developing OSes

### The C Programming Language

Using a high level language, such as C, can make OS development much easier. The most common languages that are used in OS development are C, C++, and Perl. Do not think these are the only languages that may be used; It is possible in other languages. I have even seen one with FreeBASIC! Getting higher level languages to work properly can also make it harder to work within the long run, however.

C and C++ are the most common, with C being the most used. C, as being a middle level language, provides high level constructs while still providing low level details that are closer to assembly language, and hence, the system. Because of this, using C is fairly easy in OS development. This is one of the primary reasons why it is the most commonly used: Because the C programming language was originally designed for system level and embedded software development.

[Here](2_Programming.md) are some references to learn C Language from.

### The x86 Assembly Language

80x86 Assembly Language is a low level programming language. Assembly Language provides a direct one to one relation with the processor machine instructions, which make assembly language suitable for hardware programming.

Assembly Language, as being low level, tend to be more complex and harder to develop in, then high level languages like C. Because of this, and to aid in simplicity, We are only going to use assembly language when required, and no more.

Assembly Language is another complex language that can take a book to fill. If you do not know x86 Assembly Language, the following may help:

Here is a link to AT&T syntax:

1. AT&T syntax: <https://gist.github.com/DmitrySoshnikov/c67cbde1cceb0d6a194830b41baa5c8b>
2. inline assembly: <https://www.codeproject.com/articles/15971/using-inline-assembly-in-c-c>
3. Intel vs ATT syntax: <https://www.nayuki.io/page/a-fundamental-introduction-to-x86-assembly-programming>
4. inline assembly: <https://ibiblio.org/gferg/ldp/GCC-Inline-Assembly-HOWTO.html>
5. assembly language (Intel syntax / NASM): <https://www.tutorialspoint.com/assembly_programming/>

> [!NOTE]
> The above links are not from the original author. They are links from which I learnt the x86 assembly language. They are pretty good resources for any type of coding you will do in x86 `asm`.

That is all you need to know; Everything else I'll teach along the way.

> [!IMPORTANT]
> From here on out, I will **NOT** be explaining C or x86 Assembly Language concepts. I will however, still explain new instructions that you may not be familiar with, such as `lgdt`, and the use of `sti`, `cli`, `bt`, `cpuid` and some others.
Hope you like it!

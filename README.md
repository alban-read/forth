# FORTH

!WimpForth (Wimp being windows icons mouse and pointers)

This RISC OS FORTH by Martin Läuter is inspired by Win32Forth by Andrew McKewan and Tom Zimmer

- I updated this ever so slightly to get it to work on my 200Mhz RISC PC back in the day.

- I still enjoy RISC OS; and still use this FORTH; these days on a ~~1.5Ghz~~ 2.35Ghz processor. 

- Most recently tested with RISC OS version 5.28 on PI 300 and TI, Also RPCEMU (RO D. 5.27)



Selfie 

![selfie](WimpForth.jpg)

In theory all you need is the source and the Kernel file (which is a binary) to get started.

These can be found in the WF ZIP file for RISC OS.

## Meta Compiler

This FORTH is very interesting since (true to its Win32Forth roots) it is a meta compiler.

From a working kernel this FORTH is able to recompile itself; this is true to the FORTH philosophy; 
and different from many micro (z80, 6502) forths where to bootstrap you needed to use an assembler (if you were lucky); 
or enter the hex into a machine monitor and patch it (I have done that, fun three weeks.)

The idea being  that as long as you have a computer running this FORTH `all` you need to do is re-write the assembler for another architecture; rewrite some kernel code words in that assembler; and re-generate the kernel to the new target system using the meta compiler.

Thanks to the meta-compiler once you have FORTH; FORTH can build your next FORTH, for ever.

I guess that the original author may have done that; probably starting from the PC version this descends from.

This capability has been useful over the years; when updating to run on new versions of the Systems that run RISC OS.

The original author granted permissions to copy and use the software; see !HELP file.


## Rebuild all

Unzip the wf/zip file to your desk.

Start !WimpForth

To completely rebuild 
You can optionally edit and rebuild the kernel.
And then use your new kernel to rebuild the app.

# Kernel

![kernel](step1.jpeg)

From the forth edit window you type fload meta

# Make app

![app](step2.jpeg)

You start the command line kernel and you type fload makewin


To make any changes to the FORTH you just edit the FKERNEL and other files, especially WINDOWS

This app has made its way from the Archimedes to RISC PC then via IYONIX to the TI and PI400 by repeatedly doing the above, making ever so small changes along the way.


## Fun things

The forth interpreter NEXT is only one instuction on the ARM 32.

```FORTH
: next
    >pre ldr pc, [ ip ], # 4
    pre> ;
```


## The assembler supported is classic RISC 

- the built in portable assembler implements just the ARM2 instructions as supported by the Archimedes.  

## Recent History Summary


### In Reverse order - newest first.


Sped up compilation of files; Forth compiles code into its dictionary.  
This means the ARM code cache needs to be synced with the ARM data cache.
This change tells the OS the region to update - from start of FORTH memory &8000 to the end of FORTH memory (WimpSlot) this massively speeds up compilation if the memory allocation is small; the WimpSlot Max is set to 256K which gives 128K free for new user code; enough to load the FKERNEL twice (e.g. to meta compile it.)  Speed increase for fload meta is massive from 00.06.090 to 00.00.059.
For RPC EMU which emulates a RISC PC StrongARM (on a PC or MAC) commenting out syncCode completely is faster. 


Added hardware division (sdiv and udiv) instructions to the assembler (PASM); added s/ and u/ words to use these new instructions.
These instructions are not available on older ARM systems; all the older subtract and shift division words remain untouched.
s/ is 4-5 times faster than /.
These are illegal instructions and will certainly crash on older hardware and on RPCEmu.



Added orange coloured cursor to the edit window, handle caret events, avoid drawing on other peoples windows, fixed bug that sometimes stopped the icon from displaying in the icon bar.









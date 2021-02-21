# FORTH

WimpForth is a RISC OS FORTH created by Martin Läuter for the Acorn Archimedes.

WimpForth runs under the RISCOS desktop and is a freeware Forth system. 

WimpForth is inspired by the public domain Win32Forth created by Andrew McKewan and Tom Zimmer

Current status

- Runs well on RISC OS 5.28 on the new PI 400 with 4GB of memory and 2Ghz+ capable A72 processor.

- Most recently tested with 
   - RISC OS version 5.28 on PI 400 (recommended.)
   - RPCEmu (with Direct pack 5.27)
   - Known to run on other RISC OS systems


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

### Current work in progress

Presently I am gradually adding support for graphics to the FORTH window; the current window was text only.

I have added an optional graphics layer beneath the text and made the text background transparent.

The graphics layer is created using a RISC OS sprite; graphics commands; such as line, rectangle, circle etc; are directed to the sprite and the screen is updated using refresh in the menu; or show at the command line.



### In Reverse order - newest first.

Split Kernel into 26 and 32 bit versions.

Discussed some 26Bit looking code on ROOL forum.

Tried making the kernel 32 bit clean; this involved adding test instructions to a number of words; I tested a 32 bit clean kernel - it was consistently measurably slower.

Although I am interested in running RISCOS 5.28 and above on modern ARM processors; I dont want to prevent earlier systems from also working.

Presently I have split the kernel for 26 bit and 32 bit.
There is no significant performance difference between these two kernels.
Both kernels work on the 32bit systems that I have tested.
Only the 26bit kernel would work on a 26 bit operating system.

I imagine there may be potential scenarios where chopping parts out of the address space could cause issues on a 4GB 32 bit system; but in practice forth code is not likely to use much more than a few megabytes of space starting at 32K.

Added editor support to invoke stronged on a file or word.


Added some benchmarks to benchmark the interpreter.
These incidentally confirm that the A72 in the overclocked PI 400 is fast.


Added a build script (makerpcemu) for users of RPCEmu.


Fixed an issue with the ErrorBox test routine, that could crash the app.



Made a cache sync change that speeds up compilation of files; recall that FORTH compiles code into its dictionary.  
This means the ARM code cache needs to be synced with the ARM data cache.
An update happens every time a FORTH word is added; words are small; and words are only added to the end of the dictionary.
So the update region is now set to the 8K below the dictionary pointer.
Speed increase for fload meta on PI400 is massive going from 00.06.090 to 00.00.07 (from six seconds to essentially instant.)
For RPC EMU which emulates a RISC PC (on a PC or MAC) commenting out syncCode completely is an option.



Added hardware division (sdiv and udiv) instructions to the assembler (PASM); added s/ and u/ words to use these new instructions.
These instructions are not available on older ARM systems; all the older subtract and shift division words remain untouched.
s/ is 4-5 times faster than /.
These are illegal instructions and will certainly crash on older hardware including RPCEmu.



Added orange coloured cursor to the edit window, handle caret events, avoid drawing on other peoples windows, fixed bug that sometimes stopped the icon from displaying in the icon bar.

## Download

There is a zip file included in this repo.

## Details 

Important features of WimpForth 
 * ANS compliant
 * source level debugger, decompiler
 * ARM assembler/disassembler (not difficult to extend.)
 * object orientation like Yerk on the Macs teached the forthers
 * window, icon, control, dialog, menu... classes to
   make programming Windows as easy and controllable as possible
 * variable number of threads in vocabularies
 * strong WORDS implementation
 * easy invocation of CLI commands, time control, system variables
 * local labels
 * Wimp interface
 * Drag and drop Filer->Forth window will load forth files.
 * reads normal text files with 16K buffer
 * full source included
 * low memory footprint.

limitations

* is an interpreter, not an optimizing or subroutine threaded inlining compiler.
* has integer words, does not support VFP, NEON or other ARM FP instructions.
* does not support new complex ARM instructions.
* not ported to Linux or Windows, depends on RISC OS. 






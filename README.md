# FORTH

!WimpForth (Wimp being windows icons mouse and pointers)

This RISC OS FORTH by Martin Läuter is inspired by Win32Forth by Andrew McKewan and Tom Zimmer

I updated this ever so slightly to get it to work on my 200Mhz RISC PC back in the day.

I still run RISC OS; and run this FORTH; these days on a ~~1.5Ghz~~ 2.4Ghz processor. 

Presently has some bugs with the CARET display.


Selfie 

![selfie](WimpForth.jpg)



In theory all you need is the source and the Kernel file (which is a binary) to get started.

These can be found in the WF ZIP file for RISC OS.

This FORTH is very interesting since (true to its Win32Forth roots) it is a meta compiler.

From a working kernel this FORTH is able to recompile itself; this is true to the FORTH philosophy; 
and different from many micro forths where the kernel needed you to use an assembler (if you were lucky); 
or enter the hex into a machine monitor (I have done that.)

The idea being  that as long as you have a computer running this FORTH `all` you need to do is re-write the assembler for another architecture; rewrite some kernel code words in that assembler; and re-generate the kernel to the new target system using the meta compiler.

Thanks to the meta-compiler once you have FORTH; FORTH can be used to bootstrap the next FORTH, for ever.

I guess that the original author may have done that; probably starting from the PC version.

This has been useful over the years; even when updating to run on new versions of the Systems that run RISC OS.

In any event I still enjoy and use this FORTH; for poking around my ARM based system.

The original author granted permissions to copy and use the software; see !HELP file.


## Rebuild all

Unzip the wf/zip file to your desk.

Start !WimpForth

To completely rebuild 
You can rebuild the kernel.
And then use the kernerl to rebuild the app.

# Kernel

![kernel](Step1.jpg)

# Make app

![kernel](Step2.jpg)


To make any changes to the FORTH you just edit the FKERNEL and other files, especially WINDOWS

This app has made its way from the Archimedes to RISC PC IYONIX and finally the PI400 by repeatedly doing the above, making small changes along the way.


## Fun things

The forth interpreter NEXT is one instuction on the ARM 32.

The assembler supported is very RISC - the built in portable assembler implements the ARM2 instructions as supported by the Archimedes.  










# FORTH

!WimpForth (Wimp being windows icons mouse and pointers)

This RISCOS FORTH by Martin Läuter is inspired by Win32Forth by Andrew McKewan and Tom Zimmer

I updated this ever so slightly to get it to work on my 200Mhz RISC PC back in the day.

I still run RISC OS; and run this FORTH; these days on a 1.5Ghz processor.

In theory all you need is the source and the Kernel file (which is a binary) to get started; not tested that this works; will that.

This FORTH is interesting as it (true to its Win32Forth roots) is a meta compiler.

From a working kernel this FORTH is able to recompile itself; this is true to the FORTH philosophy; 
and different from many micro forths where the kernel needed you to use an assembler (if you were lucky); 
or enter the hex into a machine monitor (I have done that.)

The idea being  that as long as you have a computer running this FORTH `all` you need to do is re-write the assembler for another
architecture; rewrite some kernel code words in that assembler; and re-generate the kernel to the new target system using the meta-
compiler.

I guess that the original author may have done that; probably starting from the PC version.

In any event I still enjoy and use this FORTH; for poking around my ARM based system.






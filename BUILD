\ BUILD.F               New design for Defining Words           by Tom Zimmer
\                       (As derived from FORML 1995)

cr .( Loading Experimental BUILD DO: defining wordset.. ) 

: build"        ( -<name>- )    \ the building part of a defining word
                header
                ((")) count pocket place
                pocket ?uppercase find 0= ?missing
                execute , ;

: ,word         ( -<name>- )    \ lay a word into the dictionary, aligned
                bl word count                   \ "name"
                here over 1+ allot              \ allocate the space
                place 0 c, align ;              \ lay in the name+NULL

: build         ( -<name>- )    \ makes words that define other words
                ?comp                           \ only while compiling
                compile build" ,word ; immediate

: do:           ( -<name>- )
                create hide !csp dodoes call, ] ;


\S
\ ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
\       A simple example of the new defining word mechanism
\ ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

\ first, define the BUILDING part of the defining word

: const         ( n1 -<name>- )
                build doconst , ;

\ later, define the EXECUTION part of the defining word

do: doconst     ( a1 -- n1 )
                @ ;

2 const two




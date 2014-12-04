Overview
========

LuaDec for Lua 5.1 is a Lua decompiler targeting lua versions 5.1.x

It is based on Hisham Muhammad's luadec which targeted lua 5.0.x

LuaDec51 is free software and uses the same license as the original LuaDec

It currently has the following functionality:

* Full support for Lua 5.1 opcodes
* Added support for files with debug informations stripped
* Includes a heuristic that tries to determine where locals have been declared
* When it encounters something undecompilable it tries to continue with the decompilation
* It has a built in disassembler, with easy to read disassembly
* It includes two ruby based tool that help further correction of the decompiled scripts

Status
------

Current version is 2.0

Currently luadec51 can decompile most constructs of lua scripts, including scripts that have debug informations stripped. It still has some shortcomings:
* Complex conditional expressions usually break the output
* while and repeat..until loops are unhandled
* The local decalration guesser usually guesses locals declaring NEWTABLE and SETLIST opcodes wrong

Planned for luadec 3.0:
* A new conditional handling engine

Usage
-----

To use luadec you have to compile it first. Read the following sections for more information

To use the ruby based tools compare and luadecguess you need to have ruby version 1.8 installed on your computer as well

To simply decompile a script run luadec as following:

    luadec filename.luac > filename.lua

This should decompile filename.luac to filename.lua

To disassemble a file use the -dis option:

    luadec -dis filename.luac

There are some more options, usually for debug purposes, or for cases where the built in local guesser guesses wrong.
Use -h to get a complete list of usable parameters

Download
--------

The source code of LuaDec 5.1 and windows binaries can be downloaded from the GitHub page. You can find windows binaries under
the Releases tab. You might need to have the Visual Studio 2013 C++ redistributables installed for the project to work.

Compiling
---------

You need to download a version of lua you want to use, and put it into the lua directory. After that you can use the Makefile
in the build directory to compile both projects. Alternatively there is also an MSVC directory which contains a Visual Studio 2013
project file you can use to compile luadec.

There is also a set up luadec project for MSVC++ 2008, that uses a modified lua 5.1.4 version with unicode support at
http://winmo.sztupy.hu/luadec.html. Do not use this project tree for usage with generic lua files, because it won't work (it
will expect numerals in Q24.8 format, and strings in unicode)

Binaries
--------

There are currently two separate binaries provided for lua 5.1. Both are windows binaries, and both contain lua 5.1.4
binaries (intperpreter and compiler) too

The generic lua 5.1 version can be found at the project's download page
The unicode mobile version used in HTC phones can be found at http://winmo.sztupy.hu/luadec.html
If you have compiled luadec for some other lua 5.1 version or operating system, then feel free to contact me,
so I can add them to the project

Changelog

LuaDec 2.0.2 [4/Dec/2014]
* Minor fixes for the `{...}` construct
* Makefile for generic builds

LuaDec 2.0.1 [17/May/2012]
* Fixes for handling unknown upvalues

LuaDec 2.0 [10/Mar/2009]
* LuaDec has now a built-in heuristic to determine local declaration and releases
* Luadec has an option to output the LDS2 string of a file

LuaDec 1.9
* Some changes regarding LDS(2) strings and for loops (it's still a bit unstable)
* LuaDec has a new option to disassemble instead of decompile

LuaDec 1.0
* fixed OP_TFORLOOP handling
* added LDS2 functionality to luadec

LuaDec beta 6
* fixed a crash where luadec encounters unhandled boolean constructs
* luadecguess has now a new heuristic called "fast guess" for large scripts

LuaDec beta 5
* luadecguess can now be parameterized, and is more powerful

LuaDec beta 4
* fixed upvalue handling
* fixed some local variable handlings
* added luadecguess: a local variable declaration place guesser

LuaDec beta 3
* fixed OP_TFORLOOP
* fixed loop variable handings
* added command line options to handle local variable declarations (LDS strings)

LuaDec beta 2
* added some workarounds for the crashes. Luadec might output lots of garbage lua code, but it tries not crashing
* fixed OP_TEST (hopefully)

LuaDec beta 1
* Corrected OP_FORPREP - OP_FORLOOP
* Added some more warnings
* Added automatic local variable declarations where possible

alpha 2
* Fixed constant loading errors
* fixed function variables
* Added handlers to the new opcodes
* Some changes to OP_TEST

alpha 1
* Initial Version

Credits
-------

LuaDec51 is based on Hisham Muhammad's luadec

The internals of Lua5.1 was learned from Kein-Hong Man's A No-Frills Introduction to Lua 5.1 VM Instructions

Also thanks to anyone involved in helping me on XDA

Contact us
----------

Contact information at http://winmo.sztupy.hu

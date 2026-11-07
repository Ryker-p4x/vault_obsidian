## Overview:

The compiling process has a lot of steps:
1. The .cpp file gets sent to the preprocessor which will read all the [[Preprocessor Directives (unfinished)]] and decide what to do with them and turn the .cpp into a .i file which is basically like a tree.
2. After the preprocessor decides what to do with the directives it'll get sent to a compiler which will turn the code into a .s file which will be just assembly code on what to do. The way it does this is it reads it with a tree structure called Abstract Syntax Tree (AST) to understand how the code works.
3. Then after the file gets turned into assembly code it gets sent to an assembler (ASM) which will turn the code into binary unreadable code that the computer can read which is an .o file. (object file).
4. Finally, a linker will connect all the object files and combine them into one single executable file.

Each kind of file has its own way to be read/generated:
- .i files can be generated through g++ with the -E flag and can simply be read through jsut opening them.
- .s files can be read normally since they are just assembly code 
- .o files can't be normally read since they are binary code they require a tool called objdump with the flag -d to translate back to assembly code
- executable files can't be read normally but they can be analyzed through dissasemblers and reverse-engineering tools.

We also learned about using [[xdot]]
And we used [[g++]]


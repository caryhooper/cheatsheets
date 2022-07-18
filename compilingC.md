# Compiling & Cross-Compiling
======

## C
------
#### 32bit Compile
i686-w64-mingw32-gcc hello.c -o hello32.exe
#### 64bit Compile
x86_64-w64-mingw32-gcc hello.c -o hello64.exe
#### Example
i686-w64-mingw32-gcc hello.c -o hello.exe -lws2_32 
#### Strip Symbols, No DEP, No Stack Canaries, Don't compile as a Position Independent Executable
gcc -no-pie -m32 -fno-stack-protector -z execstack prog.c -o prog; strip prog..//
#### Compile with Static Library
gcc dcow.c -o dirty -pthread -lcrypt -static

## C++
------
#### 32bit Compile
i686-w64-mingw32-g++ hello.cc -o hello32.exe
#### 64bit Compile
x86_64-w64-mingw32-g++ hello.cc -o hello64.exe

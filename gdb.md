# GDB & Reversing Notes
======
#### gdb-peda
git clone https://github.com/longld/peda.git ~/peda; echo "source ~/peda/peda.py" >> ~/.gdbinit

## GDB Commands
------
#### b main
Break when the program enters main()
#### info functions
List functions within binary
#### x/50i <function>
lists the first 50 instructions of a function.
#### b \*0x4006f3
create breakpoint at memory address
#### si
(unk)
#### pattern_create
invokes ruby "pattern_create" module
#### Set Arguments
set args $(python -c 'print("\x41"\*120')
#### Set Environment Variable
set env $(python -c 'print("\x41"\*120')
#### View Core Dump in GDB
gdb -q -c core
#### Change from ATT to Intel Syntax
set disassembly-flavor intel
#### Dump Assembly Instructions of the function
diass <function>
#### Pause execution when the function given is reached
break <function>
#### Print contents of a Register and Other Variables
print $eip
#### Examine memory locations
x/<int>i <mem-address>; x/20i 0x8048248
#### Print Contents and State of Registers and Other Variables
info registers
#### Continue Execution after Breakpoint
c (or continue)
#### Step One Instruction
si
#### Create Break Point At Address
break \*0x07048524
#### Run GDB with No Extensions
gdb --nex ./file
#### List all Functions
info func
#### Clear Out Arguments
set args
#### Run with Arguments
run AAAA
#### Examine Argument at EIP
x/i $eip
#### Read a String in Memory (at address at EAX)
x/s $eax
#### See Contents of a Single Register
info reg eax
#### See Call Stack / Function Backtrace (and see return addresses on the stackx)
bt 
#### Change assembly Syntax Used
set disassembly-flavor {intel,att}
#### List Breakpoints
info breakpoints
#### Delete a Breakpoints
del breakpoint 
#### View 10 words in hex at a memory location
x/10wx 0xdeadbeef
#### Breakpoint on a Relative Memory location
break \*main+39
#### Examine next 16 instructions
x/16i $eip
#### Custom Arguments
run `python -c 'print("foobar")'`
#### Custom Input
run <<(python -c 'print("AAAA")')
#### Turn on Core dumps 
ulimit -c unlimited
#### Read memory addresses Surrounding ESP
x/40wx $esp-0x268
#### Find memory address of LibC function
print system
#### Set a Relative Breakpoint to a Function
break \* functionname+60
#### Open a Shared Object (.so) File


## objdump
------
#### Disassemble a File
objdump -d
#### Display Section Headers
objdump -h
#### Specify a Section
objdump -j <section name>
#### Display Dynamic Relocation Records (GOT addresses)
objdump -R

## Readelf
------

## gdb-PEDA
------
#### Find PEDA help
help peda
#### Find all references to a function
xrefs <funciton>
#### Create a unique shellcode pattern
pattern_create 300
#### Look for all JMPs or Calls
jmpcall
#### Convert hex to ASCII
print (char []) 0x24424142
#### Find offset of Buffer
pattern_offset BAB$
#### Note
Calling a program with its shortened path vs full path changes the memory alignment of a program.  
#### Turn ASLR On
ASLR on
#### Search Memory for a Strin
searchmem BBBBBBB

## gef
------

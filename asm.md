# ASM Commands/Patterns
======

## Background Info
------
#### ESP
Points to the top of the stack
#### EBP
Used to calculate an address relative to another address.  Aka frame pointer.
#### push
Pushes data on top of the stack.  Only changes the value of ESP.  
#### pop
removes data from the top of the stack.  Only changes the value of ESP.

## Commands
------
#### mov eax,[ebp+10h]
Move a dword from 16bytes (hex 10) down the stack into EAX.

## Turn Shellcode into ASM
------
#### Shellcode to ASM
echo -n "\x31\xC0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x50\x53\x89\xe1\xb0\x0b\xcd\x80\x0a" | ndisasm -u -
#### Cyberchef
+ From Hex "\x"
+  To Hex " "
+  Disassemble x86


## Simple Egghunter
------
#### Egghunter delimited by w00tw00t egg
"\x66\x81\xCA\xFF\x0F\x42\x52\x6A\x02\x58\xCD\x2E\x3C\x05\x5A\x74\xEF\xB8".;

#C Programming
The C Programming Language (Kernighan/Ritchie) 2nd Ed.
##Compiling/Running
- Using Visual Studio "C++ Build Tools"
- Need a Developer Command Prompt ("Developer Command Prompt for VS 2019")
- "cl"

##Key C Concepts
- Every program must have a main().  "main" is special.  Typically, it will call other functions, both standard lib functions or scustom ones.
- Inter-function communication
	* Provide a list of arguments to the function.
- Certain chars need to be escaped: \\, \t, \b, \n, \"
- Variables mus be declared before they are used
	* types: int, float, char, short, long, double, || arrays, structures, unions, pointers, functions
	* long is at least 32 bits

- Define constants in a #define statement delimited by tabs (#define CONST number)

##Operators
- ++ and -- may be used to increment or decrement.  They may be prefix (++nc) or postfix (nc++)

##for loops
for loop consists of the following:
for (variable = start_val; variable <= end_cond; variable = variable + step){
	do_things;
}
for loops must have a body, either within {} or next line as a tab (null statement ";")

##while loops
while loop consists of the following:
while (variable > end_cond){
	do_things;
}
while ((c = getchar()) != EOF){
	putchar(c);
}

##Functions
function definitions can appear in any order
return-type function-name(parameter declarations, if any){
	declarations
	statements
}
The names of parameters are only local to power and not visible to any other function.  
int power(int m, int m);

##getchar and putchar
- getchar reads next input character in text stream and returns its value
- putchar prints the contents of the integer variable as a character, usually to the screen
# Bash Tricks
======
#### Ref
https://guide.bash.academy/expansions/
#### Definition
bash wraps the kernel so you can launch processes

## Logic
------
#### and
if [ -r 1 ] && [ -s 2 ]
#### or
if [ $USER == 'bob' ] || [ $USER == 'andy' ]
#### for loop
```

for i in $(cat countries.txt); do 
	echo -n ${i:0:1} | tr '[:lower:]' '[:upper:]';
	echo ${i:1}; 
```
#### for loop
for i in $(seq 1 10); do echo $i; done
#### for loop
for ((i=1;i<10;i++)); do echo $i; done
#### if statement
if [ <test> ]; then echo foo; fi
#### if-elif statement
```

if [ <test> ]; 
then 
	echo 1; 
elif [ <test2> ]; 
then 
	echo 2; 
else 
	echo 3; 
```
#### if directory exists
if [ -d <directory> ];
#### if file exists
if [ -f <directory> ];
#### if symbolic link exists
if [ -L <directory ];
#### case statements
```

case $1 in 
	start) 
		echo start;; 
	stop) 
		echo stop;;
	restart) 
		echo restart;; 
	*) 
		echo no clue;; 
```
#### while statements
while [ <test> ]; do echo 1; done
#### Read one line at a time
<file while read; do echo "$REPLY"; done
#### Read one line at a time
<file while read line; do echo "$line"; done

## Tests and Conditionals
------
#### simple test
if [[ $REPLY = y ]]; then echo 1; fi

## Shell Expansion
------
#### Asterix (*)
matches any text or no text
#### Question Mark (?)
matches a single character
#### Char Set ([chars])
matches single character as long as its within the set
#### Character Classes [[:classname:]]
alnum, alpha, ascii, blank, cntrl, digit, graph, lower, print, punct, space, upper, word, xdigit
#### Tilde Home Path (~)
Expands to current user's home directory (i.e. /home/user)
#### Arbitrary fd Redirection
+ exec 3<&gtl"Hi Mom"
+  cat <&3


## Extended Glob
------
#### Use
When multiple patterns are needed to be used.
#### +(pattern | pattern)
Matches when any of the patterns appears at least once
#### *(pattern | pattern)
Matches when patterns appear at least once or not at all (what the heck?)
#### ?(pattern | pattern)
Matches once or not at all
#### @(pattern | pattern)
Matches when any of the patterns appear exactly once
#### !(pattern | pattern)
Matches only when none of the patterns appear
#### Example 1
ls *.jp?(e)g
#### Example 2
ls *.@(jpg|jpeg)

## Command Substitution (helpful for injection)
------
#### $(cat /etc/passwd)
Launches command in subshell (new bash process)
#### `cat /etc/passwd`
Deprecated syntax for same thing

## Shell Variables and Parameter Expansion
------
#### var1=myname
echo "My name is $name"
#### contents="$(cat hello.txt)"
echo "Contents here: ${contents}<--end of file"
#### name=Britta time=23.73
echo "$name's current record is ${time%.*} seconds and ${time#*.} hundredths."
#### more expansion
echo "PATH currently contains: ${PATH//:/, }"

## Parameter Expansion Examples (Input - https://hooperlabs.xyz/h00p.html)
------
#### ${parameter#pattern}
Remove the shortest string that matches pattern (start) "${url#*/}" /www.hooperlabs.xyz/h00p.html
#### ${parameter##pattern}
+ Remove the longest string that matches pattern (start) "${url##*/}" h00p.html

#### ${parameter%pattern}
Remove the shortest string that matches the pattern (end) "${url%/*}" https://www.hooperlabs.xyz
#### ${parameter%%pattern}
Remove longest string matching pattern (end) "${url%%/*}" https:
#### ${parameter/pattern/replacement}
Replace first string matching pattern "${url/./-}" https://www-hooperlabs.xyz/h00p.html
#### ${parameter//pattern/replacement}
Replace each string matching pattern "${url//./-}" https://www-hooperlabs-xyz/h00p.html
#### ${parameter/#pattern/replacement}
Replace string matching pattern (start) "${url/#*:/http:}" http://www.hooperlabs.xyz/h00p.html
#### ${parameter/%pattern/replacement}
Replace string matching pattern at end "${url/%.html/.jpg}" https://www.hooperlabs.xyz/h00p.jpg
#### ${#parameter}
Expand length of the value (in bytes) "${#url}" 36
#### ${parameter:start:length}
Expand part of value starting at start, length bytes long "${url:7}" www.hooperlabs.xyz/h00p.html
#### ${parameter[^|^^|,|,,]pattern}
Expand the transformed value, either upper or lower (first char or all chars) of string that matches the pattern. "${url^^[ht]}" HTTps://www.Hooperlabs.xyz/h00p.HTml
#### echo ${PATH//:/ }
Substitute : for spaces in $PATH.
#### {1...10}
numbers in sequence (separated by spaces)
#### {01..10..2}
count by twos

## Special Parameters (History Expansion)
------
#### "$1"
first positional parameter
#### "$*"
expands single string, joining all parameters into one, separated by $IFS
#### "$@"
expands the positional parameters as a list of separate arguments
#### "$#"
expands into a number indicating the number of positional parameters
#### "$?"
expands the exit code of last command (0 means success)
#### "$-"
expands the set of option flags currently active in shell
#### "$$"
expands PID for current shell process
#### "$!"
expands unique PID foir last process started in background
#### "$_"
expands to the last argument of previous command
#### "!!"
expands to full previous line
#### "echo !:2"
expands to second argument of last command
#### "!-2"
second command in history
#### "!:2-5"
all but first argument of last command
#### "~+"
current working directory
#### "~-"
old working directory

## Shell Variables
------
#### BASH
full pathname of command that started the current bash shell
#### BASH_VERSION
active version of bash
#### BASH_VERSIONINFO
array of detailed info about current version of bash
#### BASH_SOURCE
filenames of the scripts currently running (usually empty)
#### BASHPID
PID of the bash that is parsing script code
#### UID
uid of user within bash shell
#### HOME
pathname of the home directory
#### HOSTNAME
name of computer
#### LANG
preferred language category
#### MACHTYPE
full description of type of system
#### PWD
pathname to current directory
#### OLDPWD
pathname of directory you were in before
#### RANDOM
expands random number between 0 and 32767
#### SECONDS
number of seconds bash shell has been active
#### LINES
contains height (rows) of terminal display
#### COLUMNS
contains width (single char spaces) of single row in display
#### IFS
"Internal Field Separator" - bash uses this for word-splitting of data.  By default, spaces, tabs, and newlines
#### PATH
List of paths bash will search for executable programs when a command is run.
#### PS1
Contains string that describes what the prompt should look like
#### PS2
describes what the secondary prompt will look like

## Arrays
------
#### array
files=( myscript hello.txt "foo bar.txt" ); rm -rv "${files[@]}"
#### array (caution)
Use quotes around array!!! don't use ${files[@]}
#### array append
files+=( selfie.png )
#### array patterns
files=( *.txt )
#### array first element
echo "${files[0]}"; echo "$files"
#### array remove element
unset "files[3]"
#### array number of elements
echo "${#files[@]}"
#### array retrieve some elements
echo "${names[@]:1:2}"; echo "${names[@]: -2}"

## Sed
------
#### Return all text between two words
sed -n -e '/BEGIN/./END/ p'
#### Substitute string for another (and delete first line)
sed -e 1d -e s/foo/bar/g /tmp/foo
#### Substitute string for another (and delete first line)
sed '1d; s/foo/bar/g' /tmp/foo
#### Delete lines from file containing string
sed -i '/192\.168\.0\.1/d' /var/log/apache2/access.log

## Awk
------
#### Use awk as cut
echo a,b,c,d,e | awk -F, '{print $1 $2 $3 $5}'

## Grep
------
#### Grep through Binary Filesystem
grep -a "SearchMe" /dev/sd*
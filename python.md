# Python
======
#### Curriculum
Automate the Boring Stuff (by Al Sweigart)

## Basics
------
#### Invoke Python from the Commandline
+ Note: on both Windows and Linux, the python program must be in your PATH.
+   python --version
+  python3 --version
+  python2 --version

#### Interactive Python shell
python3 -i

## Expressions
------
#### Exponent
**
#### Modulus/remainder
%
#### Integer Division/Floored Quotient
//
#### Division
/
#### Multiplication
*
#### Subtraction
-
#### Addition
+
#### Augmented Assignment Operators
+ spam += 1
+  spam -= 1
+  spam *= 1
+  spam /= 1
+  spam %= 1
+ 


## Variable Names
------
#### Rule 1
Variable may only be one word
#### Rule 2
Only letters, numbers, and the underscore
#### Rule 3
Cannot begin with a number
#### The "None" Value
None represents the absence of a value.  None is the only value of the NoneType data type.  Similar to null in other programming languages. 

## Comparison Operators
------
#### Equal To
==
#### Not Equal To
!=
#### Less Than
<
#### Greater Than
>
#### Less Than or Equal To
<=
#### Greater Than or Equal To
>=
#### Boolean AND
and
#### Boolean OR
or
#### Boolean NOT
not

## Flow Control
------
#### IF Statement
```
if name == "Mary":
print("Hello Mary")
```
#### ELSE Statement
```
if name == "Mary":
	print("Hello Mary")
else:
print('Hi, Alice!')
```
#### ELIF Statement
```
if name == 'Alice':
	print('Hi Alice')
elif age < 12:
print('You are not Alice, kiddo!')
```
#### WHILE Loop
```
spam = 0
while spam < 5:
	print('Hello World!')
spam = spam + 1
```
#### Break statement
+ break
+  immediately exits the while loop clause.

#### Continue statement
+ continue
+  program execution immediately jmps back to the start of the loop and reevaluates the loop's condition.

#### FOR Loop
```
print('My name is')
for i in range(5):
print(f'Jimmy Five Times ({i})')
```
#### Importing modules
+ import random, sys, os, math
+  Immediately imports a module. Each module is a Python program that contains a related group of functions that can be embedded in your programs.

#### End a Program Early
import sys; sys.exit()

## Functions
------
#### Define a Block of Code within a Function
```
def hello(name):
	print(f'Hello ' + name)
hello('h00p')
```
#### Return statement
+ return
+  the return value is what the function expression evaluates to.  

#### Keyword Arguments
+ Identified by the keyword put before them in a function call.
+  print('hello', end='')


## Rules for Scope
------
#### Local Scope
Parameters and variables that are assigned in called function.
#### Global Scope
Variables assigned outside all functionas exist in the global scope.
#### Rule 1
Code in the global scope cannot use any local variables.
#### Rule 2
A local scope can access global variables.
#### Rule 3
Code in a function's local scope cannot use variables in any other local scope.
#### Rule 4
You can use the same name for different variables if they are in different scopes. 
#### Global Statement
+ global
+  used if you need to modify a global variable from within a function.


## Exception Handling
------
#### Exception
An error occurring within the program.
#### Try/Except Statements
```
def spam(divideBy):
	try:
		return 42 / dividedBy
	except ZeroDivisionError:
print('Error: Invalid Argument')
```

## Lists
------
#### list
a value that contains multiple values in an ordered sequence.
#### Get first item in list (index 0)
my_list[0]
#### Get last item in list
my_list[-1]
#### Get second to last item in list
my_list[-2]
#### Get first two items of list (slice)
my_list[:2]
#### Get all but last items of list (slice)
my_list[0:-1]
#### Change a value in a list
my_list[1] = 42
#### List concatenation
list1 + list2
#### Remove Value from List
del my_list[1]
#### The IN operator
+ in
+  "string" in my_list

#### The NOT IN operator
+ not in
+  "string" not in my_list

#### Multiple Assignments
```
cats = ['Andy', 'Betty', 'Carl']
cat1, cat2, cat3 = cats
```
#### Find Value in a List
my_list.index('Andy') #Returns '0'
#### Add Value to a List
my_list.append('Daryll')
#### Add Multiple Values to List
my_list.extend(['foo','bar'])
#### Add Value to Start of List
my_list.insert(0,"foobar")
#### Insert Value in a List
my_list.insert(1,'Azelle')
#### Remove Value in a List
my_list.remove('Carl')
#### Remove Last Value in a List and Save
last_item = my_list.pop()
#### Sort Values in a List
my_list.sort(reverse=True)
#### Sort Strings in List (case independent)
my_list.sort(key=str.lower)
#### String (immutable)
list of single text characters
#### Tuple
+ 1. Typed with parentheses
+  2. Immutable (cannot have values appended or removed).

#### References
Lists are actually references to a variable (pointer).  Assigning another variable to the list variable actually just creates another pointer to the same data!
#### Copy module (copies list, not just reference)
```
import copy
spam = [1,2,3]
cheese = copy.copy(spam)
cheese[42]
```
#### Copy module - deepcopy
cheese = copy.deepcopy(spam)  # This also copies lists of lists.

## Dictionaries
------
#### Dictionary
Collection of many values.  Like a list but instead of sequential integer indices, indices may be any values.  Indicies are called keys and the key with its associated value is called a "key-value pair".
#### Get value with key
my_dict['key1']
#### keys() method
returns a list of all keys within a dict (i.e. my_dict.keys())
#### values() method
returns a list of all values within a dict (i.e. my_dict.values())
#### items() method
returns a list of tuples of (key,value) (i.e. my_dicts.items())
#### Check whether a key or value exists in a dictionary
'Zophie' in spam.values()
#### Get a value from a dict without causing an error
my_dict.get('doesntexist','defaultvalue')
#### Set a default for a value within a dict in case it doesnt exist
```
spam = {'name':'Rosie','age':5}
spam.setdefault('color','black')
```

## Pretty Printing
------
#### Print dicts in a human readable manner
```
import pprint
pprint.pprint(my_dict)
```
#### Alternately, preformat the dict so it can be regularly printed
```
import pprint
print(pprint.pformat(my_dict))
```

## Escape Characters
------
#### Single Quote
\'
#### Double Quote
\"
#### Tab
\t
#### Newline
\n
#### Backslash
\\

## String Manipulation
------
#### Strings can stretch multiple lines with triple quotes
```
'''Dear Alice,
Eve's cat has been arrested.

Sincerely,

Bob''
```
#### Multiline Comments
User triple quotes by themselves to delimit multiline comments.
#### Uppercase string
my_string.upper()
#### Lowercase string
my_string.lower()
#### Determine if string is uppercase
my_string.isupper()
#### Determine if string is lowercase
my_string.islower()
#### Determine if string is only letters and not blank
my_string.isalpha()
#### Determine if string only consists of letters and numbers and is not blank
my_string.isalnum()
#### Determine if string is only decimal chars and not blank
my_string.isdecimal()
#### Determine if string is only whitespace
my_string.isspace()
#### Determine if a string consists of only words that begin with an uppercase letter followed by lowercase letters.
my_string.istitle()
#### Determine if string starts with letters
my_string.startswith('ABC')
#### Determine if string ends with letters
my_string.endswith('XYZ')
#### Join a list of strings
', '.join(['foo','bar','baz'])
#### Split a list of strings on a delimiter
'MyABCnameABCisABCSimon'.split('ABC')
#### Justify Text Right
'Hello'.rjust(10,'-')
#### Justify Text Left
'Hello'.ljust(10,'*')
#### Justify Text Center
'Hello'.center(20,'=')
#### Remove leading whitespace
'  Hello'.lstrip()
#### Remove all leading and trailing whitespace
'   Hello  '.strip()
#### Remove all leading and trailing characters
'\n\nHello\n\n\n\n'.strip('\n')
#### Copy and Paste Strings with pyperclip
```
import pyperclip
pyperclip.copy('Hello World!)
pyperclip.paste()
```
#### Reverse a String
my_string[::-1]
#### Substring of first 5 Characters
my_string[:5]
#### All but first 5 characters
my_stringp[5:]
#### Substring of last 5 Characters
my_string[-5:]
#### All but last 5 characters
my_string[:-5]
#### Convert Sentence to List
foo.split(" ")

## Regular Expressions
------
#### Basic Regex (phone number regex object)
```
import re
phoneNumRegex = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
```
#### Search regex
+ mo = phoneNumRegex.search('My number is 555-555-5555.')
+  print(mo.group())

#### Grouping with Parentheses
Adding parentheses will create "groups" in the regex.  For example, (\d\d\d)-(\d\d\d-\d\d\d\d) would result in two regex groups.  These can be accessed with mo.group(1) and mo.group(2).  The whole thing can be accessed with mo.group(0).  To retrieve all groups at once, use mo.groups().
#### Match Multiple Groups with the Pipe
r'Batman|Tina Fey'
#### Optional Matching with Question Mark
r'(\d\d\d-)?\d\d\d-\d\d\d\d'
#### Match Zero or more with Star
r'Bat(wo)*man'
#### Match One or more with Plus
r'Bat(wo)+man'
#### Match Specific Repetitions with Curly Brackets
(Ha){3,5}
#### Greedy vs Non-Greedy Matching
By default, Python uses greedy matching.  In order to use a non-greedy matching algorithm, place a question mark at the end of the curly brackets.  For example, r'(Ha){3,5}' will only match the longest string of HaHaHaHa.  However, the regex r'(Ha){3,5}?' will match the first string 'HaHaHa' found.  
#### Regex FindAll Method
+ regex.findall()
+  Returns a list of strings that match as long as there are no groups in the regex.
+  If there are groups in the regex, findall() will return a list of tuples.


## Regex Character Classes
------
#### Any numeric digit 0-9
\d
#### Any character that is not a numeric digit
\D
#### Any letter, numeric digit, or underscore
\w
#### Any character that is not a letter, numeric digit, or underscore
\W
#### Any space, tab, or newline character
\s
#### Anything that is not a space, tab, or newline character
\S
#### Custom Character Classes
+ [aeiouAEIOU] (all vowels)
+ [^aeiouAEIOU] (no vowels)
+  

#### Wildcard Character
. (matches any character except for newline)
#### Match everything
.* (matches everything)
#### Match everything (nongreedy)
(.*?) (match smallest string possible)
#### Match the newlines with the dot character
```
newlineRegex = re.compile('.*',re.DOTALL)
newlineRegex.search('Do thing 1\nDo thing 2\n Do the Final thing\n').group()
```
#### Combine newline matching, case insensitive searches, and regex comments
val = re.compile('foo', re.IGNORECASE | re.DOTALL | re.VERBOSE)
#### Generate Correct File Path, Regardless of Platform (os)
os.path.join('usr','bin','spam')
#### Get Current Directory
os.getcwd()
#### Change Directory
os.chdir('C:\\Windows\\System32')
#### Create New Folders
os.makedirs('C:\\delicious\\walnut\\waffles')
#### Change Relative Path to Absolute Path
os.path.abspath('.')
#### Determine if a path is absolute or relative
os.path.isabs('.')
#### Change Absolute Path to Relative Path
os.path.relpath('C:\\Windows','C:\\')
#### Split Path based on file and dirname
```
path = 'C:\\Windows\System32\\calc.exe'
os.path.basename(path) #returns calc.exe
os.path.dirname(path) #returns C:\\Windows\\System32
```
#### Split Path based on file and dirname
dirname,basename = os.path.split(path)
#### Split Path into list based on separator
path.split(os.path.sep) #Returns ['C:','Windows','System32','calc.exe']
#### Get Size of File
os.path.getsize(path)
#### Get Info about File
os.stat(path)
#### List directory contents
os.listdir(os.path.dirname(path))
#### Checking path validity
os.path.exists('C:\\Windows')
#### Checking if file exists
os.path.isfile('C:\\nc.exe')
#### Checking if directory exists
os.path.isdir('C:\\temp')
#### Open a File
file = open('C:\\temp\\test.txt')
#### Read contents of file
content = file.read()
#### Get all lines of a file into a list
file_lines = content.readlines()
#### Write to a file
```
file = open('bacon.txt','w')
file.write('sizzzzzle...')
file.close()
```
#### Append to a file
```
file = open('bacon.txt','a')
file.write('Nothing to add...')
file.close()
```
#### Save Variables with shelve Module (import shelve)
```
import shelve
shelfFile = shelve.open('mydata')
cats = ['Al','Bert','Cindy']
shelfFile['cats'] = cats
shelfFile.close()
```
#### Retrieve information from shelf
```
shelfFile = shelve.open('mydata')
list(shelfFile.keys())
list(shelfFile.values())
shelfFile.close()
```

## Organizing Files
------
#### Add an Environment Variable
os.putenv("MYVAR","A"*1000)
#### Copying files and folders (shutil module)
shutil.copy('C:\\spam.txt','C:\\delicious')
#### Copy folder and all subelements
shutil.copytree('C:\\bacon','C:\\bacon_backup')
#### Move file
shutil.move('C:\\bacon.txt','C:\\eggs') #Results in move from C:\\ to C:\\eggs\\bacon.txt if the directory 'eggs' exists
#### Remove File
os.unlink(path)
#### Remove Directory
os.rmdir(path)
#### Remove Directory and Contents
shutil.rmtree(path)
#### Safe Deletes with send2trash module (import send2trash)
send2trash.send2trash('bacon.txt') #Sends to recycle bin
#### Walk through directory
```
for folderName,subfolders,filenames in os.walk('C:\\'):
continue
```
#### Reading a ZIP file
```
import zipfile
exampleZip = zipfile.Zipfile('example.zip')
exampleZip.namelist()
fileInfo = exampleZip.getinfo('zippedfile.txt')
fileInfo.file_size
fileInfo.compress_size
exampleZip.close()
```
#### Extract ZIP
exampleZip.extractall()
#### Extract single file from ZIP
exampleZip.extract('zippedfile.txt')
#### Extract single file form ZIP to specific directory
exampleZip.extract('zippedfile.txt','C:\\')
#### Create a ZIP file
```
import zipfile
newZip = zipfile.ZipFile('new.zip','w')
newZip.write('spam.txt', compress_type=zipfile.ZIP_DEFLATED)
newZip.close()
```

## Debugging
------
#### Raising exceptions with the "raise" keyword.
+ raise Exception
+  exceptions are raised with the "raise" statement.  Often found in try/except statements.

#### Get the traceback as a string
```
import traceback
try:
	raise Exception('This is an error')
except:
	errorFile = open('errorInfo.txt','w')
	errorFile.write(traceback.format_exc())
errorFile.close()
```
#### Assertions
sanity check to make sure your code isn't doing something obviously wrong.  Performed by assert statements.
#### Assert statements
+ Check that something is true that should be true.
+  assert 'red' in stoplight.values(), 'Neither light is red!' + str(stoplight)

#### Disable assertions
Assertions may be disabled with passing the "-0" argument to python.

## Logging
------
#### Logging Module example
```
import logging
logging.basicConfig(level=logging.DEBUG, format=' %(asctime)s - %(levelname)s - %(message)s')
logging.debug('Start of Program')
```
#### Logging Level DEBUG
Lowest level, used for small details.
#### Logging Level INFO
Used to record information on general events in your program to confirm things are working
#### Logging Level WARNING
Used to indicate a potential problem that doesn't prevent the program from working.
#### Logging Level ERROR
Used to record an error that caused the program to fail to do something
#### Logging Level CRITICAL
The highest level.  Used to indicate a fatal error.
#### Disable Logging
logging.disable(logging.CRITICAL)
#### Logging to file
logging.basicConfig(filename='program.log',level=logging.DEBUG, format=' %(asctime)s - %(levelname)s - %(message)s')

## Web Scraping
------
#### Launch a webbrowser
import webbrowser; webbrowser.open('http://google.com')
#### Handle an unknown number of commandline arguments
#### Make a GET request to a website
```
import requests
response = requests.get('http://www.hooperlabs.xyz/robots.txt')
if response.status_code == requests.codes.ok:
print(f"Success! {response.status_code}")
```
#### Check for error
response.raise_for_status()
#### Saving Response to Hard Drive
```
for chunk in response.iter_content(100000):
file.write(chunk)
```
#### Parse HTML with BeautifulSoup
soup = bs4.BeautifulSoup(response.text, 'html.parser')
#### Find an Element in BeautifulSoup with select()
soup.select('div')
#### Find an Element in bs4 of a specific ID
soup.select('#unique-id')
#### Find a span within a div
soup.select('div > span')
#### Find all elements named input that have a type attribute equal to button
soup.select('input[type="button"]')
#### Get id from element
spanElement.get('id')
#### Get attributes dict from element
spanElement.attrs
#### Control the Browser with Selenium
```
from selenium import webdriver
browser = webdriver.Firefox()
browser.get('https://hooperlabs.xyz')
```
#### Find elements on page by class name
browser.find_element_by_class_name(name)
#### Find elements that match CSS selector
browser.find_elements_by_css_selector(selector)
#### Find elements by ID
browser.find_elements_by_id(id)
#### Find elements by tag name
browser.find_elements_by_tag_name(tagname)
#### Find elements by name
browser.find_elements_by_name(name)
#### Find elements by partial link
browser.find_elements_by_partial_link_text(text)
#### Get tag name of web element object
webElem.tag_name
#### Get value of attribute
webElem.get_attribute(name)
#### Get element text
webElem.text
#### Clears typed text in field
webElem.clear()
#### Determines if element is visible
webElem.is_displayed()
#### Determines if input element is enabled
webElem.is_enabled()
#### Determines if checkbox or radio button is selected
webElem.is_selected()
#### Get location of element (x,y)
webElem.location
#### Click an element
webElem.click()
#### Fill out a form field element
webElem.send_keys('email@mail.null')
#### Submit form
webElem.submit()
#### Sending Special Keys
+ from selenium.webdriver.common.keys import Keys
+  Keys.DOWN, Keys.UP
+  Keys.ENTER, Keys.RETURN
+  Keys.HOME, Keys.END, Keys.PAGE_DOWN
+  Keys.ESCAPE, Keys.BACK_SPACE, Keys.DELETE
+  Keys.F1
+  Keys.TAB

#### Refresh Page
browser.refresh()
#### Browser Back Button
browser.back()
#### Quit Browser
browser.quit()

## Working with Excel SpreadSheets
------
#### For xls, use openpyxl
import openpyxl
#### Read an Excel Document
wb = openpyxl.load_workbook('widgets.xlsx')
#### Get sheet names
wb.get_sheet_names()
#### Get a sheet by name
sheet = wb.get_sheet_by_name('Sheet 1')
#### Get title of sheet
sheet.title
#### Get active sheet
wb.get_active_sheet()
#### Get value of cell A1
sheet['A1'].value
#### Get row and column of cell
sheet['A1'].row | sheet['A1'].column
#### Choose Cell by Row/Column
cell = sheet.cell(row=1, column=2)
#### Get highest row/column of sheet
sheet.get_highest_row() | sheet.get_highest_column()
#### Convert between letters and numbers
```
import openpyxl
from openpyxl.cell import get_column_letter, column_index_from_string
get_column_letter(1)
column_index_from_string('AA')
```
#### Get Cells within a certain range
tuple(sheet['A1':'C3'])
#### Get all items in row of sheet
sheet.columns[1]
#### Write Excel Document
```
import openpyxl
wb = openpyxl.Workbook()
sheet = wb.get_active_sheet()
sheet.title = 'My first sheet'
wb.save('example.xlsx')
```
#### Create a sheet
wb.create_sheet(index=2, title='Middle Sheet')
#### Different Font
```
from openpyxl.styles import Font, Style
fontObj1 = Font(name='Times New Roman', bold=True)
styleObj1 = Style(font=fontObj1)
sheet['A1'].style/styleObj
sheet['A1'] = 'Bold TNR'
```
#### Formulas
sheet['B9'] = '=SUM(B1:B8)'
#### Write File with Data Only (no formulas)
wbDataOnly = openpyxl.load_workbook('test.xlsx', data_only=True)
#### Adjust height/width of rows/cols
sheet.row_dimensions[1].height=70
#### Merge Cells
sheet.merge_cells('A1:D3')
#### Unmerge Cells
sheet.unmerge_cells('A1:D3')
#### Freeze Panes
sheet.freeze_panes = 'A2' #Freezes Row1

## Working with PDFs
------
#### Open a PDF
+ import PyPDF2
+  pdfFileObj = open('test.pdf','rb')
+  pdfReader = PyPDF2.PdfFileReader(pdfFileObj)

#### Number of pages
pdfReader.numPages
#### Get a page object
pageObj = pdfReader.getPage(0)
#### Extract Text from Page
pageObj.extractText()
#### Determine if a PDF is encrypted
pdfReader.isEncrypted
#### Decrypt a PDF with a password
pdfReader.decrypt('rosebud')
#### Write a PDF
pdfWriter = PyPDF2.PdfFileWriter
#### Write a page to a PDF
pdfWriter.addPage(pageObj)
#### Save PDF File
pdfWriter.write(pdfOutputFile)
#### Rotate a page clockwise
page.rotateClockwise(90)
#### Watermark a page
firstPageObj.mergePage(pdfWatermarkReader.getPage(0))
#### Encrypt a PDF
pdfWriter.encrypt('swordfish')

## Word Documents
------
#### Docx Library
import docx
#### Open a Word File
doc = docx.Document('test.docx')
#### Find length of Word File
len(doc.paragraphs)
#### Choose different styles for paragraphs
doc.paragraphs[0].style = 'Normal'
#### Get Paragraph Text
doc.paragraphs[1].text
#### Writing Word Documents
```
doc = docx.Document
doc.add_paragraph('Hello World!')
doc.save('helloworld.docx')
```
#### Add Heading
doc.add_heading('Header 0',0)
#### Add a page break
doc.paragraphs[0].runs[0].add_break(docx.text.WD_BREAK.PAGE)
#### Add Picture
doc.add_picture('zophie.png',width=docx.shard.Inches(1),height=docx.shared.Cm(4))

## CSV Documents
------
#### CSV Reader (import csv)
reader = csv.reader(open('test.csv','r'))
#### List Data
data = list(reader)
#### Get one item
reader[0][0]
#### Write a CSV
```
outputFile = open('output.csv','w', newline='')
writer= csv.writer(outputFile)
writer.writerow([1,2,3,4])
```
#### Write CSV with different delimiter/lineterminator
csvWriter = csv.writer(csfFile, delimiter='\t', lineterminator='\n\n')

## JSON
------
#### Read JSON into variable (as dict)
string_from_json = json.loads('{"foo":"bar","food":"baz"}')
#### Read JSON dict to string
json.dumps('{"foo":"bar"}')

## Keeping Time and Scheduling Tasks
------
#### Get Current Time in epoch time(import time)
time.time()
#### Get Time Difference
time.time() - time.time()
#### Sleep for 5 Seconds
time.sleep(5)
#### Round a Number
round(time.time(),2)
#### Datetime modules
import datetime
#### Separating datetime objects
```
import datetime
datetime.datetime.now()
dt = datetime.datetime(2015,2,27,11,10,49,55,53)
dt.year, dt.month, dt.day
```
#### Get Datetime Obj from Timestamp
datetime.datetime.fromtimestamp(10000000)
#### Using the Timedelta Data Type
delta = datetime.timedelta(days=11,hours=10,minutes=9,seconds=8)
#### Get total seconds
delta.total_seconds()
#### Add 10 days to now
datetime.datetime.now() + datetime.timedelta(days=10)
#### Convert Datetime Objects into Strings
date_var.strftime('%Y/%m/%d %H:%M:%S')
#### Convert String into Datetime
datetime.datetime.strptime('October 21, 2015', '%B %d, %Y')

## strftime directives
------
#### Year with century (2014)
%Y
#### Year without century (14)
%y
#### Month as Decimal Number
%m
#### Full month name
%B
#### Abbreviated month name
%b
#### Day of the month
%d
#### Day of the year
%j
#### Day of the week
%w
#### Full Weekday Name
%A
#### Abbreviated weekday name
%a
#### Hour (24hr clock)
%H
#### Hour (12hr clock)
%I
#### Minute
%M
#### Second
%S
#### AM or PM
%p
#### Literal % character
%%

## Threading
------
#### Start a Thread
```
import threading
threadObj = threading.Thread(target=print, args=['cat','dog','monkey'],kwargs={'sep': ' & '})
threadObj.start()
```

## Launching Other Programs
------
#### Subprocess Module (start a subprocess of the Python program)
import subprocess
#### Start a program with no arguments
proc = subprocess.Popen('C:\\Windows\\System32\\calc.exe')
#### Start a program with arguments
proc = subprocess.Popen(['C:\\Windows\\notepad.exe','C:\\hello.txt'])
#### Poll for a program to be complete
proc.poll()
#### Wait for a program to exit
proc.wait()
#### Open file with default application (Note- shell=True is only needed on Windows)
subprocess.Popen(['start','hello.txt'],shell=True)
#### Open file with default application OSX
subprocess.Popen(['open','hello.txt'])

## Sending and Reading Email
------
#### Send an Email with smtplib
import smtplib
#### Connect to SMTP Server using TLS
smtpObj = smtplib.SMTP('smtp.example.com',587)
#### Connect to a SMTP Server that doesn't support TLS
smtpObj = smtplib.SMTP_SSL('smtp.gmail.com',465)
#### Send client EHLO
smtpObj.ehlo()
#### Start TLS connection (only port 587)
smtpObj.starttls()
#### Login to SMTP Server
smtpObj.login('bob@example.com','PASSWORD')
#### Send an email
smtpObj.sendmail('bob@example.com','alice@example.com','Subject: So long.\nDear Alice, so long and thanks for all the fish.  Sincerely, Bob')
#### Close SMTP Connection
smtpObj.quit()
#### Gmail Application-Specific Passwords
Gmail has an additional security feature for Google accounts called "application-specific passwords", where you the exposure of this password doesn't compromise your entire google account.
#### View received email with IMAP
import imapclient
#### Connect to IMAP Server
imapObj = imapclient.IMAPClient('imap.gmail.com',ssl=True)
#### Login to IMAP Server
imapObj.login('h00p@hooperlabs.xyz','chumbawumbafan69')
#### Select IMAP Folder
imapObj.select_folder('INBOX', readonly=True)
#### List IMAP Folders
pprint.pprint(imapObj.list_folders())
#### Get all UIDs of messages after date
UIDs = imapObj.search(['SINCE 05-Jul-2014'])
#### Other IMAP Search Words
+ ALL
+  BEFORE date
+  ON date
+  SUBJECT foobar
+  BODY foobar
+  TEXT foobar
+  FROM email
+  TO email
+  CC email
+  BCC email
+  SEEN
+  UNSEEN
+  ANSWERED
+  UNANSWERED
+  DELETED
+  UNDELETED
+  DRAFT
+  UNDRAFT
+  FLAGGED
+  UNFLAGGED
+  LARGER N
+  SMALLER N
+  NOT foobar
+  OR foobar1 foobar1

#### Fetch a message with a UID
rawMessages = imapObj.fetch([40041], ['BODY[]','FLAGS'])
#### Read a message with pyzmail
import pyzmail
#### Convert message to a readable format
message = pyzmail.PyzMessage.factory(rawMessages[40041]['BODY[]'])
#### Get Message Subject
message.get_subject()
#### Get Message FROM address
message.get_address('from')
#### Get CC'd addresses
message.get_addresses('cc')
#### Get Message Text
message.text_part.get_payload().decode(message.text_part.charset)
#### Get Message HTML
message.html_part.get_payload().decode(message.html_part.charset)
#### Decode Non-Ascii Bytes
b"\x90".decode("latin-1")
#### Log out of IMAP server
imapObj.logout()
#### Read Messages with a 10MB limit instead of 10kb limit
imaplib._MAXLINE = 10000000
#### Search Gmail
UIDs = imapObj.gmail_search('meaning of life')
#### Delete a Message
imapObj.delete_messages(UIDs)
#### Expunge Deleted Messages
imapObj.expunge()

## Sending Text Messages
------
#### Send a SMS Text
```
from twilio.rest import TwilioRestClient
accountSID = 'foobar'
authToken = 'xx'
twilioCli = TwilioRestClient(accountSID, authToken)
twilioNumber = '+15555555555'
myCellNumber = '+14444444444'
message = twilioCli.messages.create(body='Mr. Watson - Come here - I want to see you.', from_=twilioNumber, to=myCellNumber
updatedMessage = twilioCli.messages.get(message.sid)
```

## Ctypes (Local Library Functions)
------
#### Ctypes allows you to load and call functions in dlls
import ctypes
#### Load a Windows Library
stdcall = ctypes.windll.LoadLibrary("/path/to/lib.dll")
#### Load a C Library
cdecl_dll = ctypes.cdll.LoadLibrary("C:\\Windows\\System32\\crtdll.dll"); cdecl_dll.printf(b'Hello, %s', b"HooperLabs")

## PEFile (Access and Modify EXEs and DLLs)
------
#### PEFile lets you read and write the various pieces of PE Files
import pefile
#### Save PE as Python Object
exe = pefile.PE("C:\\Windows\\System32\\crtdll.dll")
#### View Headers
hex(exe.OPTIONAL_HEADER.ImageBase)
#### View Entry Point
exe.OPTIONAL_HEADER.AddressOfEntryPoint
#### Print all Functions in EXE
import pefile; [print(f"Name: {fn.name} Address: {fn.address}") for fn in pefile.PE("/path/to/DLL.dll").DIRECTORY_ENTRY_EXPORT.symbols]

## Get OS Information
------
#### Determine Platform Name
sys.platform
#### Determine System Version Name
sys.getwindowsversion()

## Tricky Math
------
#### Format a decimal to a bitmap string (1s and 0s)
format(my_bitmap_int, "016b")

## Numpy Tricks
------
#### Create an array
arr = numpy.array([[0]*x] * y, numpy.int32)
#### Access an array value
arr[2,3]
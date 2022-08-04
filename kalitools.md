# Kali Linux Tools
======
#### Web Shells
ls /usr/share/webshells/ 
#### searchsploit (View Exploit)
searchsploit -x 34451
#### searchsploit (Download Exploit)
searchsploit -m 31337 
#### seachsploit (Search without Color)
searchsploit --colour -t php 5.X | grep -vi \.php | head
#### DNS Zone Transfer
dig axfr <domain> @<dns-server>
#### DNS Zone Transfer
nmap --script=dns-zone-transfer -p 53 ns2.domain.com
#### DNS Zone Transfer
host -l domain namesvr 
#### RDesktop (mount shared folder)
rdesktop -u offsec -p password <ip-address> -r disk:home=/root
#### RDesktop (xfreerdp w/ clipboard)
xfreerdp /clipboard /v:mycomputer.mydomain.local /port:3389 /u:myuser /d:mydomain.local /p:mypass /size:1600*1000
#### Desktop (mount shared folder)
rdesktop -u offsec -p password <ip-address> -r disk:home=/root
#### Debian (Kali) Network Manager
nmtui
#### Run JS from Command Line
node -e "console.log('hello')"
#### Run JS File from Command Line
node script.js
#### Mount a WEBDAV Share (requires davfs2)
mount -t davfs -o noexec http://example.com/webdav/ /mnt/webdav
#### Store username + password for WEBDAV Share
echo -e "/mtn/webdav myUser P@ssw0rd" | tee -a /etc/davfs2/secrets
#### Mount a VMDK File (libguestfs-tools)
guestmount -a /path/to/test.vmdk -i --ro /mnt/diskmnt


## CeWL
#### Create Custom Wordlist from website
cewl https://target.com/ -w outfile.txt -d 4 -m 7


## Curl
------
#### PUT a file with NTLM Auth
curl --ntlm -u domain\\myUser:P@ssw0rd\? -T shell.php http://example.com:8080/shell.php

## Empire
------
#### Configure Listeners
uselistener http
#### DefaultDelay/DefaultJitter
How often does a beacon phone home?
#### Launcher
What the base command looks like
#### Headers
Server-side headers presented by the server
#### Proxy/ProxyCreds
Web proxy-related settings
#### Configure Stager
usestager multi/launcher
#### Uses Invoke-Obfuscation
assorted string manipulation to obfuscate signature-based analysis of payloads.
#### Interact with Agent
interact AGENTID
#### Execute Shell Command
shell ipconfig

## OpenSSL
------
#### Decrypt a file with key and IV (no padding/no salt)
openssl enc -d -nosalt -nopad -aes-256-cbc -K "A4D350E68EED39C72CEA5585464789E160B5C5782FDD28A7D2D227F40D7B76E4" -iv '1BD487C6AC68570040CCB900EA9FED05' -in wonkatania.enc -out wonkatania.txt -k "Pure Imagination"
#### Connect to a HTTPS client (like nc)
openssl s_client -connect hooperlabs.xyz:443 -cipher EXP-RC4-MD5
#### Encode Base64 or other things
openssl enc -d base64 -in file.b64 -out file.txt
#### Decrypt AES or other things
openssl enc aes -k deadlist -in file.txt -out file.enc
#### Hash/Digest/Signature
openssl dgst -sha1 file.txt
#### Encrypt an image
openssl enc -aes-128-ecb -e -in logo.rgba -out logo-ecb.rgba -pass pass:deadlist
#### Use a salt, key, and IV derived from a password (-k)
openssl enc -aes-128-cbc -k pass -p -in file1 -out file1.enc
#### Create a New Certificate
+ openssl req -newkey rsa:2048 -nodes -keyout priv.key -x509 -days 362 -out priv.crt
+  cat priv.key priv.crt > priv.pem

#### Read a x509 Certificate
openssl x509 -in cert.crt -text
#### Export a Certificate from PFX
openssl pkcs12 -in file.pfx -clcerts -nokeys -out cert.crt
#### Export a Private Key from PFX
openssl pkcs12 -in file.pfx -nocerts -out key.pem

## UFW
------
#### List Rules
ufw status numbered
#### Delete Rule
ufw delete 1
#### Add Rule
uwf add allow 80:80/tcp

## Perl
------
#### Install Perl Module
perl -MCPAN -e 'install NetPacket::IP'
#### Open and create a file
open($FILE, ">name_of_file"); 
#### Close the file.
close($FILE); 
#### Print characters to file
print($FILE $file-content.$more_file_content); #
#### Declare a variable
my $variable = "poop"; 
#### Loads in little endian byte format
payload += struct.pack("<I", 0x019F6940) #

## Image Manipulation
------
#### Remove compression from an image
convert -depth 32 logo.png logo.rgba
#### Repackage RGBA into PNG
convert -size $(identify logo.png | cut -f 3 -d ' ' ) -depth 32 logo-ecb.rgba logo-ecb.png
#### Change exif data for image
exiftool -Comment='mycomment' index.jpeg

## Text Manipulation
------
#### Add bytes to end of a 1111-byte file
dd if=/dev/zero of=file2 bs=1 count=100 seek=1111

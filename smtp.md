# SMTP Enumeration
======
#### SMTP Nmap Scan
nmap -p 25 --script=smtp-commands,smtp-enum-users,smtp-ntlm-info,smtp-open-relay,smtp-strangeport,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764,smtp-brute <ip-address>
#### VRFY user
echo -n -e "VRFY root\r\n" | nc -nv 10.1.1.1 25
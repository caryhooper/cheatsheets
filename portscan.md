# Reconnaissance & Port Scanning
======

## nmap
------
#### Full Port Scan (1-65535)
"-p-"
#### Service Version Scan
"-sV"
#### Light Scan
"--top-ports 50 --open"
#### Ping Sweep
"-sn"
#### Source Port 53
"--source_port 53"
#### Send more probes and change ICMP
nmap -sP -PE -PP -PS21,22,23,25,80,113,21339 -PA80,113,443,10042 --source_port 53 -n -T4 -iL ips.list

## nc
------
#### TCP Netcat Scanning
nc -unvv -w 1 -z <ip> 440-450
#### UDP Netcat Scanning
nc -nv -u -z -w1 <ip> 160-161

## TCP
------
#### Shitty Portscanner (Egypt)
for port in {1..1023}; do : 2>/dev/null > "/dev/tcp/192.168.0.1/$port" && echo "$port"; done

## Output
------
#### Greppable Output (good for multiple hosts)
"-oG scan.grep"
#### XML  Output (viewable in iexplore.exe)
"-oX scan.xml"
#### UnicornScan (Faster for UDP scans)
unicornscan -m {UT} <ip-address>:1-65535
#### ARP
arp-scan -l
#### ARP
netdiscover -i tap0

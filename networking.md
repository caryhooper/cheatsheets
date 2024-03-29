# Networking Notes (TCP/IP)
======

## Iptables
------
#### IPV6 iptables rules
cat /etc/iptables/rules.v6
#### IPv4 iptables rules
cat /etc/iptalbes/rules.v4

## Wireless Configuration
------
#### Configure wlan0 interface
ifconfig wlan0 <ip-address>
#### Start DNS/DHCP server
service dnsmasq restart
#### Enable routing
sysctl net.ipv4.ip_forward=1
#### Enable NAT
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
#### Run access point daemon
hostapd /etc/hostapd/hostapd.conf
#### WireShark Decrypt SSL Traffic
Create SSLKEYLOGFILE environment variable pointing to log file.  (May have to run Chrome.exe --ssl-key-log-file=C:\Temp\ssl-keys.log

## Packets and Packet Captures (usually run elevated)
------
#### Capture OSPF traffic
tcpdump -i eth0 -n "ip[9]==89"
#### Remove TCP headers and dump TCP payloads into separate files
tcpick -wR -r capture.pcap
#### Remove TCP headers and dump TCP payloads into separate files for Client or Server only
tcpick -wR{C,S} -r capture.pcap

## Scapy
------
#### Import Scapy
from scapy.all import scapy
#### Send ICMP with Payload
send(IP(dst="10.1.99.2")/ICMP()/"HelloWorld")
#### Read a PCAP File
rdpcap('/path/to/pcap.cap')
#### Show a Summary
myPackets.show()
#### Show TCP Layer of Packet
myPackets[1][TCP]
#### Change src IP of packet
packet.src = "127.0.0.1"
#### Craft an IP packet
p = IP(dst="10.10.10.10")
#### Add a OSI Layer to a Packet
p = p / TCP(dport=443)
#### Gather all "Raw" data of every packet
pkt[Raw].load for pkt in TCP_PACKETS if Raw in pkt
#### Add Raw Data Paylaod
packet /= Raw("\xaa\xaa\x03\x00")
#### Do things for all packets in a pcap
sniff(offline="test.pcap",prn=handler_function,filter="tcp or udp")
#### Find Destination of Ether Layer
packet.dst
#### Find Destination of IP Layer
packet.paylaod.dst
#### Find Destination Port of TCP Layer
packet.payload.payload.dport
#### Send packet to a List of Ports
p = IP(dst="10.10.10.10") / TCP(dport=[22,80,443,1024])
#### Separate packets into Answered vs Unanswered Packets
ans,unans = sr(packet)
#### Show Summary of Packets Info
packet.summary()
#### Show Details of Packets Info
packet.show()
#### Show only IP Details of Packet
packet[IP].show() OR packet["IP"].show()
#### Hex Dump of Packet
hexdump(packet[TCP])

## SSH
------
#### SSH Hop through host
ssh -J user1@host1 user2@host2
#### Upload File with SSH
ssh user1@host1 tee rfile < lfile
#### Download File with SSH
ssh user1@host1 cat rfile > lfile

## Socat Redirector
------
#### Detatch process from shell
screen
#### Redirect with socat
sudo socat TCP4-LISTEN:80,fork TCP4:secure.losenolove.com:80
#### Detatch Screen
screen -d

## VLAN Hopping
------
#### Info
Takes advantage of a switch misconfiguration with the DTP (Dynamic Trunking Protocol) mode.  If the mode is set to dynamic desirable, the attacker can negotiate its own trunk 
#### Tool
yersinia --> DTP --> launch attack --> "enable trunking"
#### Add a VLAN interface
+ modprobe 8021q
+  vconfig add eth0 200
+  ifconfig eth0.200 up
+  ifconfig eth0.200 10.0.0.6 up


# BPF notes
======
#### Reference
https://biot.com/capstats/bpf.html
#### Reference
https://www.ibm.com/support/knowledgecenter/en/SS42VS_7.3.2/com.ibm.qradar.doc/c_forensics_bpf.html
#### Protocol List
arp,ether,fddi,icmp,ip,ip6,link,ppp,radio,rarp,slip,tcp,tr,udp,wlan
#### Negation
!=
#### Concatenation
{&&|and}
#### Alteration
{|| | or}
#### Explanation
BPFs may also be referred to with their primitives.  Multiple examples are given here.

## Examples
------
#### ICMP
proto 1
#### ICMP
ip[9] = 0x1
#### ICMP Echo
icmp[0] = 0x08
#### ICMP Not Echo
icmp[icmptype] != icmp-echo
#### Host
ip host <ip-addr>
#### Traffic between hosts
host 10.0.0.1 and host 10.0.0.2
#### Complex Hosts
host host1 and \( host2 or host3 \)
#### Destination Net
dst net <ip-subnet-CIDR>
#### Src Host
src host <ip-addr>
#### TCP Dst Port
tcp[2:2] < 0x14
#### Multiple TCP Ports
tcp dst port 80 or 8080
#### TCP Port
tcp port 80
#### UDP
ip[9] = 0x11
#### UDP + Port
udp dst port not 53
#### Portrange
src portrange 80-88
#### Mac Filter
ether {src|dst} <mac-addr>
#### VLAN
vlan 100
#### Fragmented IPv4
ip[6:2] & 0x3fff != 0x0000
#### IPV6
ip[0] & 0xf0 != 4
#### IPV6
ip6
#### TCP Flags (S)
ip[13] & 0x02 = 2
#### TCP Flags (S)
tcp-syn
#### TCP Flags (F)
tcp-fin
#### TCP Flags (SF)
ip[13] & 0x3f = 0x03
#### TCP Flags (A)
tcp[13] & 16 != 0
#### TCP Flags (U)
tcp[13] & 32 != 0
#### TCP Flags (P)
tcp[13] & 8 != 0
#### TCP Flags (R)
tcp[13] & 4 != 0
#### TCP Flags (S)
tcp[13] & 2 != 0
#### TCP Flags (F)
tcp[13] & 1 != 0
#### TCP Flags (PA)
tcp[13] = 24
#### TCP Flags
{ip|ip6} tcp tcp-{ack|fin|syn|rst|push|urg|
#### Packet Size > 134bytes
ip[2:2] > 0x86
#### Multiple Filters
tcp[13] 0x02 = 2 and ip[2:2] > <hex-size> and ip[0] & 0xF0 != 4
#### Not TOS (Types of Service)
ip[1] != 0
#### Specific Interface
ifname <interface>
#### Specific Interface
on <interface>
#### ATM Packet (Virtual Channel Identifier)
vpi <n> (where n is a path identifier)
#### LLC-encapsulated
llc
#### ATM BPF Ref:
https://yaleman.org/2013/09/11/berkeley-packet-filter-bpf-syntax/

## TCPDump Filters
------
#### Show only packets with Push and Ack (HTTP Req/Resp Data)
sudo tcpdump -A -n 'tcp[13] = 24' -r input.pcap

## Wireshark Filters
------
#### Capture on a specific network
net 10.1.1.1/24
#### Capture a spcific port
tcp.port==21
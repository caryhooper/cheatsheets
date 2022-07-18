# Linux Enumeration
======

## System
------
#### OS Information
cat /etc/*-release
#### OS Version
cat /etc/issue
#### Kernel Version and Arch
uname -a 
#### System Hostname
hostname

## Users
------
#### Another Way to List passwd
getent passwd  
#### Current Username/Privs
id
#### Logged On Users
w
#### User Info
who -a
#### Last logged in user
last -a
#### Add User
useradd -m user
#### Change current user password
passwd 
#### Remove User
rmuser username
#### Find Valid Users
grep -vE "nologin|false" /etc/passwd
#### Sudoers
cat /etc/sudoers
#### Add User to Sudoers
sudo adduser <username> sudo 
#### Sudo as other user
sudo -u otheruser bash

## Network
------
#### Network Connection
ss 
#### TCP/UDP Connection
netstat -punta
#### List of Open Files/Connections
lsof -i 
#### List interfaces
ip link
#### Arp Table
arp 
#### Routing Table
route 
#### Domain Lookup
dig -x <ip-address>  
#### Domain Lookup
host <ip-address>
#### Domain SRV Lookup
host -t SRV _service _tcp.url.com
#### Find DHCP Assignments
/var/log/messages | grep DHCP 
#### SSH through a HTTP Proxy Tunnel
ssh cobb@127.0.0.1 -o "ProxyCommand=nc.openbsd -X connect -x 10.10.10.67:3128 %h %p"
#### List all Connections
ss -anp
#### List iptables Firewall Rules
grep -Hs iptables /etc/*

## Processes, services, drivers
------
#### List Processes
ps -efww | ps -aef | ps aux
#### Kill Process
kill <pid>
#### Installed Packages (Debian)
dpkg -l 
#### Installed Packages (Redhat/CENTOS)
rpm -qa 
#### List Services
cat /etc/services 
#### List All Kernel Modules
lsmod
#### Get Kernel Module Info
modinfo <drivername>

## Files
------
#### Find pdf files
find -i -name file -type '.pdf
#### Determine File Type
file <file>
#### Search Recursively for File Content
grep -R 'thing'
#### Search for File Name
find . -iname '*config*'
#### Find Root SUID Binaries
find / -xdev -user root \( -perm -4000 \)  2>/dev/null
#### Find Writable Directories
find / -writable -type d 2>/dev/null
#### Check User Home Directories 
ls -lahR /home/
#### List Cron Jobs
ls  /etc/cron* | xargs cat {}
#### List Cron Jobs for Current User
crontab -l
#### List Cron Jobs that Ran
grep CRON /var/log/cron.log
#### Access Windows SMB Share
smb:// ip /share
#### SMB Connect
smbclient -L \\RALPH -I 10.11.1.3 
#### Passwd File
cat /etc/passwd 
#### Shadow File (password hashes)
cat /etc/shadow 
#### Trash Bin
/home/your_username/.local/share/Trash
#### Updates the Local Database
updatedb

## Misc
------
#### Update $PATH Variable
PATH=$PATH:/home/mypath
#### Download WebPage
wget http:// url -0 url.txt -o /dev/null
#### Remote Desktop
rdesktop 10.10.10.12
#### SCP Put File
scp /tmp/file user@x.x.x.x:/tmp/file 
#### SCP Get File
scp user@ remoteip :/tmp/file /tmp/file
#### Command History
history <user>
#### Compile C Program
gcc -o outfile myfile.c 
#### Interactive PTY Shell
python -c 'import pty; pty.spawn("/bin/sh")' 
#### Cron Log
cat /var/log/cron
#### Redirect STERR to STOUT
command 2>&1
#### Unzip an Archive
unzip scripts.zip 
#### Unpack a Tarball
tar xvzf tarball.tar.gz
#### Pack a Tar Archive
tar cvf tarball.tar files/*

## Privesc Scripts
------
#### LinPEAS
<a href="https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS">https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS</a>

## Filesystem
------
#### Find inode number of files in current directory (inodes are 4 bytes)
ls -i .
#### Find inode number of current directory
ls -id .
#### Read an inode
icat /dev/sdb1 <inode-number> | xxd | head
#### Input a file, block size, skip blocks, count for # blocks
dd if=/dev/mapper/VulnOSv2--vg-root bs=4096 skip=4718592 count=32767 > /images/bg144.raw
#### Find Ascii strings with decimal offset
strings -a -t d
#### Mount an NFS Share (requires nfsutils)
mount -t nfs 192.168.0.1:/home/karl nfs
#### List all mounted filesystems
mount
#### List Drives Mounted at Boot
cat /etc/fstab
#### View all Available Disks
lsblk

## Anti-Forensics
------
#### Change Timestamps (use current time)
touch -t
#### Stop Logggin to .bash_history
unset HISTFILE
#### Zero Messages Log
echo > /var/log/messages
#### strace sniffing
+ sh -c while [ 1 ]
+  do 
+ export pid=$(ps aux | grep sshd| grep net | grep -v grep | awk {'print $2'})&& 
+  if [ "$pid" != "" ]
+ then 
+  strace -p $pid -e write 2>>/var/log/mail/.$pid.log
+  fi
+  done


## System Administration
------
#### Start a Service at Boot (newer)
systemctl enable apache2
#### Start a Service at Boot (older)
update-rc.d enable apache2

## Crontab Examples (https://crontab.guru/examples.html)
------
#### Every Minute
* * * * * command
#### Every 3 Minutes
*/3 * * * * command
#### Every Hour at 30min
30 * * * * command
#### Every Day at 1AM
0 1 * * * command
#### Every Wednesday (first three letters of day)
0 0 * * WED command
#### Every Saturday and Sunday
0 0 * * 6,0
#### Every Week
0 0 * * 0 command
#### Every Month
0 0 1 * * command
#### Every 6 Months
0 0 1 */6 * command
#### Every Year
0 0 1 1 * command

## Mysql
------
#### Failed to start DB troubleshooting
+ mysqld --help --verbose | grep 'log-error' | tail -1
+  mysqld --help --verbose | grep 'datadir' | tail -1

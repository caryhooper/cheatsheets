# NFS Enumeration
======
#### Run nmap NSE scripts for NFS
nmap -p 111 --script nfs* 10.1.1.1
#### Show Mounted NFS shares
showmount -e 10.1.1.1
#### Mount an NFS share (disable file locking on older shares)
sudo mount -o nolock 10.1.1.1:/myshare /mnt/mymountedshare
#### Add a User with a Specific UUID
sudo adduser newuser; sudo sed -i -e 's/1001/1014/g' /etc/passwd
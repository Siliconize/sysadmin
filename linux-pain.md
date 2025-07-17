# Linux Command that migh save your ass

```
rsync -aHAXv /source /destination
```
Flags explained:
```
-a  archive
-H  follow Hardlinks
-A  ACLs
-X  extended Attributes
-v  verbose
```
Basically this is the way to backup a linux system.

List Block Devices (talks to the kernel):
```
lsblk -f
```

Also list block devices, but this command talks directly to the device instead of the kernel.
```
blkid

blkid >> /etc/fstab
```
This gives you the UUIDs you need to create the fstab file.

Get info on youre `/dev/` devices:
```
udevadm info /dev/sda
```
Yes the output is daunting, but also very helpful.

What is a certain program? This gives a small description of the program.
```
whatis
```

Where is a progam location? 
```
whereis
```

Which one of the saved programs is the current shell using, like often times you have the same program installed across different /bin/ directories, this shows which one you are using:
```
which
```

Tells you what file a file is. Like if it's a txt or a binary for example. 
```
file
```



Perfect to see what is slowing down your boot.

```
systemd-analyze blame
```

# Linux PAIN 

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

## Partition Stuff

`fdisk -l` - get info on all disks and partitions on system 

`parted /dev/sdX print` - show partition table

`parted /dev/sdX resizepart N END` - resize the partition number N to new end sector END

`sfdisk -d /dev/sdX > table.bak` - backup the partition table
`sfdisk /dev/sdX < table.bak`	restore partition table


you can also just run an x server and use gparted or if you are remote you could forward x over ssh, but I think learning the commands would be better for that situation. 

After resizing you also need to resize the filesystem to fit the partition
use `resize2fs /dev/sda1` for ext or `btrfs filesystem resize max /` if you are on btrfs. Oh and for btrfs you specify the mount point of the drive at the end, not the inode. 

`partprobe /dev/sdX` - tell the OS to re-read the partition table

`sync` - flush all pending writes from cache to the disk, good for flashdrives and such.

`udevadm settle` - wait for udev events to finish, tells you if devices are ready.

`sgdisk -g /dev/sdX` convert the partition table from mbr to gpt 

### Labels!

`e2label /dev/sdXN "LABEL"`	        -   set ext2/3/4 label

`ntfslabel /dev/sdXN "LABEL"`       -   set NTFS label

`fatlabel /dev/sdXN "LABEL"`        -   set FAT label

`xfs_admin -L "LABEL" /dev/sdXN`    -   set XFS label

I like to use them for the `/etc/fstab`. Why? Because vfat filesystems are weird and gave me issues with "forgetting" their UUIDs. 

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


## Boot Process 

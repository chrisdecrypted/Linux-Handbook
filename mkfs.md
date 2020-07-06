# `mkfs` Command in Linux

The letters in `mkfs` stand for "make file system". This command is commonly used for managing storage devices in Linux.  I will discuss generally what a file system is, and provide examples for using this command effectively.

#### Caution: Improper use of this command may lead to permanent data loss. 

This is a powerful tool. It is important to understand the potential consequences of altering the filesystem. Selecting the wrong device node will erase all data on that device. Use this command at your own risk.


## Usage 
```
mkfs -t [fs type] [target device]

OR 

mkfs.[fs type] [target device]
```

This command requires a privileged account,so you will need to run as root or use sudo.

## What is a file system?
A file system (fs) refers to the structure and logic that manage data on a device. The file system controls how data is stored and retrieved. There are many types of file systems and each has its own advantages and disadvantages. Let's look at some common types.

### Common types of file systems
* FAT* 
* NTFS 
* ext* 
* APFS
* HFS*

You have probably come across one or more of these fs types before. You may even associate the types with their respective operating systems. 

Generally speaking FAT/NTFS are designed for Windows, Ext is used with Linux systems, and APFS/HFS are MacOS/OS X file systems. Each of these address the logic of file structure in a different way which can result in issues.

## Compatibility 
This is why it is crucial to think about this before declaring a fs type, or "formatting" your device. Each use case is different, and it is up to you to decide what fs works best for your needs.

Keep in mind that choosing the wrong fs can cause a lot of frustration. 

An error could mean your files are inaccessible once the fs is created. Always have a backup before removing critical data from any device.

Also keep in mind that older fs can be limited with regards to storage capacity, ie: older versions of FAT are limited to use on storage devices less than 4 GB.

# Create a File System on a USB Device
Now that we have some background information, we can start using mkfs. The most practical demonstration I can think of is formatting a USB flash storage drive. These same principles will apply to any type of storage you choose. 

## 1) Find Your Device
First you will need to find your device. One method you can use is `sudo fdisk -l`. This will list all disk nodes that are currently mounted. 

```
christopher@linux-handbook:~$ sudo fdisk -l
Disk /dev/sda: 25 GiB, 26843545600 bytes, 52428800 sectors
Disk model: VBOX HARDDISK   
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x3c62c49c

Device     Boot    Start      End  Sectors  Size Id Type
/dev/sda1  *        4096  1023998  1019903  498M 83 Linux
/dev/sda2        1024000 44036094 43012095 20.5G 83 Linux
/dev/sda3       44036096 52424702  8388607    4G 82 Linux swap / Solaris

Disk /dev/sdb: 28.93 GiB, 31040995328 bytes, 60626944 sectors
Disk model: Patriot Memory  
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 91A34D6F-E67B-E54D-B19C-5CC828DAAB9A

Device     Start      End  Sectors  Size Type
/dev/sdb1   2048 60626910 60624863 28.9G Linux filesystem
```

Your output will obviously vary. Please be very careful when identifying your desired drive. If you are unsure, remove the disk and run the `fdisk -l` command again. If you have the correct device, it won't be listed while disconnected.

## 2) Verify the Partition
The device I'm using is a Patriot Memory USB and it is located at `/dev/sdb`. In addition to identifying the correct disk, you will need to make sure that you are changing the fs of the desired partition.

I used fdisk tools to delete existing data and write a new partition table. While I was doing that, I created a new partition to write to. That partition will be our target: `/dev/sdb1`. 


### 3) Unmount 
Before we attempt to change the file system, we will need to unmount it using the `umount` command.
```
christopher@linux-handbook:~$ sudo umount /dev/sdb1
```

### 4) Create the File System
Now that we have verified our target and unmounted the drive, we can proceed to creating the file system. 

I have added the `-v` verbose option here to display more information when running.

```
christopher@linux-handbook:~$ sudo mkfs.ext4 /dev/sdb1 -v
mke2fs 1.45.5 (07-Jan-2020)
fs_types for mke2fs.conf resolution: 'ext4'
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
1896832 inodes, 7578107 blocks
378905 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=2155872256
232 block groups
32768 blocks per group, 32768 fragments per group
8176 inodes per group
Filesystem UUID: 73882769-7599-4c79-a00b-ef317ccd921d
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
	4096000

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done 
```
This process can take some time, but should finish in under 20 minutes unless the target is larger than 2TB. 

I had several issues with the program hanging on the last item. Unfortunately, there is no progress indicator I had no errors thrown. 

### 5) Verify
It is important to make sure that the device is recognized on the systems you will use it with. I created a folder called test and a file within it called test.txt.

To save time, you can copy and paste my commands here. 

```
mkdir test && cd test
touch test.txt
echo "THIS IS ONLY A TEST" > test.txt
cat test.txt
```
If everything worked, you should be able to mount the drive to your desired systems and access the files. If you cannot access the files on your system, there is probably a compatibility issue.

# Conclusion
Did you enjoy our guide to the `mkfs` command? I hope all of these tips taught you something new. If you like this guide, please share it on social media. If you have any comments or questions, leave them below. If you have any suggestions for topics you'd like to see covered, feel free to leave those as well. Thanks for reading. 

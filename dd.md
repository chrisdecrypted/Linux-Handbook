# Using the `dd` Command
The `dd` command is a utility for copying and converting files and has many practical uses. 

It has been suggested that the name is derivative of an older IBM Job Control Language function where dd stood for "Data Definition". In Linux, the abbreviation stands for "Data Duplicator" or "Disk Dump" or a variety of other alliterations depending on your source.

It may have even earned the poignant nickname "data destroyer" which brings me to an important point. Please exercise caution when practicing with `dd`. 

This command is capable of doing some serious damage. Be sure to double check your syntax to avoid a costly mistake. You don't want to be the person that confuses partition names and watches in agony as their root partition is destroyed and replaced with a blank file. 
 

# Syntax
```
dd if=<filename> of=<filename> [options]
```

## Getting to Know 'dd'
There are a wide range of uses for this command, I'll introduce some common approaches. 

### Physical Media / Partition Clones/Back-Ups
In the above syntax, `if` and `of` are for input file and output file, respectively. This is the core functionality of dd. It duplicates data from one source to another. You don't need to use physical media with dd. 

### Text Manipulation
It is possible to use stdin (standard input) from your keyboard to collect input and point it to a file. It's also possible to quickly convert case and a variety of other useful text editing tools are included in the man page. 

I mentioned IBM earlier alluding to the long history of this program. One of the original functionalities of this command actually centered around converting EBCDIDC, an encoding schema created by IBM, to ASCII. 

### Filesystem Manipulation
You can also copy files with it, but `cp` is generally recommended over dd for this application. We have an article where you can read about the cp command [here](https://linuxhandbook.com/cp-command/).

### Some Behavioral Notes
When copying with `dd`, you should also be aware that by default it will copy the <em>complete</em> information from a specified source. 

Meaning that if you try to duplicate a partition or a disk, it will also copy free space. 

So, for instance, if you're cloning a hard drive with 4TB,you will need a destination drive with at least 4TB to prevent truncated files and errors. Remember also, if the disk has only 1TB worth of data, dd will still copy the other 3TB of space. That's a bad move that will waste a lot of time and resources. 

There are some constraints that we can add to dd and other measures we can take to change this behavior. There are actually an overwhelming amount of controls that can be used in conjunction with dd. I will try to address some of the ones that I think may benefit our readers most, but the goal of this article is to give a primer on dd, not document every possible function. 

Returning to the dangers of improper use with dd. I urge you to conceptualize your goal and carefully execute it to avoid corrupting or destroying important files. Obviously, we are not liable for the loss of your information. If you make a mistake. Don't say we didn't warn you.

Are you ready to move on? I hope I didn't scare you too bad. Learning Linux is a lot of fun. Part of the adventure is learning from mistakes we make. If you're using dd for the first time, don't do it on your production machine or try to manipulate critical data.


### Use a Virtual Machine
I recommend practicing on a dummy virtual machine to familiarize yourself before attempting to alter any "real world" assets. 

For this tutorial, I decided to try something outside the Debian family and spun up a copy of Fedora 31 in VirtualBox. Are any of you big supporters of Red Hat? If you are, let me know what you like about it in the comment section. 

With the warnings and some contextual information out of the way, we are ready to move on to some applications for this very simple, but powerful command.

## Example 1: Clone Disks
Cloning one disk to another can be very easy with dd. For my example, I have two disks named 'sda' and 'sdb'. 

I created 'sdb' in a virtual machine for this demonstration, it does not reflect an actual device. For this to be effective in a real world application, you would substitute 'sdb' with whatever the name associated with your target disk partition is.

Remember that 'sda' will attempt to copy itself onto 'sdb' using the entire contents of the drive, not just the data. 

You need to allocate enough space on your output file to accommodate for unused space on the sector. You can also choose to re-partition the drive to the exact size currently filled by data. I would recommend this method. It will decrease the amount of time it takes to perform the operation and create a more useful document.

When you're ready to clone a disk, you can run `fdisk` to identify your disks, their partitions, and their capacity. 

```
sudo fdisk -l 
```
Running this command will list available drives and partitions and their respective sizes. This can be helpful for correctly identifying your target device. 

Again, for our application we are using the names 'sda' and 'sdb' and we will assume they are the same size.


```
[linuxhandbook@fedora ~]$ sudo dd if=/dev/sda of=/dev/sdb
[[enter pw for sudo]]
dd: writing to 'dev/sdb': No space left on device
8108369+0 records in
8108369+0 records out
4151484416 bytes (4.2 GB, 3.9 GiB) copied, 12.3602 s 336 MB/s
```
The output lets us know that the write was successful, we can ignore the message saying there's no longer any space left on 'sdb'. 

The summary also lists the amount of data copied, how long it took, and how quickly it was copied. We will look at this a bit more when I cover block size.

## Example 2: Backing Up a Disk Partition
The steps for cloning a device and backing up a partition are similar. Instead of our target file being a device, we can create an '.img' (raw disk image) file.

Let's say that our system has a separate partition for our home directory... 

### Wait, you didn't know you could do that? 
Yes, you can! Learn more about how creating a dedicated home partition allows you to keep your data AND easily swap distros at our sister site <strong>It's FOSS</strong> by clicking [here](https://itsfoss.com/replace-linux-from-dual-boot/).

Okay, so let's say we've found our home partition at 'sda2' and we want to back it up to a file named 'home_backup.img' in our current directory.

```
dd if=/dev/sda2 of=home_backup.img
```
It's that easy! So now you have no excuse for not having a good backup routine. 

Sure, that was easy, but there's always more to learn. 

## Dealing with BS
Before we get into the next example, let's talk about BS, or block size. If you've seen this used to specify a value with dd commands, you might wonder why it's there. 

If your curiosity lead you to an internet search, then I'm willing to bet that you're probably <em>still</em> wondering why it's there.

## What is a Block Device?
I'll try my best to give a plain language explanation. Block devices are usually physical media with finite storage. 

You can look up information on a medium like a disc by seeking a specific block of data. So for instance, the system can read a CD-ROM and search for information starting at block 500 (an arbitrary number). It can also be used to "bookend" information and maybe use info from block 500 to block 1500. 

These blocks can be segmented in ways that make it efficient for the system to analyze. This may reflect the storage space of the medium, or standard system specs the medium is likely to be associated with. 

I'll continue with the example of a CD-ROM which has its own defined block size (2048). Each block must have a maximum of 2048 bytes. Even if a block only contains 100 bytes of data, it will still take up the same 2048 bytes. 

There are some cases where you may want to define the block size to make dd run faster or prevent data corruption. Going back to our CD-ROM example, creating blocks of a different size could cause anomalies when it's time for the data to be read.

If left undefined, dd will use a block size of 512. This is the smallest block size that a typical hard drive can read. 

If your medium is not confined to a certain block size, you're probably safe adjusting it for performance (write time). Let's look at a few examples.

### Performance Comparisons
#### Performance with unspecified block size
```
[linuxhandbook@fedora ~]$ sudo dd if=/dev/sda of=home_backup.img
[sudo] password for linuxhandbook: 
dd: writing to 'home_backup.img': No space left on device
31974953+0 records in
31974952+0 records out
16371175424 bytes (16 GB, 15 GiB) copied, 113.848 s, 144 MB/s

```

#### Performance with block size of 1024.
```
[linuxhandbook@fedora ~]$ sudo dd if=/dev/sda of=home_backup.img bs=1024
[sudo] password for linuxhandbook: 
dd: error writing 'home_backup.img': No space left on device
15987477+0 records in
15987476+0 records out
16371175424 bytes (16 GB, 15 GiB) copied, 75.4371 s, 217 MB/s
```

You can see that the process was performed at a faster speed. Another run with a bs of 4096 was faster yet with a rate of 327 MB/s. System caching can also play a role in speed, but that is a topic for another day.

You may have noticed the variation in the number of records in and out. This is because we are changing the size of each block and therefore the capacity of the individual blocks, despite the output file remaining the same size. For this reason, adjusting the bs value can have unintended consequences. For example, it could lead to discrepancies when a checksum performed. 

## Example 3: Delete Data and Zero the Disk

```
dd if=/dev/zero of=/dev/sda
```
Remember all the warnings from earlier? This command will replace every block of 'sda' with zeroes. 

How does this work? Essentially, the same as all the other in and out dd commands. What is '/dev/zero'?

It is a pseudo-device included on Unix/Linux operating systems that will write zeroes to a file until the it reaches the end of the file. 

You can similarly use 'dev/random' which outputs random bits of data.

This may be unnecessary if you plan to use an raw image file to replace contents since using dd will already copy unused space. 

## Example 4: Create .ISO from CD/DVD
We can copy directly from the cd-rom drive if your computer still has one. Earlier I mentioned that the standard byte size of a cd-rom is 2048. We'll set the byte size to match that to avoid conversion issues and then add a couple other commands. 

```
conv=noerror
``` 
As the name implies, any errors will be ignored. The program will continue through to the final block without stopping.
ill not stop for them. It
```
sync
```

When used in conjunction with 'noerror', 'sync' will ensure that any missing blocks of data will automatically be padded with null information. 

This means the existing data will be mapped to the same locations, presumably preserving as much of the content as possible. 

It's important to make sure that your source and destination files have the same 'bs' set for these operations, otherwise they will not have the intended results.

#### Here's our complete syntax:
```
dd if=/dev/cdrom of=space_jam_dvd.iso bs=2048 conv=noerror,sync
```

## Example 5: Create Bootable USB
We can use dd to create a bootable USB and it's just as easy as you might expect. There is one extra step. The bootable part.

### Use 'mkfs' to Build the File System
We use the 'mkfs' command to build the filesystem to our USB before running 'dd'. 

Without options, it uses the default ext2 system. So assuming the USB we want to prepare is called 'sdb' and we want to change the file system to ext4, we would run the following command:

```
sudo mkfs.ext4 /dev/sdb
```
If you want to use with a Windows system you could replace the first part of the command with mkfs.ntfs. 

You can also use the following syntax:
```
mkfs -t [for type] $filesystem.
```
Once the bootable medium is prepared, we can continue to our dd command. 

```
dd if=someFile.iso of=dev/sdb
```
Use the .iso mountable image and copy to corresponding drive name for your usb device. 

## Bonus Content
I'll list a few more options here as a resource. There are way more than this, but these are a few that I believe that you  may find useful.

#### Count
`count=n` 

With count, 'n' represents the number of blocks you wish to count in total.

#### Using Seek 
`seek=n` 

If you want to begin your copy at a specific block sector, you can use the seek function to tell the program where to start. 

Text Formatting Options
```
Convert to all lower case characters
`conv=lcase`

Convert to all lower case characters
`conv=ucase`

Convert from EBCDIC to ASCII
`conv=ascii` 

Convert from ASCII to EBCDIC
`conv=ebcdic` 
```

## Conclusion

Thanks for reading. I hope you enjoyed this primer on 'dd'. There are so many different ways that you can use this command. I tried to cover a lot of the more useful examples. If you've got something you'd like to see or a direct question, I'd love to help. Let me know what you think below in the comments.


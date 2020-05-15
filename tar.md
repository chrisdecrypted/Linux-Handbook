# Tar Command in Linux

What is tar? Tar stands for "tape archive" and refers to a practice from the earlier days of computing when data was backed up to tapes. Despite the nostalgiac origin of the name, tar is very powerful and uses modern technologies to archive and compress files.

The tar command is essential for linux users to understand. Before we get too deep into that subject, let's start things off with a little clarification. 

* Archiving - The act of storing multiple files as one or more files.
* Compression - The act of shrinking a larger file or files.

I'm a little embarassed to admit, I didn't know there was a difference for a long time. The two concepts are closely related. This isn't the only confusing thing about tar. More about that later. Let's discuss some other tools to give you some background.

## Common Archive and Compression Tools
Most of us come to Linux after years of using Windows or Mac. If that's the case, then when you think of compressed files, you probably think of '.zip' or '.rar' files. 

Actually, there are a lot of different types of compression. Tar and g-zip (tar.gz) dominate Linux systems and both are accessible via the tar command. 

It's important to remember that extensions are not necessary on Unix-based systems. A unix-based operating system can typically identify files by their headers regardless of extension, but using the common naming scheme can help avoid confusion. I recommend following convention, especially if you will be sharing the files with other users.

Let's take a look at common conventions to provide some clarity. 

# Naming Conventions for Common Archive Types
## .Tar 
This is a tarball file. It is only an archive and no compression is performed.

## .Tar.Gz or .tgz
This is the extension of an archive that has been compressed with G-Zip. 

## .Tar.Bz2 or .tbz
This is the extension of an archive that has been compressed with Bz2. This is a relatively new technology. It features a higher ratio of compression, but that increased shrinking power means it takes a bit longer to complete.  

## .Tar.xz or .txz, etc.
Tar also features built in support for xz, lzip, and more. These tools primarily use the same compression algorithim, LZMA. The popular 7z that has become fairly common in Windows environments also uses this algorithim. Further differences in the files result from structure and metadata. I won't go into these details in our examples, but I wanted to mention them.


# Documents to be Archived

For this article, I want to demonstrate some of the common methods for archiving and compressing files using tar.

I have assembled some files of different types in my Documents folder. There are stock images, some lengthy text files and a dummy file that takes up 1gb of space. We will look at how the file size is changed by the compression through several examples.

Here is a complete list of the documents that will be used. 
#### Note the total file size of 1054000.

```
christopher@linuxhandbook:~/Documents$ ll
total 1054000
drwxr-xr-x  2 christopher christopher       4096 Apr 29 11:10 ./
drwxr-xr-x 15 christopher christopher       4096 Apr 29 11:15 ../
-rw-r--r--  1 christopher christopher 1073741824 Apr 29 11:10 1gig-file.file
-rw-r--r--  1 christopher christopher    1048216 Apr 29 11:04 closeup-photo-of-black-and-blue-keyboard-1194713.jpg
-rw-r--r--  1 christopher christopher      11179 Apr 29 11:07 lorem1.txt
-rw-r--r--  1 christopher christopher      11179 Apr 29 11:08 lorem3.txt
-rw-r--r--  1 christopher christopher      11179 Apr 29 11:08 lorem4.txt
-rw-r--r--  1 christopher christopher      11179 Apr 29 11:07 lorem.txt
-rw-r--r--  1 christopher christopher    2977109 Apr 29 11:05 photo-of-woman-wearing-turtleneck-top-2777898.jpg
-rw-r--r--  1 christopher christopher    1462681 Apr 29 11:04 semi-opened-laptop-computer-turned-on-on-table-2047905.jpg
```

I've already touched on the capabilites of tar. It is a powerful tool with a lot of options. This may make the command appear more complicated than it really is. As always, my goal is to demystify the command line. So let's break things down into smaller pieces before combining several options in the examples. 

Here is a table of commonly used options. Keep in mind, this is just the beginning. I reccomend going throught the help documentation yourself to find even more possibilities once you feel comfortable.

Switch | Expansive Options | Description |
|--|--|--|
-c, |--create              | create a new archive
-d,| --diff, --compare     | find differences between archive and file system
-r,| --append               | append files to the end of an archive
-t,| --list                 | list the contents of an archive
-u,| --update               | only append files newer than copy in archive
-x,| --extract, --get      | extract files from an archive                       
-j,| --bzip2                | filter the archive through bzip2
-z,| --gzip, --gunzip, --ungzip   | filter the archive through gzip

# Examples
## 1) Create a Tarball
Earlier I mentioned the common file types associated with the tar command. This is perhaps the most basic. 

```
tar cvf doc.tar ~/Documents
```


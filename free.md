<!-- First article written. Originally in Word format, converted to markdown to clean up.  -->
# Using Free Command in Linux 
## Usage
The command is called using the syntax:
```
free [options]
```

## Default Output
If a user would like to know detailed information about their memory availability, the free command is a simple utility that makes it easy to find real time results for a variety of use cases.

The free command without options returns results for ‘total’, ‘used’, and ‘free’ memory on your system by accessing information from the linux kernel. It also displays categories for ‘shared’, ‘buff/cache’, and ‘available’. To avoid some potential confusion, let’s clarify what those terms mean. 

## Key Definitions:
`Total` is straightforward. This figure represents all existing memory. 

`Used` is a calculation of the total system ram minus allocated free, shared, buffer, and cache memory. 

`Free` is memory that is not being used for any purpose. 

`Shared, Buffer, and Cache` fields identify memory being used for kernel/operating system needs. The buffer and cache are added together and the sum is listed under ‘buff/cache’.

`Available` memory appears in newer versions of free and is intended to give the end user an estimation of how many memory resources are still open for use. 

These clarifications are important. Incorrectly attributing meaning to the terms free or used memory can create a misconception of your system’s memory use.

This may lead an inexperienced user to falsely believe their system needs to be upgraded with more ram. Note that in previous versions there was no display for available memory. Users may incorrectly assume that because there is high memory usage, their hardware is underpowered. The available tab was presumably put in place to help offset this common misunderstanding.

The Linux operating system uses caching to improve performance. In very basic terms, this means that a certain amount of memory is set aside for use before it’s needed so it can be processed more quickly. This is a standard process and nothing to be concerned about unless the values seem very unusual for your current use. 

The ‘available’ memory estimate is probably adequate for someone who simply wants to know how their system is responding to certain applications. If you are unable to see this field, you may need to update to the latest version of ‘free’. You can check your current version by running ‘free -V’.
Customizing Output
My computer has version 3.3.15 of ‘free’ installed and the default output looks like this: 
```
[chris@machine ~]$ free
total        used        free      shared  buff/cache    available
Mem:        8048372     2593004     1366712   658380      4088656      4494976
Swap:             0           0           0
```
The default output displays information in kibibytes, but there are options to display in different formats if you prefer. Running the help (free -help) displays all the possible options you can append.
```
Options:    
 -b, --bytes             show output in bytes
     --kilo          show output in kilobytes
     --mega          show output in megabytes
     --giga          show output in gigabytes
     --tera          show output in terabytes
     --peta        show output in petabytes
     -k, --kibi          show output in kibibytes
 -m, --mebi          show output in mebibytes
 -g, --gibi          show output in gibibytes
     --tebi          show output in tebibytes
     --pebi              show output in pebibytes
 -h, --human         show human-readable output
     --si            use powers of 1000 not 1024
 -l, --lohi          show detailed low and high memory statistics
 -t, --total         show total for RAM + swap
              -s N, --seconds N     repeat printing every N seconds
 -c N, --count N     repeat printing N times, then exit
     -w, --wide          wide output
```

Special Case Notes for Certain Users
I’m using Manjaro Linux which is based on Arch. When I tried to get free to output in mebibytes, I got this result: 

```
[chris@machine ~]$ free -m
free: Multiple unit options doesn't make sense.
```

I was a little puzzled, so I spun up a virtual machine image of Ubuntu LTS 16.04. This time, when I entered the command, the output displayed as expected. After a quick internet search, I switched back to my Manjaro terminal and I ran:

```
[chris@machine ~]$ unalias free 
```

The `unalias` command removes specified aliases from the shell configuration file. After doing this, I was able to get the expected results and a variety of outputs. Please be aware this is a ‘semi-permanent’ solution. There are other options for the unalias command to restrict this modification to a specific instance.

## Interpreting output
```
[chris@machine ~]$ free -k
              total        used        free      shared  buff/cache   available
Mem:            8048372     2637544     1535384      490460     3875444     4618428
Swap:             0           0           0
[chris@machine ~]$ free -m
              total        used        free      shared  buff/cache   available
Mem:           7859        2573        1500         479        3785        4511
Swap:             0           0           0
[chris@machine ~]$ free -g
              total        used        free      shared  buff/cache   available
Mem:              7           2           1           0           3           4
Swap:             0           0           0
[chris@machine ~]$ free -h
              total        used        free      shared  buff/cache   available
Mem:          7.7Gi       2.5Gi       1.5Gi       479Mi       3.7Gi       4.4Gi
Swap:            0B          0B          0B
```

Here are several examples of different options. They show the same requested information with some basic math conversions. I think that the human readable option (free -h) is one of the most effective for an everyday user. 

```
[chris@machine ~]$ free -h --si
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.7G        1.4G        485M        3.8G        4.4G
Swap:            0B          0B          0B
```

If we add ‘--si’, we get the output converted from powers of 1024 to powers of 1000. Depending on your region, this may be the more familiar figure. Although, it’s not uncommon for these terms to be used interchangeably despite the real differences in value. 

Another great feature is the capability to automate the command. There are two options that help us customize this tool. There is ‘-s’, which runs the free command for the designated interval of seconds until the user quits the program (^+C). 

There is also ‘-c’ which can be used separately or in conjunction with the seconds option. If you enter only ‘-c’ and an integer (n), it will run the command n number of times. By default it uses one second intervals.

Let’s say you want to open a series of applications and see how your memory is affected. For my test output I will use the human readable format using powers of 1000 (Gb) instead of 1024 (GiB). I’m going to record for 30 seconds to analyze the impact. I will capture the data every 3 seconds and I will do this for 10 counts. Here is this example formatted for the command line and its output:

```
[chris@machine ~]$ free -h --si -s 3 -c 10
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.8G        1.2G        501M        3.8G        4.2G
Swap:            0B          0B          0B
 
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.9G        1.2G        501M        3.8G        4.2G
Swap:            0B          0B          0B
 
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.9G        1.2G        501M        3.8G        4.2G
Swap:            0B          0B          0B
 
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.8G        1.2G        501M        3.8G        4.2G
Swap:            0B          0B          0B
 
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.8G        1.2G        501M        3.8G        4.2G
Swap:            0B          0B          0B
 
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.8G        1.2G        501M        3.8G        4.2G
Swap:            0B          0B          0B
 
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.8G        1.2G        501M        3.8G        4.2G
Swap:            0B          0B          0B
 
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.9G        1.1G        520M        3.8G        4.2G
Swap:            0B          0B          0B
 
              total        used        free      shared  buff/cache   available
Mem:           7.9G        2.9G        1.1G        549M        3.9G        4.1G
Swap:            0B          0B          0B
 
              total        used        free      shared  buff/cache   available
Mem:           7.9G        3.0G        998M        553M        3.9G        4.0G
Swap:            0B          0B          0B
```

I waited about 20 seconds before doing anything. Then, I opened a few browser tabs and accessed some bookmarks. The stress of those activities is noted by the fluctuations in the output. Please note, the effect would be more pronounced using an output format with less rounding. For our purely demonstrative purposes, this is unnecessary. 

## Conclusions
This tutorial demonstrated how to get started using the ‘free’ command. Hopefully, you find this guide helpful and easy to understand. 

‘Free’ can be used to analyze system memory usage and can be tweaked using its various options to finely tailor output for your needs. 

If you have any questions or suggestions, please let us know in the comment section or send an email to the LinuxHandbook.com team at _________

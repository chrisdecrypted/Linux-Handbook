# Uniq Command
Uniq is a command line utility designed for filtering duplicate text. It can be used by itself but it is commonly used in along with other commands like [sort](https://linuxhandbook.com/sort-command/) to identify redundant information in a file.

## Syntax 
```
uniq [options] <input-file> <output-file>
```

## Quick Look at Defaults
When you run uniq without options it will use the stdin and stdout for input and output.

While using stdin is possible using the clipboard (copy/paste), this isn't the most practical use. 

Instead you would probably want to use this command on a file that you suspect contains duplicate information.

One limitation of the 'uniq' command is that it will only identify duplicates that are adjacent, or next to each other, in the file. This is pretty straightforward, but let me show you at an example so you can see it in action.

```
cat apple.txt
apple
orange
apple 
orange
```
```
[linuxhandbook@fedora ~]$ uniq apple.txt 
apple
orange
apple 
orange
```
As you can see, the duplicate text was not identified. So, we know right away that we cannot trust the program to identify every duplicate. There are some ways to get around this.

I'll show you a way to do this later, but let me run through some examples to familiarize you with 'uniq' before mixing in other commands and potentially confusing things. 

## Download the Demo Log File Here
I created a file to help you follow along without risking corruption of any system files or dealing with extraordinarily lengthy outputs. You can download a copy [here](link). 

I used a real system log but edited it for demonstration purposes. Most of the file has already been sorted into adjacent order, but I've left a couple lines "out of place" to show functionality.


## Example 1: Default Syntax 
Although I showed you this already, let's look at our sample file using the default syntax. 

```
[linuxhandbook@fedora ~]$ uniq sample_log_file.txt 
/usr/lib/gdm3/gdm-x-session[1443]: (II) No input driver specified, ignoring this device.
/usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: device is a keyboard
/usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: device removed
/usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: is tagged by udev as: Keyboard
/usr/lib/gdm3/gdm-x-session[1443]: (II) No input driver specified, ignoring this device.
/usr/lib/gdm3/gdm-x-session[1443]: (II) systemd-logind: got fd for /dev/input/event10 13:74 fd 55 paused 0
/usr/lib/gdm3/gdm-x-session[1443]: (II) This device may have been added with another device file.
PackageKit: get-updates transaction /354_eebeebaa from uid 1000 finished with success after 1514ms
wpa_supplicant[898]: RRM: Ignoring radio measurement request: Not RRM network
```
We can see that a lot of the duplicate lines are consolidated, but we still have redundant information. This is due to the functional limitation I already described. Let's look at a few more examples and examine some of the options that are built-in to 'uniq'.

## Example 2: Output Filtered Results to Destination File
You may want to save this output so you can easily edit it or preserve it. We can direct our output to a separate file instead of the normal stdout (terminal). It is important to note that you cannot use this format to override the original file. Your information will be erased. 

```
[linuxhandbook@fedora ~]$ uniq sample_log_file.txt sample_log_file1.txt 
[linuxhandbook@fedora ~]$ cat sample_log_file1.txt 
/usr/lib/gdm3/gdm-x-session[1443]: (II) No input driver specified, ignoring this device.
/usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: device is a keyboard
/usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: device removed
/usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: is tagged by udev as: Keyboard
/usr/lib/gdm3/gdm-x-session[1443]: (II) No input driver specified, ignoring this device.
/usr/lib/gdm3/gdm-x-session[1443]: (II) systemd-logind: got fd for /dev/input/event10 13:74 fd 55 paused 0
/usr/lib/gdm3/gdm-x-session[1443]: (II) This device may have been added with another device file.
PackageKit: get-updates transaction /354_eebeebaa from uid 1000 finished with success after 1514ms
wpa_supplicant[898]: RRM: Ignoring radio measurement request: Not RRM network
```

## Example 3: Using '-c' to Get Count of Repeated Lines
This option is pretty self-explanatory. The program will append the count to the beginning of each line. 

```
[linuxhandbook@fedora ~]$ uniq sample_log_file.txt -c
      2 /usr/lib/gdm3/gdm-x-session[1443]: (II) No input driver specified, ignoring this device.
      2 /usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: device is a keyboard
      1 /usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: device removed
      2 /usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: is tagged by udev as: Keyboard
      5 /usr/lib/gdm3/gdm-x-session[1443]: (II) No input driver specified, ignoring this device.
      1 /usr/lib/gdm3/gdm-x-session[1443]: (II) systemd-logind: got fd for /dev/input/event10 13:74 fd 55 paused 0
      7 /usr/lib/gdm3/gdm-x-session[1443]: (II) This device may have been added with another device file.
      1 PackageKit: get-updates transaction /354_eebeebaa from uid 1000 finished with success after 1514ms
      8 wpa_supplicant[898]: RRM: Ignoring radio measurement request: Not RRM network
```
## Example 4: Only Print Repeated Lines with '-d'
As you can see only lines that are duplicated throughout the file are shown. 

```
[linuxhandbook@fedora ~]$ uniq sample_log_file.txt -d
/usr/lib/gdm3/gdm-x-session[1443]: (II) No input driver specified, ignoring this device.
/usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: device is a keyboard
/usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: is tagged by udev as: Keyboard
/usr/lib/gdm3/gdm-x-session[1443]: (II) No input driver specified, ignoring this device.
/usr/lib/gdm3/gdm-x-session[1443]: (II) This device may have been added with another device file.
wpa_supplicant[898]: RRM: Ignoring radio measurement request: Not RRM network
```

## Example 5: Only Print Unique Lines with '-u'
Here, we get the inverse output of the previous command. None of these commands are repeated in the file.

```
[linuxhandbook@fedora ~]$ uniq sample_log_file.txt -u
/usr/lib/gdm3/gdm-x-session[1443]: (II) event9  - Intel HID events: device removed
/usr/lib/gdm3/gdm-x-session[1443]: (II) systemd-logind: got fd for /dev/input/event10 13:74 fd 55 paused 0
PackageKit: get-updates transaction /354_eebeebaa from uid 1000 finished with success after 1514ms
```

## Example 6: Ignore Fields or Characters with Uniq ['-f' and '-s']
This is really two examples, but the functions are nearly identical. I will explain how they work and then provide some clarity on the differences between the two of them.

Each of them use the following syntax
```
Skip fields with:
uniq <source_file> -f N
Skip characters with:
uniq <source_file> -s N
```
In each of these examples, 'N' is the count of items that you wish to skip. When you skip this number of items,uniq will begin the comparison at that point rather than compare the entire line.

The option 'f' will skip the assigned number of fields. The fields will be interpreted using the blank space.

```
[linuxhandbook@fedora ~]$ cat field_separated_values.txt 
blue	fish
blue	fish
blue	fish
one	class 
red	fish 
red	fish
two	class
two	class
[linuxhandbook@fedora ~]$ uniq -f 2 field_separated_values.txt 
blue	fish
one	class 
red	fish

```
The first 2 fields are ignored when the comparison is made and the output reflects this.

Similarly we can skip a specific number of characters.
```
[linuxhandbook@fedora ~]$ uniq -s 10 field_separated_values.txt 
blue	fish
```

## Example 7: Use '-w' to Compare Only N Characters

The '-w' option allows us to specify an exact number of characters to use in our comparison.

If you used the log file for the previous couple examples, that is fine. I wanted to make the comparison text a little simpler to limit confusion. If not, let's pull it back up and see what happens when we use only the first for characters to find duplicates.

```
[linuxhandbook@fedora ~]$ uniq -w 4 sample_log_file.txt 
/usr/lib/gdm3/gdm-x-session[1443]: (II) No input driver specified, ignoring this device.
PackageKit: get-updates transaction /354_eebeebaa from uid 1000 finished with success after 1514ms
wpa_supplicant[898]: RRM: Ignoring radio measurement request: Not RRM network
```

All of the lines that begin '/usr' are now identified as the "same" from the perspective of the program. 

This might prove helpful if you are looking for a particular log event. 

## Bonus: Avoid Incomplete Matches Using 'sort' and 'uniq' at the same time. 

You can run these commands separately to achieve the same effect, but if you have never used a pipe (the | character) in Linux this is a great way to learn about them. 

We can use pipes to combine different commands to save us keystrokes and improve our workflow. The commands will be performed in the order that they are typed. 

```
[linuxhandbook@fedora ~]$ cat apple.txt 
apple
orange
orange
apple
apple
banana
apple
banana
[linuxhandbook@fedora ~]$ uniq apple.txt | sort
apple
apple
apple
banana
banana
orange
[linuxhandbook@fedora ~]$ sort apple.txt | uniq 
apple
banana
orange
```

I added some some text to my "apple.txt" file to help demonstrate the output. We can see in the above examples how the different pipe order alters the results. 

Performing the 'uniq' command first will identify only the adjacent duplicates, and then they will each be sorted into alphabetical order using the 'sort' command.

In the second block, we have rearranged the text so that all items are in adjacent order first. Then we run the 'uniq' program and see there are only 3 unique lines in the file.

```
[linuxhandbook@fedora ~]$ uniq apple.txt -c | sort
      1 apple
      1 apple
      1 banana
      1 banana
      2 apple
      2 orange
[linuxhandbook@fedora ~]$ sort apple.txt | uniq -c
      4 apple
      2 banana
      2 orange
```
To further emphasize this point, I added the count command. Pipes allow us to run multiple commands at the same, but it is important to consider their order. 

Note that the contents of the file remains unchanged just as it would when running the commands individually. Piping the two commands together also keeps the results in the system's "memory". If you ran them separately, you could not get these results unless you made a new file and used it to overwrite the content of the original before running your second command.

## Conclusion

As you might imagine, that makes this an important concept in learning bash. These particular commands (sort and uniq) are often used together for quickly filtering information from large files like our pseudo-log. 
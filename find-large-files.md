# Find Large Files 

This is a quick tutorial for finding large files on your linux machine. We will combine a few commands that you may already be familiar with `du`, `sort`, and `head`. 

| Command | Description | 
|--|--|
| du | Displays disk usage of files in current or specified directory |
| sort | Sorts data according to user settings|
| head | Displays top lines of a text input source |

This just one combination for displaying file size information via the command line. On Linux, there are always plenty of options for your specific needs. That said, this is probably the most common approach. 

## Combining the Elements
Each command brings something to the table here. Our breakdown above shows generally what each command is capabale of. We are going to look at a few examples of how to target your searches and common pitfalls to avoid. 

# Examples 

## Defaults
What happens if you run the three commands together without options? Your output probably won't be very useful. 

When we run these commands, unless specified with `du`, everything will run automatically using the current working directory as the source file.

Sort without options arranges items in numerical order, but this behavior is a little strange. 100 is considered less than 12 because 2 > 0. That's definitely not what we want.

Head here defaults to displaying the first 10 items. Depending on the directory you want to analyze, you can tailor this to find large files quickly.

```
christopher@linuxhandbook:~$ du | sort | head
100	./.local/share/evolution/addressbook
108	./.mozilla/firefox/jwqwiz97.default-release/datareporting
112	./.local/share/gvfs-metadata
12	./.cache/fontconfig
12	./.cache/gnome-software/screenshots/112x63
12	./.cache/thumbnails/fail
12	./.config/dconf
12	./.config/evolution
12	./.config/gnome-control-center/backgrounds
12	./.config/ibus
```

## Adding Options
So let's look at what might be more typical options. We are going to add some options to sort that will help give us more logical output. 

Adding `-n` means that items will be sorted by numeric value. Adding `-r` means that the results will be reversed. This is what we want when searching for the largest number.

I'm also going to add `-5` to limit our results further than the default for head. This value is something that you should decide based on what you know about the system. 

You may want to expand the value to a number greater than 10, or omit it entirely if there are many large files you are trying to filter. Otherwise, you may run it, delete several files, but still have space issues. 

Okay, let's put it all together and see what happens. 

```
christopher@linuxhandbook:~$ du | sort -nr | head -5
1865396	.
1769532	./Documents
76552	./.cache
64852	./.cache/mozilla
64848	./.cache/mozilla/firefox
```
That's better, we can quickly see where the largest files are. We can do better though, let's clean it up with some more options.

## Human-Readable Ouput
The human options for certain commands help present numbers in a way that is familar to us. Let's try adding that to the `du` command.

```
christopher@linuxhandbook:~$ du -h | sort -nr | head -5
980K	./.local/share/app-info
976K	./.local/share/app-info/xmls
824K	./.cache/thumbnails
808K	./.cache/thumbnails/large
804K	./.local/share/tracker
```

Wait a second...

## Corrected Human-Readble Output
Those numbers don't make any sense. No, they don't because we've only changed the content to human-readable for the `du` command. `Sort` has it's own built-in function for human-readable numeric sort with `-h`. Both must be used to get the desired output. You can run into these kinds of issues often in Linux. 

It's important to experiment and make sure that your results "make sense" before using a command a specific way.


Let's try it again.

```
christopher@linuxhandbook:~$ du -h | sort -hr | head -5
1.8G	.
1.7G	./Documents
75M	./.cache
64M	./.cache/mozilla/firefox/jwqwiz97.default-release
64M	./.cache/mozilla/firefox
```

That's more like it. 

## What's taking up so much space?

We can tell from the output that the Documents folder contains some larger files, but if we switch to that folder and run our command again, we don't get the largest file. We get this: 

```
christopher@linuxhandbook:~/Documents$ du -h | sort -hr | head -5
1.7G	.
```
This is just telling us what we already know. The current directory, referred to as  `.`, has 1.7G worth of files. That isn't helpful if we're trying to find single, unusually large files.

We need to add another flag to `du` for this task. Using `-a`, we can get the output that we're looking for. Let's try it.

```
christopher@linuxhandbook:~/Documents$ du -ah | sort -hr | head -5
1.7G	.
1.1G	./1gig-file.file
699M	./doc.tar
2.9M	./photo-of-woman-wearing-turtleneck-top-2777898.jpg
1.4M	./semi-opened-laptop-computer-turned-on-on-table-2047905.jpg
```
# Conclusion
Did you enjoy our guide to `finding large files in linux`? I hope all of these tips taught you something new. If you like this guide, please share it on social media. If you have any comments or questions, leave them below. If you have any suggestions for topics you'd like to see covered, feel free to leave those as well. Thanks for reading. 
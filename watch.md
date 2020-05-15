# Watch Command in Linux
Watch is a great utility that automatically refreshes data. Some of the more common uses for this command involve monitoring system processes or logs, but it can be used in combination with pipes for more versatility. 

## Syntax

```
watch [options] [command]
```
# Examples

## Standard Output
Using Watch without any options will use the default parameter of 2.0 second refresh intervals.

As I mentioned before, one of the more common uses is monitoring system processes. Let's use it with the [free](https://linuxhandbook.com/free-commmand) command. This will give us up to date information about our system's memory usage. 

```
watch free
```

Yes, it is that simple friends.

```
Every 2.0s: free                                pop-os: Wed Dec 25 13:47:59 2019

              total        used        free      shared  buff/cache   available
Mem:       32596848     3846372    25571572      676612     3178904    27702636
Swap:             0           0           0
```
## Adjust Refresh Rate
We can easily change how quickly the output is updated using the `-n` flag. 

```
watch -n 10 free
```
```
Every 10.0s: free                               pop-os: Wed Dec 25 13:58:32 2019

              total        used        free      shared  buff/cache   available
Mem:       32596848     4522508    24864196      715600     3210144    26988920
Swap:             0           0           0
```
This changes from the default 2.0 second refresh to 10.0 seconds as you can see in the top left corner of our output.

## Remove Title/Header Info

```
watch -t free
```
The `-t` flag removes the title/header information to clean up output. The information will still refresh every 2 seconds. 

```
              total        used        free      shared  buff/cache   available
Mem:       32596848     3683324    25089268     1251908     3824256    27286132
Swap:             0           0           0
```

## Highlight Changes with '-d'

We can add the `-d` option and watch will automatically highlight changes for us. Let's take a look at this using the date command. I've included a screen capture to show how the highlighting behaves.

![image](watch-highlight.gif)

## Using Pipes with Watch
You can combine items using pipes. This is not a feature exclusive to watch, but it enhances the functionality of this software. Pipes rely on the `|` symbol. Not coincidentally, this is called a pipe symbol or sometimes a vertical bar symbol.

```
watch "cat /var/log/syslog | tail -n 3"
```
While this command runs, it will list the last 3 lines of the syslog file. The list will be refreshed every 2 seconds and any changes will be displayed.

```
Every 2.0s: cat /var/log/syslog | tail -n 3                                                      pop-os: Wed Dec 25 15:18:06 2019

Dec 25 15:17:24 pop-os dbus-daemon[1705]: [session uid=1000 pid=1705] Successfully activated service 'org.freedesktop.Tracker1.Min
er.Extract'
Dec 25 15:17:24 pop-os systemd[1591]: Started Tracker metadata extractor.
Dec 25 15:17:45 pop-os systemd[1591]: tracker-extract.service: Succeeded.
```

## Conclusion
Watch is a simple, but very useful utility. I hope we've given you ideas that will help you improve your workflow. 

This is a straightforward command, but there are a wide range of potential uses. If you have any interesting uses that you would like to share, let us know about them in the comments. 




# Screen Command
The Screen command in linux allows the user to create multiple virtual terminals that can be saved by name and reopened using keyboard shortcuts. Should you consider using screen to improve your work flow? Let's look at some of the reasons you might want to try it out. 

If you spend a lot of time in the terminal, you may find yourself using several terminals at once to perform different tasks. If you are accessing a machine remotely via SSH, for instance, this could be slowing you down. 

This is one of the most obvious use cases for screen. If you need to install a large package or some other intensive task, you would normally be stuck waiting for it to complete. Even worse, if you get disconnected or need to quickly exit, your troubles could quickly multiply. 

If this is starting to sound familiar, then you need `screen`! With this installed, you can simply "detach" the shell for that intensive task and it continues on, uninterrupted in the background. There are a lot of other cool built-in features. 

So let's take a look at some of the ways you can get started using screen to make your life easier. 

## Syntax
```
screen [options] [PID] 
```
Because this is a more interactive software, the specific syntax is less important than usual. Screen follows normal Linux conventions when entering commands. 

## Check for Installation
First, you'll want to see if this software is already included with your Linux distribution. Many modern flavors include it, but it's usually easy to install otherwise. You can check to see if it's installed by running the following:

```
screen --version
```

I am using Pop OS which is a Debian derivative distribution that uses the apt package manger. Screen is not installed by default, so I will type:

```
sudo apt install screen
```
If you are using a different package manager, obviously this command may be different. 

If you still cannot find it, you can also download the source [from GNU.org](https://www.gnu.org/software/screen/).

## Quick Overview
Screen is fairly easy to use, but it can still be a little confusing for new users. Starting screen on my machine removes the color theme from my terminal. However, if you're on a simple black and white shell, it may not be obvious that you have started the application.

As I mentioned previously, screen uses keybindings. These are shortcuts created by a specific combination of keys. One example of a shortcut you may use a lot is: [ctrl + c] to copy items to the clipboard. 

Just so you're aware, the symbol associated with the control key is `^` (carat). You may see this written in some documentation instead of "ctrl".

For those of you who like to dive right in, I've created a table to explain some basic functions.  You can also access the keybindings screen for a full list.

In the table, I use `highlighting` to help illustrate the proper key combinations. You do not hit all the keys at once. Instead you will hit [ ctrl + a ]  and then `the specified key`. It's important to note that these shortcuts are case sensitive. Like most things on linux, they can also be customized. This can be achieved by editing the `.screenrc` file which can usually be found in `/etc/screenrc`

#### Quick Reference Table
|Function|Shortcut|
|--|--|
|Detach Screen|  [ctrl + a] + `d`|
|Quit/Kill Screen |[ ctrl + a ] + `k`|
|Switch to Next|[ ctrl + a ] + `n`|
|Switch to Previous|[ ctrl + a ] + `p`|
|All Keybindings|[ ctrl + a ] + `?`|

# Examples
I will look at these common management tasks in an easy to follow linear method. This will effectively put you in the driver seat as you demo the functionality.

## Start and Name a Session

```
screen -S top
```

You can start screen and apply a memorable name. For this instance, I've created one called `top`. It automatically launches the named session and I can accomplish whatever task I need to. I will start an instance of `top`. I will then use the `[ctrl + a] + d` keyboard shortcut to detach it. Top will continue to run in the background, but I am taken back to the screen application.

From here, I can start another session. Let's call it `free` and enter:

```
watch free
```
This will constantly monitor RAM usage. If you're not familiar with free, check out our article [here](https://linuxhandbook.com/free-commmand).

```
Every 2.0s: free                                                  pop-os: Sun Dec 22 02:25:32 2019

              total        used        free      shared  buff/cache   available
Mem:       32596848     5500212    22689952      894876     4406684    25801480
Swap:             0           0           0
```

Detach once again using the `[ctrl + a] + d ` keyboard shortcut. So we have two processes running now in the background. 

How do you get back to your processes to check on them? 


## Basics of Managing Screen Sessions

### Quick Re-attach
We can use the session name to easily re-attach a screen. 

```
screen -r free
```
![Perform Quick Re-attach](/img/screen-01-quick-reattach.gif)

You can see this in action above. If you're not getting the same results, you may have made a mistake when naming the session (or forgotten all together). This is nothing to panic about.

We can use the following command to list all of our open screen sessions.

### List All Sessions
```
screen -ls
```

Since I detached my free session again to enter this, I get the following output:

![Perform Screen -ls](/img/screen-02-screen-ls.gif)

### Use PID for Re-attachment
If you didn't name your sessions, they will be identifiable by an assigned PID and a computer ID. You can use the process ID (PID) to access the desired screen just like you would for a named session. 

```
screen -r 685
```

This is the PID associated with the screen I've named "free". 

## Closing Screens

Okay, if you're following along you should have the `free` session open. Let's get rid of it and stop it from running.

We use `[ctrl + a]+ k` to kill the active screen. A message will appear in the bottom left with a confirmation prompt. Enter `y` to exit the session. After a moment you will be left with something like this:

```
christopher@linuxhandbook:~$ screen -r free
[screen is terminating]
```
We can confirm by running `-ls` again.

![Perform Kill and Ls](/img/screen-03-kill-screen.gif)

As you can see, the free screen is no longer active. 

## View Multiple Windows at Once
We've demonstrated how using screen can save you time and make you more productive. There is a way to make this great tool even better, though. 

What truly makes screen indispensible is the ability to split the terminal into multiple windows within one session arranged horizontally or vertically. 

Screen will use the active area to perform the split functions and create screen functions. Once a split is created, it will become the active area. However, you may find that you cannot input anything on the active window. You will need to create a screen in order to do that. You can initialize the shell by using  `[ctrl + a] + c`. 

#### Shortcuts for Splitting and Navigating Windows 
The following commands are the essential shortcuts for managing multiple windows within a screen session. 

Feel free to create your own arrangement and explore. You can split into many sessions, but I find that, for me personally, anything beyond a quadrant makes text difficult to read. 

In the table, you can see the option to rename windows. This is different than the naming of screens we performed earlier with `screen -S [name]`. You will notice the window name in the bottom left corner. You can get a list of windows with their corresponding names and ID's by entering `[ ctrl + a ] + ["]`.

#### Table of Window Management Commands

|Function|Shortcut|
|--|--|
|Split Horizontal (Left / Right)|[ ctrl + a ] + `S`|
|Split Vertical (Top / Bottom) |[ ctrl + a ] + `|`|
|Create Screen / Start Shell| [ ctrl + a ] + `c`|
|Switch by Window ID| [ ctrl + a ] + `0` , `1` ,  etc.|
|Rename Window| [ ctrl + a ] + `A`|
|Close Active Window| [ ctrl + a ] + `X`|
|Close All Inactive Windows| [ ctrl + a ] + `Q`|
|Switch to Next Window| [ ctrl + a ] + `[tab]`|

Remember, you can use all the functions we explored earlier within the new windows also. There are a ton of possibilities to explore. 

![Example of Multi-Screen View](/img/screen-04-multiple-screens.gif)

Here is an example of a setup using `top`, `free`, and `df`.

## Conclusion
There are so many ways to customize your terminal using GNU Screen. It's a really great way to improve your productivity and make your workflow a little simpler when you're doing administration tasks via the command line. Especially, if you're working on a remote machine. 

If you are new to this, leave us a comment and let us know if you enjoyed the tutorial. If you're more experienced, feel free to share some of your go-to setups with other readers. We love feedback from our readers.
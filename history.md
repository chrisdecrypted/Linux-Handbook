# History Command in Linux
Let's face it, us humans are not great at remembering things. Sometimes being forgetful can be very frustrating and lead to painful consequences. 

Unlike us, computers are capable of near-perfect memory. One example is the history command in linux. This program keeps track of everything that we type into the command line. 

It sounds pretty simple, and it is. You'd be surprised how often this tool can come in handy though!

Let's walk through some examples that will improve our command-line skills and make us more productive.

## Some Background Information
To understand the history command better, we will look at what settings can be configured by the user. 

The typical default for the number of commands logged is `1000` on Ubuntu, but it can vary from system to system. The settings for history are set by your bash profile (Normally `~/.bashrc`). There are several history file settings that are editable from this file including the location of the log file.

By default, command history is usually logged to `~/.bash_history`.

```
christopher@linuxhandbook:~$ cat ~/.bash_history
sudo apt-get clean
#sudo e4defrag /
df -h
sudo e4defrag /
sudo fstrim /
sudo -s
poweroff
ls
```

# Examples

## 0) Use Arrow Keys
Many of us don't think of what the command line was like before we knew this trick. If you don't already know, using your up/down arrow keys lets you quickly scroll through your command history. This is great for when you make a mistake while entering some long complex command. Just hit the up arrow, and correct it. Done. 

## 1) Default Settings
Let's start with something simple. We're just going to enter the command and see what is returned.

```
history
```

This will return a numbered list of your recently entered commands. 

```
christopher@linuxhandbook:~$ history
    1  sudo apt-get clean
    2  #sudo e4defrag /
    3  df -h
    4  sudo e4defrag /
    5  sudo fstrim /
    6  sudo -s
    7  poweroff
    8  ls
    9  history
```
Looks familiar, right? This is the content from our `.bash_history` file, plus a new entry for `history`. 

In fact, new entries will not be reflected in the file until you close the shell. 

## 2) Using Indexed Commands
Did you notice that our commands were numbered when we ran the history command? To re-run a specfic command quickly, type `!` and then the number.

```
christopher@linuxhandbook:~$ !8
ls
Desktop    Downloads         fontconfig  Pictures  Templates
Documents  examples.desktop  Music       Public    Videos
```

## 3) Delete a Specific Entry
If you made a mistake, you can erase a specific item with the `-d` option followed by the line number. Let's erase line 9.

```
christopher@linuxhandbook:~$ history -d 9
christopher@linuxhandbook:~$ history
    1  sudo apt-get clean
    2  #sudo e4defrag /
    3  df -h
    4  sudo e4defrag /
    5  sudo fstrim /
    6  sudo -s
    7  poweroff
    8  ls
```

## 4) Clear the History
Maybe you want to get rid of more than one line. We can erase the entire history using the `-c` option. 

```
christopher@linuxhandbook:~$ history -c
christopher@linuxhandbook:~$ history
    1  history
```

## 5) Searching History
Obviously, my history file is now fairly short since I've just cleared it. However, with the potential to have up to 1000 commands, things can get messy quickly. Fortunately, you can use tools to search history to help find that complex command you used earlier.

### Use Grep
Here's an updated list of our history.
```
christopher@linuxhandbook:~$ history
    1  history
    2  ls
    3  ll
    4  cd
    5  cd ..
    6  cd 
    7  ls
    8  ll
    9  history
```
Now, I am going to use the history command piped with a grep command to find entries containing the character `l`. 

```
christopher@linuxhandbook:~$ history | grep l
    2  ls
    3  ll
    7  ls
    8  ll
   10  history | grep l
```

You can also search your commands using the reverse-i-search tool. If you hit `ctrl+r`, you will see a new prompt that you can use to search your command history.

### Use reverse-i-search
```
christopher@linuxhandbook:~$ 
(reverse-i-search)`': 
```
You can start typing and it will return results as you add letters. 

Both grep and the reverse-i-search can be used to make your life easier.  

# Conclusion
Did you enjoy our guide to the `history` command? I hope all of these tips taught you something new. If you like this guide, please share it on social media. If you have any comments or questions, leave them below. If you have any suggestions for topics you'd like to see covered, feel free to leave those as well. Thanks for reading. 
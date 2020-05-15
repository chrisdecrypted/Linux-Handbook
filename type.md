# Type Commad in Linux

The `type` command in Linux shares nothing with the Windows command of the same name. Instead it is a utility that can provide the type of a specified command. This shows the user how the command name entered is being interpreted by the shell. This definition may seem like it is a bit circular. Let's look at some examples to get some clarity on when and why we may want to use this command. 

# Syntax
```
type [options] name
```
# Examples

## 1) Type without Options
To get started, let's use the type command without options on a well-known system command. 

```
christopher@linux-handbook:~$ type echo
echo is a shell builtin
```
It tells us that echo is a shell builtin command. This is the `type` of command that would run if the name echo is interpreted by the command line. Hopefully that clarifies some of the confusion.

You're probably already familar with aliases in Linux. If not, these are psuedo commands that work like shortcuts. They can be set in your shell profile. 

Now if "echo" were an alias, it would display that instead of the shell builtin info. Let's look at an example.

## 2) Type of an Alias
Here's what that looks like using a known alias name. We're going to use one that is generally created by default in Linux.

```
christopher@linux-handbook:~$ type ll
ll is aliased to `ls -alF'
```

Again, `ll` is an alias for `ls -alF`. This is the expected output.
 


## 3) Return the Type of Multiple Names
We can also use type with multiple names and get the results echoed back to us. 

```
christopher@linux-handbook:~$ type ls ll
ls is aliased to `ls --color=auto'
ll is aliased to `ls -alF'
```

## 4) Force Type to Return a Path (-P)
We may want to force type to return the path. For example `ls` is an alias, but if we want to know the system path, we can type the following:

```
christopher@linux-handbook:~$ type -P ls
/usr/bin/ls
```
This will return the path name even if it is not an executable file. The option `-p` can be used for files, but will return nothing on shell built-ins. 


## 5) Return All Information With -a
We can get the most complete information using `-a`. 
```
christopher@linux-handbook:~$ type -a ls
ls is aliased to `ls --color=auto'
ls is /usr/bin/ls
ls is /bin/ls
```

This shows us both the type information and every location on the system path with the file.

## 6) Return Name Type Only

#### Types are defined as being one of the following:
+ Alias 
+ Builtin 
+ File
+ Function 
+ Keyword

You can prompt for only the type with the `-t` option. Here are a few examples:

```
christopher@linux-handbook:~$ type -t ls
alias
christopher@linux-handbook:~$ type -t echo
builtin
christopher@linux-handbook:~$ type -t sort
file
christopher@linuxhandbook:~$ type -t _mac_addresses 
function
christopher@linuxhandbook:~$ type -t if
keyword
```
# Conclusion
Did you enjoy our guide to type? I hope all of these tips taught you something new. If you like this guide, please share it on social media. If you have any comments or questions, leave them below. If you have any suggestions for topics you'd like to see covered, feel free to leave those as well. Thanks for reading. 



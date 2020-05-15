# Source Command

The `source or .` command executes commands from a file in the current shell. It can also be used to refresh environment variables.

Syntax
```
source filename [options]

OR

. filename [options]
```

# Getting Started

The syntax of this command is simple, but understanding it requires a slightly deeper look at some Linux concepts. If you're brand new to Linux or programming, you might only have a vague idea about what a variable is. If you've heard this term, but don't know exactly what it means. That is okay! Remember, all of us start from exactly the same place. No one suddenly wakes up in the morning being a system administrator or programmer. 

I will give a brief explanation before moving on.

You may skip to the next header if you're already familiar with how to create variables in bash. 

## Overview of Variables

We can open any bash terminal and create new variables. A variable can be thought of as a placeholder that can be used to point your system to a piece of information (letters, numbers or symbols). Let's look at an example.

I am going to make a new variable called `name` and I'm going to assign the value `Christopher`. 

In bash this is done using the formula: `variable_name=your_variable`. Do not add any spaces between  `=` symbol and your text.

```
christopher@linuxhandbook:~$ name=Christopher
christopher@linuxhandbook:~$ echo $name
Christopher
```
What happens if I just type the variable name?

```
christopher@linuxhandbook:~$ echo name
name
```
If you forget this symbol, bash will return the text that you've entered. Here, I tell it to `echo`, or print, "name". Without the `$` symbol, bash does not recognize that you want to use the variable you've created.

Your variable will be inserted where it is called. So I can also include it in a sentence like this: 

```
christopher@linuxhandbook:~$ echo "Hello, $name. $name is a great name. It's good to meet you."
Hello, Christopher. Christopher is a great name. It's good to meet you.
```

There are many things you can do with variables, but I'm hoping that primer will be enough to allow anyone reading this to understand how they work.

# Environment vs Shell Variables

For the next key to understanding `source`, let's talk about persistance. This is an easy way to think about the difference between shell and environmental content. You might also think of it in terms of "portability" depending on the context.

Simply put, if you create a variable in a terminal shell, it will be lost once you exit that shell.

In contrast, an environmental variable has persistance in your operating system.  These variables typically use all caps to distinguish themselves. An example of this is your username which is known by the OS as `$USER`.

```
christopher@linuxhandbook:~$ echo $USER
christopher
```

# Using Source / . (dot)
Okay, so we spent quite a bit of time going over the  differences between environment and shell variables. What does that have to do with `source`? Everything, really. 

Otherwise there would be no difference in running `source` and `bash`. In order to illustrate this point, I have one more demonstration lined up. 

# Source vs. Bash
If you've been around Linux for a little while, you may have encountered these commands and thought they did the same thing. After all, both commands can be used to execute a script. 

`Source` works in the current shell, unlike running `bash` which creates a new shell. This isn't obvious since no new windows are displayed. 


If you're following along, this one will require us to write a very simple script that will look like this:

Contents of `echo.sh`:
```
#! bin/bash

echo $USER
echo $name
```

Before we do anything else in your terminal, assign your name to the variable name.

```
christopher@linuxhandbook:~$ name=Christopher
```
Next, I am going to show you what happens when we try all 3 commands in the same terminal that we assigned our variable in.

```
christopher@linuxhandbook:~$ bash echo.sh 
christopher

christopher@linuxhandbook:~$ source echo.sh 
christopher
Christopher
christopher@linuxhandbook:~$ . echo.sh 
christopher
Christopher
```
As you can see, our local variable was not recognized when we executed our script via `bash`.

## Refresh Environment Variables

Source can also be used to update environmental variables in the current shell. A common application for this task is updating your bash profile in the current shell.

A user may want to modify their bash profile to, say, create an alias. Normally, once you save the configuration you will need to open a new terminal window for the changes to take place.

```
christopher@linuxhandbook:~$ source .bashrc 
```
Running this will refresh the settings in your current shell without forcing you to open a new terminal. 

## Conclusion
We hope that you enjoyed this tutorial on the `source / .` command. As always, please let us know your thoughts in the comment section. If you enjoyed this post please share it on social media using the buttons below.



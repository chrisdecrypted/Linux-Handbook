# Time Command in Linux

This is a simple command that measures... you guessed it, time. It is not a clock application, though. It measures resource usage. 

There are a few different versions of the time utility. Here we will be looking at the Bash version, since this is the one you're most likely to encounter on your system. There is also a Zsh version and a GNU version. 

Let's avoid confusion and verify your version now. We are going to use the type command. We will be publishing an article on `type` soon and include a link here once it is up. For now, all you need to know is that it is a great tool for clarifying objects in Linux.

```
christopher@linuxhandbook:~$ type time
time is a shell keyword
```

If your output looks like this, that's perfect. That means that you are using bash. The command performs the same task in all its iterations, so if you're not using bash, fear not, you will still be able to understand what is happening. However, it may look quite different. 

## Examples

Time will measure the real time (total time elapsed), user (OS processing in User Mode), and sys (OS processing in kernel mode). It can be used with any command or piped commands. 

Let's look at an example with nano. Nano is a terminal based text editor. If we start nano and then promptly exit through the application (CTRL+X), our output will look like this:


## Time with a Text-Based Application
```
time nano
```
[exit nano]

```
real	0m1.465s
user	0m0.031s
sys	    0m0.006s
```

## Time with a GUI Application
This is also works with a GUI application. The output will be returned once the application is exited normally or if an interrupt (CTRL+C) is input at the terminal. 
```
time firefox
real	0m6.784s
user	0m4.962s
sys	    0m0.459s
```

## Traditional GNU Version
As I touched on before, most Linux users run Bash, which essentially uses a shortcut to create human readable content. You can run the full GNU version by using the escape character `\`. This will bypass the built-in shortcut.

This time I will just use sleep to create a dummy job. The number is the duration in seconds. You will also see this reflected in the output's real time. Note that because it is a dummy task, there is no actual resource time devoted to it. 

``` 
christopher@linuxhandbook:~$ \time sleep 3
0.00user 0.00system 0:03.00elapsed 0%CPU (0avgtext+0avgdata 1944maxresident)k
0inputs+0outputs (0major+75minor)pagefaults 0swaps
```

This output is a little more difficult to read but it also shares some information about RAM usage that you might find helpful. 



## GNU Time -p = (bash) time
The output that we normally see with the bash version is kind of like an alias to GNU time run with the `-p` option.
```
christopher@linuxhandbook:~$ \time -p sleep 3
real 3.00
user 0.00
sys 0.00
```
As you can see this gives us the same output as if we had run it with the bash shortcut.


# Conclusion
Did you enjoy our guide to the `time` command? I hope all of these tips taught you something new. If you like this guide, please share it on social media. If you have any comments or questions, leave them below. If you have any suggestions for topics you'd like to see covered, feel free to leave those as well. Thanks for reading. 
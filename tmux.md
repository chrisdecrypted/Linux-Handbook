# How to Use Tmux

With `tmux`, we are able to create multiple terminal sessions that can be opened (attached) and closed (detached) or displayed simultaneously all from one window.

Learning how to use a multiplexer will save you a lot of headaches if you spend a lot of time in the terminal. This is especially true if your work involves accessing remote machines via command line only.

## Screen vs. Tmux

Tmux is considered to be the next evolutionary step forward from the [GNU Screen](https://linuxhandbook.com/screen-command/) multiplexer. 

If you're used to screen, you'll find it easy to get started right away. There are many similarities between the two applications. We had a great response to our screen article, and I feel like our readers will really enjoy using some of the updated features of tmux.

If you are already comfortable with screen, you can quickly scan this article for the differences. For some commands, I may point out similarities or differences. Aside from these notes, this article will not presume any previous knowledge.

## Don't Worry

If you are a little lost and don't know what this article is about yet, that is totally fine. We're going to walk through everything together. I will show you how to install tmux and how to perform basic operations. 

## Check for Installation

First, you'll want to see if this software is already included with your Linux distribution. You can quickly check to see if it's installed by simply typing the name of the software in your terminal.

```
tmux
```
If tmux starts for you, you can move on to the next section. If you get an error message, you'll need to install it. 

Tmux is not installed on my system by default, so I will type:

```
sudo apt install tmux
```

If you are using a different package manager, this command may be different.

## Getting Started

As we touched on, tmux is a great application to make you more productive. It is a powerful piece of software, but it can be a little confusing to get started with. I will guide you through critical features one at a time. My goal is to ease you in and show you the basic functionality. There are so many ways to customize tmux, we won't be able to cover everything in this article. If your curious about an article on advanced features and functionalities, let us know in the comment section!

Now that you have tmux installed, let's get started. 

## Create Your First Session
```
christopher@linuxhandbook:~$ tmux
```
This should bring you into tmux. You will see a command prompt as usual, but you will now see a taskbar style menu on the bottom of the terminal that will say something like `bash 0 *`. The asterisk indicates that this is your active session.

Let's create a couple sessions that we can switch between. We will do this by using the prefix `[ctrl + b] + c`. 


##### NOTE: If you are an experienced Screen user, you may be used to using [ctrl + a] prefix. Editing the configuration file will allow you to change the prefix if you would like. I actually found the alternate key combo improved my efficiency, but I also understand old habits are hard to break.

You should see on the taskbar that a session named `bash 1` has been added. Let's add one more before we continue.

It should look like the screen shot below. You should have a total of 3 new terminal windows. 

![Tmux with 3 Open Windows](/img/tmux-3-open.png)


#### Navigation Basics
Remember that `ctrl+b` (simultaneously) is like our "tmux" key. It tells the software that we want to enter a command. Look at the table below to get started navigating the tmux interface.


Previous | Next | `n` (0, 1, 2, 3 etc.)
|--|--|--|
[ctrl + b] + p | [ctrl + b] + n |  Switch to `n` Window: [ctrl + b] + `0` 

Now we can move "back and forth" or select a specific instance by it's ID number. Try those things out until it feels comfortable. 

Ready? Awesome. Let's check out some of the other functionalities.


## Name Your Session
You may find it helpful to name your sessions with meaningful titles to keep things organized. Let's try naming our first session with tmux. 

We can name it anything that we want, but in this case we will name it `free`. Enter the following command:

```
tmux new -s free
```

You should now have a new session of tmux running. If you look in the bottom-left area of the window, you will see the name of your session rather than the generic 'bash'. 

#### Note: Tmux can actualy identify certain programs and rename your windows automatically.

## Detach a Session
Before we continue, let's begin running 'free' with the 'watch' command which will update the results every 2 seconds. 

```
watch free
```

If you are not familar with `free` or `watch`, I reccommend that you check out our other articles on those commands. Knowledge of their functionality, however, is not essential for using them with tmux. 

Okay, so once the program begins, go ahead and detach the session. Use `[ctrl + b] + d` to do this.

This should return you to a standard command prompt. 

## View Current Sessions
What happened to our session? It is still running in the background. We can re-open the session by name or by ID number, but what if you forget those?

There is a list function built into tmux. 

```
tmux ls
```
This will list all your current tmux sessions. Running it will produce output like this:

```
christopher@linuxhandbook:~$ tmux ls
free: 1 windows (created Sat Feb 29 03:16:31 2020) [80x23]
```

## Reattach
To reopen our session we can use the following command

```
tmux attach-session -t free
```

Here is an animation that shows all these steps up until this point of the demonstration. 

![Animation of Previous Commands](/img/tmux-name-detach-attach.gif)

## Multiple Panes
Now that we have that have an understanding of the basiscs, we can practice using multiple panes. 

Horizontal (Left/Right) | Vertical (Up/Down) | 
|--|--|
[ctrl + b] + % | [ctrl + b] +  " | 

Let's get some practice with these commands by creating a vertical split followed by a horizontal split.

```
[ctrl + b] + " 
[ctrl + b] +  %
```

If you've entered the commands in that order, you should have three panes that look this: 

![Tmux Split Horziontally and Vertically](/img/tmux-split.png)

## Switching Between Panes
To switch between panes you will use the tmux prefix `[ctrl+b] + arrow keys`. This cycle the panes in the direction you choose. The selected pane will be highlighted in green. 

## Switch Using Window List
Another option uses `[ctrl+b] + w`. This gives us a visual overview of sessions. You can use arrow keys to select the desired windows/panes.

![Switch Sessions Using Prefix + W](/img/tmux-prefix-w.png)

## Zoom
You can also "zoom" into a selected pane with the `[ctrl+b] + z`. This will bring the selected screen to full size. To exit the zoom mode, hit `[ctrl+b] + z` again.

## Closing Panes and Windows
This is an important one. You can close a pane (splits) by using the prefix + `x`. In order to close the  window (tabs), use the prefix + `&`.

## Conclusion
Thank you for following along with our introduction to `tmux`. As you can see there are a wide variety of applications. I hope that this basic overview has given you some ideas about how you can use tmux to improve your workflow. As always, if you have any questions, please leave them below in the comment section.

# How to Use Tmux 
With Tmux, we are able to create multiple terminal sessions that can be opened (attached) and closed (detached) or displayed simultaneously all from one window. 

Learning how to use a multiplexer will save you a lot of headaches if you spend a lot of time in the terminal. This is especially true if your work involves non-gui remote servers or similar.

## Screen vs. Tmux
Tmux is considered to be the next evolutionary step forward from the [GNU Screen](https://linuxhandbook.com/screen-command/) multiplexer. 

If you're used to screen, you'll find it easy to get started right away. There are many similarities between the two applications. We had a great response to our screen article, and I feel like our readers will really enjoy using some of the updated features of tmux. 

I will make some special notes about functionality differences between screen and tmux for experienced users. If you are already comfortable with screen, you can quickly scan for the differences. Aside from that, this article will not presume any previous knowledge. 

## Don't Worry...
If you are a little lost and don't know what this article is about yet, that is totally fine. We're going to walk through everything together. I will show you how to install tmux, how to perform all the basic operations, and give you some notes about configuration too.



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
We use `apt` in our articles because the majority new users are likely to be using debian-based systems. If you are using a different package manager, this command may be different. 

## Getting Started
We've already touched on why you might want to use multiple terminal sessions together. The options are widely varied. With this kind of software, you can "switch" between different apps or view an overview of different system process all from one view by creating different panes within a single window. 

This article is meant as only an introduction. Our intent is to give you enough to get you started using tmux.





















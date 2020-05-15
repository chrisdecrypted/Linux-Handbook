# Ulimit Command in Linux

`Ulimit` is a built-in shell command designed to display, allocate, and limit resources. It is essential for any system to regulate these types of controls.

This type of control can be enforced at the global, group, and user levels. In addition to ensuring smooth processing of tasks, it  prevents unwanted processes from being able to devour system resources like RAM, and CPU power. 

Ulimit is linked to a security configuration file. Your exact location may vary but it is typically something like `/etc/security/limits.conf`. Ulimit allows us to edit that configuration quickly.

## Soft vs Hard Limits
As a user, you can actually adjust your ulimit settings. 

You may be wondering why even set a limit if a user can adjust it. This is where soft and hard limits come into play.

So from the admin perspective, you may prefer your user to hover around a certain value. This would be your soft limit (let's say 25). Then, you could establish a hard limit that could not be exceeded by that user (50). The user would be authorized to increase their limit from 25 up to 50.

## Syntax 
```
ulimit <options>
```
# Examples
Let's get started by taking a look at our own user settings. To do this, you will type:
```
ulimit -a 
```
The `-a` flag will display all options and their configuration for your specific user name.

This gives me the following output:
```
christopher@linux-handbook:~$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 31503
max locked memory       (kbytes, -l) 65536
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 31503
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```

Your default values may be different than mine, of course. This view displays a description, the assigned flag, and the configuration. 

## Display Hard/Soft Limits
It is also possible to see either of these respective limits with a flag. 

Soft:
```
ulimit -S
```

Hard:
```
ulimit -H
```
You can also combine these with specific flags from above. So if we want to check the hard limit on the maximum number of user processes, we would type:

```
christopher@linux-handbook:~$ ulimit -Hu
31503
```

Now, let's change that value to 31500 for demonstration purposes and check the hard limit again.

```
christopher@linux-handbook:~$ ulimit -u 31500
christopher@linux-handbook:~$ ulimit -Hu
31500
```


## Limitations 
It is worth noting that any changes your priviliege allows you will only be temporarily written and affect your current shell. 

To confirm this, I exited my shell and created a new terminal and got the original default value. 

```
christopher@linux-handbook:~$ ulimit -Hu
31503
```

## Changes as Root 
Now if I want to change another user, I would have to make changes to the security file as root. Even if you wanted to change your own account, the edits will not have an effect.

When editing you need to include these four elements: `<domain> <type>  <item>  <value>`.


Here is a table that includes possible item keywords and their descriptions:

Item Keyword |Description|
|--|--| 
core | limits the core file size (KB)
data | max data size (KB)
fsize | maximum filesize (KB)
memlock | max locked-in-memory address space (KB)
nofile | max number of open file descriptors
rss | max resident set size (KB)
stack | max stack size (KB)
cpu | max CPU time (MIN)
nproc | max number of processes
as |  address space limit (KB)
maxlogins |  max number of logins for this user
maxsyslogins |  max number of logins on the system
priority  | the priority to run user process with
locks |  max number of file locks the user can hold
sigpending |  max number of pending signals
msgqueue |  - max memory used by POSIX message queues (bytes)
nice  |  max nice priority allowed to raise to values: [-20, 19]
rtprio | max realtime priority
chroot | change root to directory (Debian-specific)

Limit Type |Description|
|--|--| 
hard | hard limit
soft | soft limit
- | both hard and soft limit


Here is the text I appended to the file:
```
christopher	hard	nproc	2000
```
I have added this restriction to my account to show you what happens. 

Keep in mind that it is a best practice not to enable the root account unless you are fully aware of the potential consequences. I've done this on a virtual machine so you don't have to do it yourself. 


```
christopher@linux-handbook:~$ su
Password: 
root@linux-handbook:/home/christopher# nano /etc/security/limits.conf 
root@linux-handbook:/home/christopher# exit
exit
christopher@linux-handbook:~$ ulimit -u
20000
```
As you can see the limit for `christopher` was changed to 20000. 

## Groups
If you want to change settings for a group of users, you will once again have to be logged in as root. Changing a group policy is very similar to user policy's but you will include an `@` symbol before the name of the group. 

Here's an example pulled from the comments.
```
@student    -   maxlogins   4
```

# Conclusion
Did you enjoy our guide to ulimit? I hope all of these tips taught you something new. If you like this guide, please share it on social media. If you have any comments or questions, leave them below. If you have any suggestions for topics you'd like to see covered, feel free to leave those as well. Thanks for reading. 
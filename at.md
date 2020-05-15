# At Command

The `at` command in linux can be used to schedule jobs that do not run on a regular schedule. 

At can be compared to Crontab, which is better for automating recurring tasks. You can learn more about Cron by reading our in-depth tutorial [here](https://linuxhandbook.com/crontab/). 

## Syntax
```
at [options]
```

## Installation 
Before we get started, it should check to see if `at` is installed on your system. It is not installed by default on all operating systems. 

We can check by typing: 
```
at -V
```
If the software is already installed, this will return the version number.

If not, it can be installed on Debian based systems by typing:

```
sudo apt install at
```
If you're using a different distribution, then you may need to modify this command to reflect the package manager used by your OS. 

## Getting Started
At is actually a series of commands that work together to schedule jobs. As I already mentioned, `at` is preferred for situations where your task is more of a "one-off" than a recurring event. I've made a table with some of the basic commands associated with `at`. 

|Command| Meaning |
|--|--|
|at | allows user to schedule task|
|atq| lists queued jobs for the logged-in user, or all users if run as sudo|
|atrm| removes jobs by specified job number|
|batch| instructs the system to only run the job at the specified time if system load is at a certain level (load average of <1.5)

## Usage

Using `at` has its own unique format. When you want to schedule a job, you will type into your terminal:

```
at [time] [date/day]
```
The time is mandatory, but the date is optional, if nothing is input, it will make an assumption based on the current date and system time. 

When you hit enter, you will be prompted to input commands. You can enter as many as you like. Type 'ctrl + d' to save and exit. 

### Enter Time/Date Using Natural Language 
You have many different options for entering time. Unlike crontab with its somewhat tricky asterisk based system, `at` recognizes "human" input more efficiently.

There are many human like expressions that can be understood by the software. A lot of these are locale specific. It can recognize common expressions like "midnight" or "noon". It can also differentiate between AM and PM. Likewise, it can recognize different formats for days and dates, including abbreviations.

It can also utilize the expression "now". You can simply enter the command like below and it will run the command in 5 minutes.

```
at now + 5 minutes
```


## Example 1 : Using Relative Time
```
christopher@linuxhandbook:~$ at now + 1 min
warning: commands will be executed using /bin/sh
at> echo "Look at you, using at like a champ!" > message.txt
at> <EOT>
job 8 at Mon Jan  6 02:59:00 2020
```
You can most likely ignore the warning about `bin/sh`. It could potentially cause a headache if you are using a different shell. The vast majority of Linux distros come with bash (or more recently on Ubuntu dash) as the system shell symlinked as "sh"... It's a long story.

So, it's been about a minute, right? Let's check our directory for a new file.

You should have a file called 'message.txt' containing our text. 

```
christopher@linuxhandbook:~$ ls m*
message.txt
```
Looks good, but did it capture our message properly?

```
christopher@linuxhandbook:~$ cat message.txt 
Look at you, using at like a champ!
```
## Example 2: Using a Specified Time/Date
For our first job, we used the "relative" time `'now + [time]'`. This is a great easy way to schedule a job, but you may want to get more specific. This time, let's schedule 3 jobs at different times.

We will use our message.txt file for the demonstration. Each job will change the text of the file. 

#### 1) Set up the first job for a specific time (5 mins from now)
```
christopher@linuxhandbook:~$ at 3:45 
warning: commands will be executed using /bin/sh
at> echo "5 minutes later..." > message.txt
at> <EOT>
job 11 at Mon Jan  6 03:45:00 2020
```
#### 2) Set up the second job for a specific time (10 mins from now)
```
christopher@linuxhandbook:~$ at 3:50
warning: commands will be executed using /bin/sh
at> echo "10 minutes later..." > message.txt	
at> <EOT>
job 12 at Mon Jan  6 03:50:00 2020
```
#### Verify at 3:45
```
christopher@linuxhandbook:~$ cat message.txt 
5 minutes later...
```
#### Verify at 3:50
```
christopher@linuxhandbook:~$ cat message.txt 
10 minutes later...
```

## Example 3: View Queued Jobs with `atq` 
At any time we can verify scheduled jobs using this command. It will list all currently scheduled jobs for the user who is logged in. To see all jobs on the system, you may need to use elevated privileges. 

```
christopher@linuxhandbook:~$ atq
11	Mon Jan  6 03:45:00 2020 a christopher
12	Mon Jan  6 03:50:00 2020 a christopher
```
Each job is identified by a job ID, its scheduled time, and the associated user.

## Example 4: Removing Jobs with `atrm`
If you decide to cancel a job before it is executed, this can be done by typing the command followed by its corresponding job id. 

```
christopher@linuxhandbook:~$ atrm 11
christopher@linuxhandbook:~$ atq
12	Mon Jan  6 03:50:00 2020 a christopher
```

As you can see job 11 has been removed from the queue. 

## Example 5: Use a File for `at`
Maybe you have a set of scripts that you want to run irregularly and cron isn't the right fit. You can input multiple jobs without using the standard input. 

Let's imagine a scenario where HR requests documentation for computer activity of an employee who they believe is violating work policy. You may want certain activity logs or other history information to generate a report for you at specified times.

You can save yourself time by listing the necessary scripts in a text file executing them with at. 

```
christopher@linuxhandbook:~$ cat problem_employee_logs.txt 
path/to/get_browsing_history.sh
/whatever/path/get_activity_logs.sh
```
You get the idea. So now, we can add `-f` to our at command and include the filename after like so:


```
christopher@linuxhandbook:~$ at now + 2 minutes -f problem_employee_logs.txt 
warning: commands will be executed using /bin/sh
job 16 at Mon Jan  6 05:42:00 2020
```
## Example 6: Batch 
Batch jobs will be run when the CPU load average drops below 1.5 by default. 

```
batch
```
The method for entering batch jobs is identical to `at`, except that it does not need a time to be specified.

If you want to change the load threshold, you can do so with the following command:

```
atd -l [n]
```
Where n is the load threshold you'd like to choose. The man page recommends that you change it to higher than n-1 where n is the number of CPUs in your system.

## Conclusion
Thanks for reading. I hope that your understanding of the `at` command has improved. If you have any questions or would like to share how you use this command, tell us! Leave a comment below. 



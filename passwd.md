# Passwd Command Practical Examples

Security technologies have come a long way, but the venerable password still remains one of the most common tools used to secure data. 

Many Linux desktop environments allow you to change passwords via the graphical user interface (GUI). It's still important to know how to make these changes from the command line. So let's get started.

### Syntax
```
passwd [options] [username]
```

### Password Changing Process
+ Username verification
+ Enter current password
+ Enter new password twice
+ Confirm password change

# Create and Change Passwords
## 1) Change the password of the current user (no options)
```
christopher@linuxhandbook:~$ passwd
Changing password for christopher.
(current) UNIX password: 
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
```

If you enter your current password as the new password, the system will throw an error message saying that the password is unchanged and prompt you again for a new password. 

```
christopher@linuxhandbook:~$ passwd
Changing password for christopher.
(current) UNIX password: 
Enter new UNIX password: 
Retype new UNIX password: 
Password unchanged
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
```

## 2) Create a root password
You may need root access from time to time. Many Linux distributions come without a root password set. This is because a default password like 'toor' would make a system vulnerable to attackers. 

If you have not created a root password, you may need to do so. 

You must be an admin or be part of the sudoers list for this. 

```
christopher@linuxhandbook:~$ sudo passwd root
[sudo] password for christopher:             
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
```
This is one of many reasons why it is critical to properly configure user access. You wouldn't want all users to be able to change your root password! 

```
christopher@linuxhandbook:~$ su 
Password: 
root@linuxhandbook:/home/christopher# 
```
#### I'm in.

## 3) Change user passwords as root

Now that we're logged into the shell as root, we can change any user's password.

```
root@linuxhandbook:/home/christopher# passwd christopher
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
```

# Add constraints to passwords
You may also want to place constraints and create rules about how and when passwords need to be changed.

There are also options to lock and unlock passwords that may be useful.

I will provide some detailed information here to give you some ideas about how to implement constraints. The complete list of options will be included below for you to reference. 

## Check status
```
christopher@linuxhandbook:~$ passwd -S christopher
christopher P 06/13/2020 0 99999 7 -1
```
Let's review this information. I will organize it into a table to make it easier to read. Then I will discuss what certain values mean. 

| Username | Status | Date Last Changed | Minimum Age | Maximum Age | Warning Period | Inactivity Period|
|--|--|--|--|--|--|--|
christopher| P | 06/13/2020 | 0 | 99999 | 7 | -1 |

### Status Codes
Let's look first at the status column. Here are the possible options for this field.

|Status| Description |
|--|--|
| P | Usable password |
| NP | No password |
| L | Locked password |

### Min/Max Age
There are some special numbers reserved for setting parameters on password rules. 

|Special Numbers for Age | Description |
|--|--|
| 9999 | Never expires |
| 0 | Can be changed at anytime |
| -1 | Not active |

Here you see that the warning period is set at 7 days, but because the inactivity period is disabled and the age is set to never expire, no warning would occur. 

## Expiring Passwords

### Force expiration
We can choose to set a period of days for passwords to expire and provide warning. We can also force expire a password for a specified user.

```
root@linuxhandbook:/home/christopher# passwd -e christopher
passwd: password expiry information changed.
```
Now we can check the status to note the changes.

```
root@linuxhandbook:/home/christopher# passwd -S christopher
christopher P 01/01/1970 0 99999 7 -1
```
#### Epoch Date
As you can see the password set date has been changed to '01/01/1970'. 

+ This date is historically linked to Unix systems as it's "epoch" date. This basically means that that date is day '0' (on a 32-bit scale) in the history of Unix. 

We have succesfully expired the password. The next time my account logs in, it will be forced to change to a different password. 

## Lock/Unlock 
### Lock
This feature allows you to block access for a specified user. Their password will no longer work to grant them access. 

Toggle lock:
```
root@linuxhandbook:/home/christopher# passwd -l christopher
passwd: password expiry information changed.
```
Confirm Status:
```
root@linuxhandbook:/home/christopher# passwd -S christopher
christopher L 06/13/2020 0 99999 7 -1
```

### Unlock
Unlocking is just as easy. 

Toggle lock:
```
root@linuxhandbook:/home/christopher# passwd -u christopher
passwd: password expiry information changed.
```

Confirm status:
```
root@linuxhandbook:/home/christopher# passwd -S christopher
christopher P 06/13/2020 0 99999 7 -1
```

# Complete list of options
These options can always be viewed by entering:
```
passwd -h 
```
OR
```
passwd --help
```

|Options: | Description|
|--|--|
| -a, --all       |              report password status on all accounts|
|  -d, --delete       |           delete the password for the named account |
|  -e, --expire        |          force expire the password for the named account |
| -h, --help           |         display this help message and exit |
| -k, --keep-tokens      |       change password only if expired |
| -i, --inactive INACTIVE   |    set password inactive after expiration to INACTIVE |
|-l, --lock              |      lock the password of the named account |
| -n, --mindays MIN_DAYS    |    set minimum number of days before password change to MIN_DAYS |
|-q, --quiet                 |  quiet mode |
| -r, --repository REPOSITORY |  change password in REPOSITORY repository |
|-R, --root CHROOT_DIR     |    directory to chroot into |
| -S, --status            |      report password status on the named account |
| -u, --unlock             |     unlock the password of the named account |
| -w, --warndays WARN_DAYS  |    set expiration warning days to WARN_DAYS |
| -x, --maxdays MAX_DAYS    |    set maximum number of days before password change to MAX_DAYS |

## Conclusion
I hope this tutorial was helpful in getting you started with the `passwd` command in linux.

As always, we love to hear from our readers about content they're interested in. Leave a comment below and share your thoughts with us!

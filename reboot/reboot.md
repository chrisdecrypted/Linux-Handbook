# Halt / Poweroff / Reboot Command in Linux

When personal computing first became a reality, we were more likely to power-off our machines for different reasons. Now, for the average user, power-related tasks may seem like an afterthought.

That is, until you need to reboot a remote server. Cue the reboot commmand and its related commands halt and poweroff.
This method will apply to most modern Linux distros (2010s-now).

## Syntax
```
halt [options]
```
```
reboot [options]
```
```
poweroff [options]
```

Pretty straightforward, right? There is still more to learn here though. It's important to remember that running commands like halt, particularly with options can lead erratic results like memory loss or data corruption. In other words, do not practice these commands while editing your Master's thesis.

#### Note: User privileges may require you to use `sudo` to run these commands.  


## Halt
```
halt
```
This command issues a hardware command that stops all CPU processing. The term itself comes from a much older era of computing. Back then, a signal would be sent to stop all processes and once it was safe to do so, the user would get a notification that they could turn off the machine. In a more modern context, halt will stop all processes, but doesn't send a ACPI (Advanced Configuration and Power Interface) signal. 


## Poweroff
```
poweroff  
```
The ACPI signal is the distinction between Halt and Poweroff. At least conventionally speaking. You may find that running the halt command actually turns off the power, at least without any options. To ensure this result, we want to use the designated poweroff command. This performs the actions of halt, but also sends a signal to your hardware to poweroff.

## Reboot
```
reboot    
```
Reboot performs the actions of the halt command, requiring that all processing stop. Then instead of triggering the ACPI signal, your system is restarted. 


# Options
### Force
As you might imagine, force bypasses the processes that typically faciliate a safe shutdown. This means that items running in volatile memory (RAM) are subject to corrpution or data loss. You may even lose data that was recently saved. This is not recommended. 
```
-f --force     Force immediate halt/power-off/reboot
```

### WTMP only
Does not actually perform action, but writes a logout entry to var/log/wtmp.
```
-w --wtmp-only 
```

### No WTMP
Performs designated action, but does not create record.
```
-d --no-wtmp   
```

### No Wall
Do not send a wall message before issuing command.
```
--no-wall   Don't send wall message before halt/power-off/reboot
```

# Conclusion
Did you enjoy our guide to power commands? I hope all of these tips taught you something new. If you like this guide, please share it on social media. If you have any comments or questions, leave them below. If you have any suggestions for topics you'd like to see covered, feel free to leave those as well. Thanks for reading. 
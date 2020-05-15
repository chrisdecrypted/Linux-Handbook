
# Background on Processes 
This may be the first time you've seen some of these terms. Many of us just accept that our operating system does what it needs to. We don't really question how it works, until something breaks. Read on below under background on processes to learn more.

### What does an Opearting System Actually Do, Anyway?!
You probably have some intuitive understanding of how an OS works. It makes sure that when you hit a key, a character appears on the screen. It allows you to sync your photos when you connect a device via USB. It doesn't just make hardware work with software though. 

An OS has a large range of critical jobs. Put simply, it is the most important software on your computer, but we often take it for granted. 

For understanding CPU statistics, we need to know a little bit more. 

### User vs. Kernel Modes
These modes are named for whether or not users or the more privilieged kernel have control. It is necessary, but "expensive" (in terms of resources) to switch between these modes. Generally speaking access to specific areas of hardware are off limits to user-controlled software. These types of low-level operations are done by the kernel. An example of these controls are access to

You might think of it like being a passenger and a driver in a vehicle. Passengers are free to communicate with the driv``er or even independently adjust non-critical controls like climate systems or the radio. In this analogy, the driver operates in kernel mode. 

Only they have access to the accelerator, brake, and clutch. Similarly only the Kernel has direct access to the CPU, RAM, and other critical components. This means that malicious or just poor quality software won't cause catastrophic errors if executed. 

### It's Nice to be Nice
This is a feature that is specific to Linux, but there are other kinds of priority-based process scheduling in other OS that work similarly. Nice is a value given to less important processes. The higher the value, the less priorty recieved. I have heard in the past that this is a play on the idiom "nice guys finish last". 

### Idle vs Waiting
These may sound like similar things. The words have different contexts here, though. The idle value refers to time the CPU is spent idling-- without performing any tasks. Here, waiting refers to the time that processes spend "waiting" before they can execute. An example might help to clarify that. Imagine that task 2 is waiting on task 1 to finish executing, that could be an example of waiting time. 

### Interrupts 
There are hardware and software interrupts. This allow the CPU to momentarily give precedence to a critical task. 

### Virtual Resources
In an environment with virtual machines, the tasks created by those are not seen by the CPU in the same manner. This statistic reflects that time consumed by these Virtual resources. 
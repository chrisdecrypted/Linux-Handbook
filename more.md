# More Command in Linux
The more command is helpful for viewing larger files in the terminal. While there are many ways of viewing text files in linux, users might default to using something like `cat`. This works great for files with only a few lines out of output, but larger files quickly scroll content past the user making it difficult, or even impossible for you to find what you need.

### A Look at the Problem
![Cat View ](/img/more-cat-problem.gif)

I've included this capture to demonstrate the problem with using a command like `cat` on large files. You will immediately be skipped to the end of the file. Navigation may be possible if you're using a GUI with a scrollbar, but this is far from ideal. Fortunately, there is a much better way.

### Demo Text File
For this demo, I've created a text file with 199 lines of "Lorem Ipsum". For clarification, the `more` command does not add line numbers. This was done manually to show off some of the later options. 

<!-- Link to text file --> 
For your convenience, I've included the file [here](/rsrc/more.txt). 





# Using More

![More View](/img/more-more-view.gif)

This shows the same file from before using the default settings of `more`. Now, our navigation tools can be used to help us find what we need in the file. 

## More Control
With `more` you are able to easily scroll through data one page at a time. You can use the following methods for navigation.

|Input|Action|
|----|--|
|Down Arrow / Space Bar|Scroll Down (One Page) |
|Up Arrow / B |Scroll Up (One Page) |
| Enter | Scroll One Line at a Time |
|- number |  The Number of Lines per Screenful
|+ number    |Display File Beginning from Line Number
|+/ string  |Display File Beginning from Search String Match

While using `more`, you can also enter `q` to quit at anytime or `h` to display the built-in help.

## Display n Number of Lines per Screen
![Display n Number of Lines per Screen](/img/more-n-page.gif)

Typing an `- n` (where n is an integer) after the command will display only n number of lines as a page.


## Skip the first n Number of Lines
![Skip the first n Number of Lines](/img/more-plus-20.gif)


Typing `+ n`  (where n is an integer) after the command will skip to that line number before displaying your content.

## Skip To First Instance of String (and Search within View)
![Skip To First Instance of String](/img/more-search-string.gif)

We can skip to the first instance of a specified string using `+/ string` after our command. To find the next instance, you can type `/ string` while in the more view to search.

## Run and Skip Multiple Blank Lines (-s)
![Run and Skip Multiple Blank Lines](/img/more-skip-blank.gif)
You may have been wondering why there was a large gap between the first couple items in the text file. It was to demonstrate this feature, which compresses multiple empty lines down into one for easier readability.

## Run with Help Options Displayed (-d)
![Run with Help Options Displayed](/img/more-option-d.gif)

If your audience might need help navigating, before using more with a script, you may want to include the `-d` flag. This also makes it so that any illegal character strikes suggest help methods using `h` which displays detailed instructions for navigation or exit.

## Even More Options:
As you can see from the instruction page in the above screenshot, there are also a few more tricks and tips included.

```
more --help
-d          display help instead of ringing bell
-f          count logical rather than screen lines
-l          suppress pause after form feed
-c          do not scroll, display text and clean line ends
-p          do not scroll, clean screen and display text
-s          squeeze multiple blank lines into one
-u          suppress underlining

// from the detailed instructions page accessible via h while running
<space>                 Display next k lines of text [current screen size]
z                       Display next k lines of text [current screen size]*
<return>                Display next k lines of text [1]*
d or ctrl-D             Scroll k lines [current scroll size, initially 11]*
q or Q or <interrupt>   Exit from more
s                       Skip forward k lines of text [1]
f                       Skip forward k screenfuls of text [1]
b or ctrl-B             Skip backwards k screenfuls of text [1]
'                       Go to place where previous search started
=                       Display current line number
/<regular expression>   Search for kth occurrence of regular expression [1]
n                       Search for kth occurrence of last r.e [1]
!<cmd> or :!<cmd>       Execute <cmd> in a subshell
v                       Start up /usr/bin/vi at current line
ctrl-L                  Redraw screen
:n                      Go to kth next file [1]
:p                      Go to kth previous file [1]
:f                      Display current file name and line number
.                       Repeat previous command

```


# Conclusion

Did you enjoy our guide to the `more` command? I hope all of these tips taught you something new. If you like this guide, please share it on social media. If you have any comments or questions, leave them below. If you have any suggestions for topics you'd like to see covered, feel free to leave those as well. Thanks for reading. 
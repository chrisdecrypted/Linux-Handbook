# Use the Read Command

The `read` command in linux is a way for the user to interact with input taken from the keyboard, which you might see referred to as std/in (standard input) or other similar descriptions. We are going to write some simple bash scripts and explore some of the command's different applications.

## Getting Started with Read Command

The read command can be confusing to get started with, especially for those who are new to programming. The scripts I will use are very simple and should be easy to follow, especially if you are following along with the tutorial.

### Basic Programming Concepts

With almost every program or script, we want to take information from a user (input) and tell the computer what to do with that information (output).

When we use `read`, we are communicating to the bash terminal that we want to capture the input from the user. By default, the command will create a variable to save that input to.

## Usage

```
read [options] variable_name
```

## Example 1: Read Without Options

When you type read without any additional options, you will need to hit enter to start the capture. The system will capture input until you hit enter again. By default this information will be stored in a variable named `$REPLY`.

#### Reminder: Variable names are case-senstive.

To make things easier to follow for the first example, I will use the `↵` symbol will show when the enter key is pressed.

```
read ↵
hello world ↵
echo $REPLY ↵
hello world
```

### More About Variables

As I mentioned earlier, the `$REPLY` variable is built into `read`, so we don't have to declare it.

That might be fine if you have only one application in mind, but more than likely you'll want to use your own variables. When you declare the variable with read, you don't need to do anything other than type the name of the variable.

When we want to call the variable, we will use a `$` in front of the name. Here's an example where I create the variable `Linux_Handbook` and assign it the value of the input.

We can use `echo` to verify that the read command did its magic.

```
read Linux_Handbook ↵
for easy to follow Linux tutorials.
echo $Linux_Handbook ↵
for easy to follow Linux tutorials.
```

## Example 2: Prompt Option `-p`

If you're writing a script and you want to capture user input, there is a read option to create a prompt that can simplify your code. Coding is all about efficiency, right?

Instead of using additional lines and echo commands, you can simply use the `-p` option flag. The text you type in quotes will display as intended and the user will not need to hit enter to begin capturing input.

These two blocks both have the same output, but the second one is much cleaner.

```
echo "What is your desired username? "
read username
```

```
read -p "What is your desired username? " username
```

## Example 3: "Secret"/Silent Option `-s`

I wrote a simpe bash script to demonstrate the next flag. First take a look at the output.

```
bash secret.sh
What is your desired username? tuxy_boy
Your username will be tuxy_boy.
Please enter the password you would like to use:

You entered Pass123 for your password.
Masking what's entered does not obscure the data in anyway.
```

Here is the content of `secret.sh` if you'd like to recreate it.

```
#!/bin/bash
read -p "What is your desired username? " username
echo "Your username will be" $username"."
read -s -p "Please enter the password you would like to use: " password
echo
echo "You entered" $password "for your password."
echo "Masking what's entered does not obscure the data in anyway."
```

As you can see, the `-s` option masked the input when the password was entered. This is a superficial technique and doesn't offer any security at all.

## Example 4: Using a Character Limit with Read `-n`

We can add a constraint to the input and limit it to n number of characters in length.

Let's use the same script from before but modify it so that inputs are limited to 5 characters.

```
read -n 5 -p "What is your desired username? " username
```

Simply add `-n N` where N is the number of your choice.

I've done the same thing for our password.

```
bash secret.sh
What is your desired username? tuxy_Your username will be tuxy_.
Please enter the password you would like to use:
You entered boy for your password.
```

As you can see the program stopped collecting input after 5 characters for the username.

However, I could still write LESS than 5 characters as long as I hit `↵` after the input.

If you want to restrict that, you can use `-N`. This modifcation makes it so that exactly 5 characters are required.

## Example 5: Storing Information in an Array `-a`

You can also use read to create your own arrays. This means we can assign chunks of input to elements in an array. By default, the space key will seperate elements.

```
christopher@pop-os:~$ read -a array
abc def 123 x y z
christopher@pop-os:~$ echo  ${array[@]}
abc def 123 x y z
christopher@pop-os:~$ echo  ${array[@]:0:3}
abc def 123
christopher@pop-os:~$ echo  ${array[0]}
abc
christopher@pop-os:~$ echo  ${array[5]}
z
```

If you're new to arrays, or seeing how them in bash for the first time, I'll break down what's happening.

1. Enter desired elements, separated by spaces.
2. If we put only the @ variable, it will iterate and print the entire loop.
3. The @ symbol represents the element number and with the colons after, we can tell iterate from index 0 to index 3 (as written here).
4. Prints element at index 0.
5. Similar to above, but demonstrates that the elements are seperated by the space

## Example 6: Adding a Timeout Function

We can also add a timeout to our read. If no input is captured in the allotted time, the program will move on or end.

```
christopher@pop-os:~$ read -t 3
christopher@pop-os:~$
```

It may not be obvious looking at the output, but the terminal waited 3 seconds before timing out and ending the read program.

## Conclusion

I hope this tutorial was helpful in getting you started with the `read` command in linux.

As always, we love to hear from our readers about content they're interested in. Leave a comment below and share your thoughts with us!

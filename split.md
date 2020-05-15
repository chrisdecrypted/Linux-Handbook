# Split Command with Examples

## Getting Started with Split
The `split` command allows you to break up a file into more managebale chunks. There are several ways you can customize parameters for your given application.

<strong>Note:</strong> I will not directly display output in these examples because of the large file sizes. I will use the `wc` and `ll` commands to highlight file changes. You can download the example file and read more about wc below.


## Download the Example Text File 
To help you learn about split I am using a relatively large (1.4MB) text file. I created a file of gibberish called `someLogFile.log`. You can download a copy of the file <a href=""> here</a>.

##  Quick Take on `wc` 
The `wc` (word count)  command is simple to use. It can quickly count the number of words, lines, characters, etc. in a file.

```
chris@discodingo:~/Documents$ wc someLogFile.log 
17170   53101 1369273 someLogFile.log

chris@discodingo:~/Documents$ wc someLogFile.log -l
17170 someLogFile.log

chris@discodingo:~/Documents$ wc someLogFile.log -w
53101 someLogFile.log

chris@discodingo:~/Documents$ wc someLogFile.log -c
1369273 someLogFile.log
```

By default, the output shows counts for lines, words, and bytes in a given file. You may have noticed already that 1 byte = 1 character in this ascii encoded file.

As you can see, I also separated these individual outputs using options `[-l, -w, -c]`


# Using Split

## Syntax
```
split [options] filename [prefix]
```

## 1. Split Using Defaults

` split someLogFile.log`
``` 
chris@discodingo:~/Documents$ ls
someLogFile.log  xab  xad  xaf  xah  xaj  xal  xan  xap  xar
xaa              xac  xae  xag  xai  xak  xam  xao  xaq
```
What does this output mean? It is probably confusing without any context. Remember that in Linux, files do not require extensions like '.txt' or '.zip'. By default, split creates new files for each 1000 lines. If no prefix is specified, it will use 'x'. The letters that follow enumerate the files therefore xaa comes first, then xab, and so on.

You can use `wc` to quickly check of the line counts after splitting.

```
chris@discodingo:~/Documents$ wc xaa -l
1000 xaa
chris@discodingo:~/Documents$ wc xaq -l
1000 xaq
chris@discodingo:~/Documents$ wc xar -l
170 xar
```
Remember from earlier that we saw our initial file had 17,170 lines. So we can see our program has done as expected by creating 18 new files. 17 of them are filled with 1000 lines each, and the last has the remaining 170 lines. 

Another way that we can demonstrate what is happening is to run the command with the verbose option. If you're unfamilar with verbose, you are missing out! It provides more detailed feedback about what your system is doing and it is available to use with many commands.


`split someLogFile.log --verbose`
```
creating file 'xaa'
creating file 'xab'
creating file 'xac'
creating file 'xad'
creating file 'xae'
creating file 'xaf'
creating file 'xag'
creating file 'xah'
creating file 'xai'
creating file 'xaj'
creating file 'xak'
creating file 'xal'
creating file 'xam'
creating file 'xan'
creating file 'xao'
creating file 'xap'
creating file 'xaq'
creating file 'xar'
```

## 2. Split Files Using Specific Line Number Parameters

The next option I will suggest is the `-l` tag. When this is added, we can now specify how many lines we want in each of our new files. 

`split someLogFile.log -l 500`
``` 
chris@discodingo:~/Documents$ wc -l xbh
500 xbh
chris@discodingo:~/Documents$ wc -l xbi
170 xbi
```
Now we have many more files, but with half as many lines in each one. 

## 3. Create <em>n</em> Number of Chunks with Split
The `-n` option makes splitting into a designated number of pieces or chunks easy. You can assign how many files you want by adding an integer value after -n. 

`split someLogFile.log -n 15`
```
chris@discodingo:~/Documents$ ls
someLogFile.log  xaa  xab  xac  xad  xae  xaf  xag  xah  xai  xaj  xak  xal  xam  xan  xao
```

## 4. Custom Names with Split Prefixes

What if you want to use split but keep the original name of my file or make a new name altogether instead of using 'x'? 

You may remember seeing the prefix as part of the syntax described in the begninning of the article. You can write your own custom file name after the source file, similar to other command formatting with `cp` or `mv`.

`split someLogFile.log someSeparatedLogFiles.log_`
```

chris@discodingo:~/Documents$ ls
someLogFile.log               someSeparatedLogFiles.log_aj
someSeparatedLogFiles.log_aa  someSeparatedLogFiles.log_ak
someSeparatedLogFiles.log_ab  someSeparatedLogFiles.log_al
someSeparatedLogFiles.log_ac  someSeparatedLogFiles.log_am
someSeparatedLogFiles.log_ad  someSeparatedLogFiles.log_an
someSeparatedLogFiles.log_ae  someSeparatedLogFiles.log_ao
someSeparatedLogFiles.log_af  someSeparatedLogFiles.log_ap
someSeparatedLogFiles.log_ag  someSeparatedLogFiles.log_aq
someSeparatedLogFiles.log_ah  someSeparatedLogFiles.log_ar
someSeparatedLogFiles.log_ai
```
## 5. Split and Specify Suffix Length

Split features a default suffix length of 2 [aa, ab, etc.]. This will change automatically as the number of files increases, but if you would like to manually change it, that is possible too. So let's say we want our files to be named something like `someSeparatedLogFiles.log_aaaab`. How can we do this? The option `-a` allows us to specify the length of the suffix. 

`split someLogFile.log someSeparatedLogFiles.log_ -a 5 `
```
chris@discodingo:~/Documents$ ls
someLogFile.log                  someSeparatedLogFiles.log_aaaae  someSeparatedLogFiles.log_aaaaj  someSeparatedLogFiles.log_aaaao
someSeparatedLogFiles.log_aaaaa  someSeparatedLogFiles.log_aaaaf  someSeparatedLogFiles.log_aaaak  someSeparatedLogFiles.log_aaaap
someSeparatedLogFiles.log_aaaab  someSeparatedLogFiles.log_aaaag  someSeparatedLogFiles.log_aaaal  someSeparatedLogFiles.log_aaaaq
someSeparatedLogFiles.log_aaaac  someSeparatedLogFiles.log_aaaah  someSeparatedLogFiles.log_aaaam  someSeparatedLogFiles.log_aaaar
someSeparatedLogFiles.log_aaaad  someSeparatedLogFiles.log_aaaai  someSeparatedLogFiles.log_aaaan
```
## 6. Split with Numeric Order Suffix
Up to this point, we've seen our files separated using different letter combinations. Personally, I find it much easier to distinguish files using numbers. 

Let's keep the suffix length from the previous example, but change the alphabetical organization to numeric with the option `-d`.

`split someLogFile.log someSeparatedLogFiles.log_ -a 5 -d`
```
chris@discodingo:~/Documents$ ls
someLogFile.log                  someSeparatedLogFiles.log_00004  someSeparatedLogFiles.log_00009  someSeparatedLogFiles.log_00014
someSeparatedLogFiles.log_00000  someSeparatedLogFiles.log_00005  someSeparatedLogFiles.log_00010  someSeparatedLogFiles.log_00015
someSeparatedLogFiles.log_00001  someSeparatedLogFiles.log_00006  someSeparatedLogFiles.log_00011  someSeparatedLogFiles.log_00016
someSeparatedLogFiles.log_00002  someSeparatedLogFiles.log_00007  someSeparatedLogFiles.log_00012  someSeparatedLogFiles.log_00017
someSeparatedLogFiles.log_00003  someSeparatedLogFiles.log_00008  someSeparatedLogFiles.log_00013
```

## 7. Split Files Using Size-Specific Parameter
It's also possible to use file size to break up files in split. Maybe you need to send a large file over a size-capped network as efficiently as possible. You can specify the exact size for your requirements. The syntax can get a little tricky as we continue to add options. So, I will explain how the `-b` command works before showing the example. 

When we want to create files of a specific size we use the `-b` option. 
You can then write <em>n</em>K[B], <em>n</em>M[B], <em>n</em>G[B] where <em>n</em> is the value of your file size and K [1024] is -kibi, M is -mebi, G is -gibi, and so on. KB [1000] is kilo, MB - mega etc.

It may look like there is a lot going on, but it's not that complex when we break it down. We have specified the source file, our destination filename prefix, a numeric suffix, and seperation by file size of 128kB.

`split someLogFile.log someSeparatedLogFiles.log_ -d -b 128KB`
```
chris@discodingo:~/Documents$ ls
someLogFile.log               someSeparatedLogFiles.log_02  someSeparatedLogFiles.log_05  someSeparatedLogFiles.log_08
someSeparatedLogFiles.log_00  someSeparatedLogFiles.log_03  someSeparatedLogFiles.log_06  someSeparatedLogFiles.log_09
someSeparatedLogFiles.log_01  someSeparatedLogFiles.log_04  someSeparatedLogFiles.log_07  someSeparatedLogFiles.log_10
```
We can verify the results with the 'wc' command.
```
chris@discodingo:~/Documents$ wc someSeparatedLogFiles.log_0*
1605    4959  128000 someSeparatedLogFiles.log_00
1605    4969  128000 someSeparatedLogFiles.log_01
1605    4953  128000 someSeparatedLogFiles.log_02
1605    4976  128000 someSeparatedLogFiles.log_03
1605    4955  128000 someSeparatedLogFiles.log_04
1605    4975  128000 someSeparatedLogFiles.log_05
1605    4966  128000 someSeparatedLogFiles.log_06
1605    4964  128000 someSeparatedLogFiles.log_07
1605    4968  128000 someSeparatedLogFiles.log_08
1605    4959  128000 someSeparatedLogFiles.log_09
16050   49644 1280000 total
```

## 8. Split Files into Files of 'At Most' Size <em>n</em> with - C

If you wanted to split files into roughly the same size, but preserve the line structure, this might be the best choice for you. With `-C`, you can specify a maximum size. Then the program will automatically split the files based on `complete lines`.

`split someLogFile.log someNewLogFiles.log_ -d -C 1MB`
```
chris@discodingo:~/Documents$ ls
someLogFile.log  someNewLogFiles.log_00  someNewLogFiles.log_01
chris@discodingo:~/Documents$ ll
total 2772
drwxr-xr-x  2 chris chris   81920 Jul 24 22:01 ./
drwxr-xr-x 19 chris chris    4096 Jul 23 22:23 ../
-rw-r--r--  1 chris chris 1369273 Jul 20 17:52 someLogFile.log
-rw-r--r--  1 chris chris  999997 Jul 24 22:01 someNewLogFiles.log_00
-rw-r--r--  1 chris chris  369276 Jul 24 22:01 someNewLogFiles.log_01
```

## 9. Use `-x` to Append Hex Suffixes
Another option for suffix creation is to use in the built-in hex suffix which alternates ordered letters and numbers. For this example, I will combine a few things I've already shown you. We will split the file using our own prefix I chose an underscore for readability purposes. I used the `-x` option to create a hex suffix. Then I split our file into 50 chunks and gave the suffix a length of 6.


`split someLogFile.log _ -x -n50 -a6`


```
chris@discodingo:~/Documents$ ls
_000000  _000003  _000006  _000009  _00000c  _00000f  _000012  _000015  _000018  _00001b  _00001e  _000021  _000024  _000027  _00002a  _00002d  _000030
_000001  _000004  _000007  _00000a  _00000d  _000010  _000013  _000016  _000019  _00001c  _00001f  _000022  _000025  _000028  _00002b  _00002e  _000031
_000002  _000005  _000008  _00000b  _00000e  _000011  _000014  _000017  _00001a  _00001d  _000020  _000023  _000026  _000029  _00002c  _00002f  someLogFile.log
```

## 10. Rejoining Split Files Using `cat`

This isn't a split command, but it might be helpful for new users. One of the things that I love about computers is that very few mistakes are permanent and these mistakes often teach us something useful. 


 ```
chris@discodingo:~/Documents$ ls
someLogFile.log
```
```
chris@discodingo:~/Documents$ split someLogFile.log 
chris@discodingo:~/Documents$ ls
someLogFile.log  xab  xad  xaf  xah  xaj  xal  xan  xap  xar
xaa              xac  xae  xag  xai  xak  xam  xao  xaq
```
Imagine you're experimenting with the command line and you see some code on a Linux forum and decide to try out an unfamiliar command. 

```
chris@discodingo:~/Documents$ rm someLogFile.log 
```
### Wait, `rm` does WHAT?!
Don't despair! When you run the `ls` command, you see your previously split files are unaffected. So what can we do?

```
chris@discodingo:~/Documents$ ls
xaa  xab  xac  xad  xae  xaf  xag  xah  xai  xaj  xak  xal  xam  xan  xao  xap  xaq  xar
```

We can use another command to rejoin those files and create a replica of our complete document.
 
  The `cat` command is short for concatenate which is just a fancy word that means "join items together". Since all of the files begin with the letter 'x', the asterisk will apply the command to any files that begin with that letter.
```
chris@discodingo:~/Documents$ cat x* > recoveredLogFile.log
chris@discodingo:~/Documents$ ls
recoveredLogFile.log  xab  xad  xaf  xah  xaj  xal  xan  xap  xar
xaa                   xac  xae  xag  xai  xak  xam  xao  xaq
```

As you can see, our recreated file is the same size as our original.

`wc -l recreatedLogFile.log `
```
17170 recreatedLogFile.log
```
Our formatting (including the number of lines) is preserved in the file created.

# Conclusion
If you're new to linux, I hope this tutorial helped you. If you are more experienced tell us your favorite way to use `split` in the comments below!
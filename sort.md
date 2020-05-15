# Sort Command with 11 Examples

## Getting Started

Sort arranges text lines in useful ways. This simple tool can help you quickly sort information from the command line.

### Usage
``` 
sort [options] <filename>
```
### Notes

+ When you use sort without any options, the default rules are enforced. Understanding the default rules helps avoid unexpected outcomes.

+ When using sort, your original data is safe. The results of your input are displayed on the command line only. However, you can specify output to a separate file if you wish. More on that later.

+ Sort was originally designed for use with ASCII characters. I did not test for this, but it is possible that different encodings may produce unexpected results. 

### Rules 

These are the default rules when using sort. The first few examples will clarify how these priorties are managed. Then we will look at specialized options. 
+ numbers > letters 
+ lowercase > uppercase

## Examples

### I. Alphabetical
The default sort command makes it easy to view information in alphabetical order. No options are necessary and even with mixed-case entries, A-Z sorting works as expected.

`Contents of filename.txt:`
``` 
MX Linux
Manjaro
Mint
elementary
Ubuntu
```

` chris@discodingo:~$ sort filename.txt`
```
elementary
Manjaro
Mint
MX Linux
Ubuntu
```
<!-- 2 -->
### II. Numerical [Without Options]
Let's take the same list we used for the previous example and sort in numerical order. In case you were wondering, the list reflects the most popular Linux Distributions (July, 2019) according to distrowatch.com.

I will modify the contents of the file so that the items are numbered, but out of order as shown below.

`Contents of filename.txt:`
``` 
1. MX Linux
4. elementary
2. Manjaro
5. Ubuntu
3. Mint
```

` chris@discodingo:~$ sort filename.txt`
```
1. MX Linux
2. Manjaro
3. Mint
4. elementary
5. Ubuntu
```
Looks good, right? Can you rely on this method to arrange your data accurately, though? <em>Probably not.</em> Let's look at another example to find out why.

`Contents of order.txt`
```
1
5
10
3
5
2
60
23
432
21
```

`chris@discodingo:~$ sort order.txt `

```
1
10
2
21
23
3
432
5
5
60
```

#### NOTE: Numbers are sorted by their leading characters only.

<!-- 3 -->
### III. Numeric [-n]
When you add the `-n` option, the numerical value of the string is now being evaluated rather than only the first character. Now, you can see below that our list is properly sorted.

`sort order.txt -n`
```
1
2
3
5
5
10
21
23
60
432
```
<!-- 4 -->
### IV. Reverse [-r]
For this one, I am going to use our distro list again. The reverse function is self-explanatory. It will reverse the order of whatever content you have in your file. 

`chris@discodingo:~$ sort filename.txt -r`
``` 
5. Ubuntu
4. elementary
3. Mint
2. Manjaro
1. MX Linux
```

<!-- 5 -->
### V. Random [-R]
If you accidentally mashed your shift key while attempting the reverse function, you might have gotten some strange results. `-R` rearranges output in randomized order.  

`chris@discodingo:~$ sort filename.txt -R`
``` 
4. elementary
1. MX Linux
2. Manjaro
5. Ubuntu
3. Mint
```

<!-- 6 -->
### VI. Months [-M]
Sort also has built in functionality to arrange by month. It recognizes several formats based on locale-specific information. I tried to demonstrate some unqiue tests to show that it will arrange by date-day, but not year. Month abbreviations display before full-names.

`Contents of filename.txt`
```
March
Feb
February
April
August
July
June
November
October
December
May
September
1
4
3
6
01/05/19
01/10/19
02/06/18
```
`sort filename.txt -M`
```
01/05/19
01/10/19
02/06/18
1
3
4
6
Jan
Feb
February
March
April
May
June
July
August
September
October
November
December

```

<!-- 7 -->
### VII. Output Results to Another File
As I mentioned earlier, sort does not change the original file. If you need to save the sorted content, it is easy to do.

For this example, I've created a new file where I want the sorted information to be printed and saved with the name filename_sorted.txt. 

#### <em>Caution:</em> If you try to direct your sorted data to the same file, it will erase the contents of your file.



`Contents of filename.txt:`
``` 
1. MX Linux
4. elementary
2. Manjaro
5. Ubuntu
3. Mint
```

`chris@discodingo:~$ sort filename.txt -n > filename_sorted.txt`

`[Contents of filename_sorted.txt]`
```
1. MX Linux
2. Manjaro
3. Mint
4. elementary
5. Ubuntu
```

<!-- 8 -->
### VIII. Sort Specific Column [-k]
If you have a table in your file, you can use the `-k` option to specify which column to sort. I added some arbitray numbers as a third column and will display the output sorted by each column. I've included several examples to show the variety of output possible. Options are added following the column number.

`Contents of filename.txt`
```
1. MX Linux 100
2. Manjaro 400
3. Mint 300
4. elementary 500
5. Ubuntu 200
```

`chris@discodingo:~$ sort filename.txt -k 2`

`[2nd Col Sorted A-Z]`
```
4. elementary 500
2. Manjaro 400
3. Mint 300
1. MX Linux 100
5. Ubuntu 200
```

`chris@discodingo:~$ sort filename.txt -k 3n`

`[3rd Col Sorted Numerically]`

```
1. MX Linux 100
5. Ubuntu 200
3. Mint 300
2. Manjaro 400
4. elementary 500
```

`chris@discodingo:~$ sort filename.txt -k 3nr`

`[3rd Col Sorted Numerically in Reverse]`
```
4. elementary 500
2. Manjaro 400
3. Mint 300
5. Ubuntu 200
1. MX Linux 100
```


<!-- 9 -->
### IX. Sort and Remove Duplicates [-u]
If you have a file with potential duplicates, the `-u` option will make your life much easier. Remember that sort will not make changes to your original data file. I chose to create a new file with just the items that are duplicates. Below you'll see the input and then the contents of each file after the command is run.

`chris@discodingo:~$ sort filename.txt -u >  filename_duplicates.txt`

`[Contents of filename.txt]`
```
1. MX Linux 
2. Manjaro 
3. Mint 
4. elementary 
5. Ubuntu 
1. MX Linux 
2. Manjaro 
3. Mint 
4. elementary 
5. Ubuntu 
1. MX Linux 
2. Manjaro 
3. Mint 
4. elementary 
5. Ubuntu 
```

`[Contents of filename_duplicates.txt]`
```
1. MX Linux 
2. Manjaro 
3. Mint 
4. elementary 
5. Ubuntu 
```
<!-- 10 -->
### X. Ignore Case [-f]
Many modern distros running sort will implement ignore case by default. If yours does not, adding the `-f` option will produce the expected results.

`chris@discodingo:~$ sort filename.txt -f`
```
alpha
alPHa
Alpha
ALpha
beta
Beta
BEta
BETA
```


<!-- 11 -->
### XI. Human Numeric Values
Allows the comparison of alphanumeric values like 1k (1000).

`chris@discodingo:~$ sort filename.txt -h`
```
10.0
100
1000.0
1k
```

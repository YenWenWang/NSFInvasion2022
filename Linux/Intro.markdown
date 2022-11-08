---
layout: page
permalink: /Linux/Intro
title: "Intro to Linux"
---

Please press "Hint" if only necessary.  
Press "Click to learn more!" even if you completed the tasks without hints.

<br/>

![band](../img/band.png)

<br/>

## Review
This should be quite simple if you have done the exercises before.

### Directory Navigation

What's the Present Working Directory? (i.e. which directory are you in?)
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>pwd  </pre>
</details>
<br/>

Change Directory to `LinuxIntro/Review`.
<details>
  <summary><b><u>Hint</u></b></summary>
  You can use either absolute path or relative path.
  <pre>cd LinuxIntro/Review  </pre>
  OR
  <pre>cd /[&lt;pwd&gt;]/DennyMaterials/LinuxIntro/Review  </pre>
  (replace <code>[&lt;pwd&gt;]</code> with your <code>[pwd]</code> output.)
</details>
<br/>

Go to the parent directory.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cd ..  </pre>
</details>
<br/>

Go to back to the directory you were in (`Review`).
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cd -  </pre>
</details>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  You can use <code>cd -</code> to hop back and forth between two directories.
</details>
<br/>

Go to the home directory.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cd  </pre>
  OR
  <pre>cd ~  </pre>
</details>
<br/>

### File Exploration
First, go to directory `LinuxIntro/Review/FileExploration`.  
Then, LiSt the files.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls  </pre>
</details>
<br/>

Which is the oldest file and which is the largest file?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls -lh  </pre>
  <code>-l</code> provide the details of the files and <code>-h</code> provides human-readable file size etc. <br/>
  We merged the two options together into <code>-lh</code> (This only works with single character options.)
</details>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  You can sort the files by time and size!
  <pre>ls -lht  
ls -lhS  </pre>
</details>
<br/>

You might find that some of the "files" are directories. But how to tell which one is which?
Look at the first column of your `ls -l` results. If it starts with a `d`, it's a directory! Other options include using tab completion (my personal go to), or `ls -p`, if there's a `/` after the name, that's a directory.

Now, what's in `directory"X"`, where X can be anything?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls directory*  </pre>
  <code>*</code> is one of the wildcards, it can be anything at any length! However, the syntax is not the same in every situation. We will explore other usage of wildcards later!
</details>
<br/>

What's in `directoryRecipes/FiveSpiceSeaweed`?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cat directoryRecipes/FiveSpiceSeaweed  </pre>
  OR
  <pre>less directoryRecipes/FiveSpiceSeaweed  </pre>
  To leave <code>less</code> press q.<br/>
  There are a lot more choices!
</details>
<br/>

### Super Basic File and Directory Handling
Go to directory `LinuxIntro/Review/FileDirHandle`.  
Make a file named `fileX` with `1+1=3` as its content with `nano`.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>nano fileX  
# type in 1+1=3  
# control C  
# click Y  </pre>
</details>
<br/>

Let's remove `fileX` and use `echo` and `>` instead.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>echo 1+1=3 > fileX  </pre>
  <code>echo</code> will just print out the exact same thing you typed in. But <code>></code> redirect it to <code>fileX</code>.
</details>
<br/>

Make a directory called `Knowledge` and make two subdirectories in `Knowledge` called `Facts` and `Believes`.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>mkdir Knowledge  
mkdir Knowledge/Facts  
mkdir Knowledge/Believes  </pre>
</details>
<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  You can make all directories at once!
  <pre>mkdir -p Knowledge/Facts Knowledge/Believes  </pre>
  <code>-p</code> is "recursive" this way you can create the parent and child directories at the same time.
</details>
<br/>

ConCATenate `fileY` and `fileZ` and append them to the end of `fileX`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cat fileX fileY fileZ > temp  
mv temp fileX   </pre>
  You can't simply run 
  <pre>cat fileX fileY fileZ > fileX  </pre>
  It is because the fileX is opened as a writing file already and cannot be read. And this solution is not elegant, so check <code>Click to learn more!</code>.
</details>
<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  You can use <code>>></code> to append things to a file, super useful!
  <pre>cat fileY fileZ >> fileX  </pre>
</details>
<br/>

CoPy `fileX` into `Knowledge/Facts` and rename it into `math`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cp fileX Knowledge/Facts  
mv Knowledge/Facts/fileX Knowledge/Facts/Math  </pre>
  OR
  <pre>cp fileX Knowledge/Facts/Math  </pre>
</details>
<br/>

CoPy `Knowledge/Facts/Math` into current directory without renaming
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cp fileX Knowledge/Facts/Math .  </pre>
</details>
<br/>

Make `they're definitely correct` to the end of `fileX` without using `nano`.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>echo "they're definitely correct" >> fileX  </pre>
  Notice the apostrophe will open a quote, so we need to use the double quotes to suppress it.
</details>
<br/>

ReMove `Knowledge/Facts/math`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>rm Knowledge/Facts/math  </pre>
  Note: this is dangerous, the files you <code>rm</code> are gone forever. You can't get it back from the recycle bin!
</details>
<br/>

ReMove `Knowledge`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>rm -r Knowledge  </pre>
</details>
<br/>

![band](../img/band.png)

<br/>

## "New" stuff!

### Compressions & Archives

In bioinformatics we often deal with large files, and so we need to compress the files. Also, there will be times you want to package a folder into an archive, so it's easier to move around. Here you'll learn about how to handle these files!
<br/>

#### Compression
The most common compression method is `gzip`. You might be quite familiar with `zip`, but that's mostly used in Windows.   
First, go to `LinuxIntro/NewStuff/CompArch`, make two file called `mouth` and `pants`, and try to compress them (You can add any content you want into the two files.)  
Since we are learning, let's get some help.

```
gzip -h
```

It opens a manual and tells you how to use this command:

```
gzip [-123456789acdfhklLNnqrtVv] [-S .suffix] [<file> [<file> ...]]
```

It is a little bit confusing, but what you need to know is anything start with a `-` means it's an option, and the manual tells you what they are below. You don't need the options right now, here we only need `file`, without brackets, greater and lesser signs.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>gzip mouth pants  </pre>
</details>
<br/>

After zipping it, list all files, what did you find?  

Now, let's unzip it with `gunzip`.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>gunzip *.gz  </pre>
  If you want to do this, you should make sure that there's no other gz files.
</details>
<br/>

What if we want to keep the original file when compressing??  
Go check the manual again to see what you can do!  
This time, we will use:

```
man gzip
```

This opens the detailed manual with `less`. You can scroll up and down with your mouse and press `q` to leave.

Now, let's complete the task!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>gzip -k mouth pants  </pre>
  OR
  <pre>gzip --keep mouth pants  </pre>
</details>


<details>
  <summary><b><u>Fun Fact</u></b></summary>

  Compressibility can be used to estimate the complexity and relatedness of genomes. <br/>
  See <a href="/ref/Chen2000.pdf">Chen et al. 2000</a>  

</details>
<br/>

#### Archive
We will use `tar` to archive.  
Let's make a folder called `stuffs` and put `mouth` and `pants` in it. We will archive `stuffs` into `stuffs.tar`  
Now, use `-h` again to get some help.

```
tar -h
```

You will see that tar is a lot more complicated, it can do a lot of things!  

```
First option must be a mode specifier:
  -c Create  -r Add/Replace  -t List  -u Update  -x Extract
```

Since we want to make a new archive, we want to focus on `Create`:

```
Create: tar -c [options] [<file> | <dir> | @<archive> | -C <dir> ]
```

As well as the common options:

```
Common Options:
  -b #  Use # 512-byte records per I/O block
  -f <filename>  Location of archive
  -v    Verbose
  -w    Interactive
```

And so this mean that we need `-c` to create and `-f` to indicate the name of the archive you want to create (Yes, I agree. `tar`'s manual isn't the best).  
People often use `-v` so they can track the progress, too.

With all the information, let's try to archive!
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tar -c -v -f stuffs.tar stuffs  </pre>
  You can also put the all three options together!
  <pre>tar -cvf stuffs.tar stuffs  </pre>
</details>
<br/>

List the files, what did you see?

Now, remove the `stuffs` folder, and extract the tar file.  
(Use `tar -h` or `man tar` for information!)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>rm -r stuffs  
tar -x -v -f stuffs.tar stuffs  </pre>
  OR
  <pre>rm -r stuffs  
tar -xvf stuffs.tar stuffs</pre>
</details>
<br/>

#### Archive + Compress
You can archive and compress at the same time with `tar`!  
We will archive and compress `stuff` into `stuff.tar.gz`

Same drill: use `man` or `-h` for help and figure out how to do it!  

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tar -czvf stuffs.tar.gz stuffs  </pre>
</details>
<br/>

Compare the file size between compressed and uncompressed archives.  
Remember how to do it?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls -lh stuffs.tar*  </pre>
</details>
<br/>

#### See contents in tar without unpacking
Sometimes an archive is so huge, say 200 GB. You know extracting it will crash your poor laptop, but you want to know what's inside. What should you do?

Let's look at `List` in the `tar` manual! You should be able to figure out how to do it.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls -lh stuffs.tar*  </pre>
</details>
<br/>

Now, extract `mouth` only (Same drill)

<details>
  <summary><b><u>Hint</u></b></summary>
  Remember that you need to provide the full path
  <pre>tar -xzf stuffs.tar stuffs/mouth  </pre>
</details>
<br/>

#### Read compressed files without extraction
You can actually read compressed files without extracting them into new files! But, why do we want to do that? Because we can directly feed it into other commands with pipes `|`, which saves disk space and computational time (We will talk about it later).

Let's run the followings and see what you got.
```
echo nonsense > temp.txt
gzip temp.txt
gzcat temp.txt.gz
```

### Head and Tail  
You know `head` already it spits out the first few lines of a file. It could be handy if you want to take a quick glance at a file.  
But do you know `head` can do more than that?  
For example, you can specify how many lines you want it to spit out.  
Same drill, go to `LinuxIntro/NewStuff/HeadTailAndWordCount` and try to read file see what's the first three lines of `HeadAndTails.txt`?

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>head -n 3 HeadAndTails.txt  </pre>
</details>
<br/>

On the other hand, when you are dealing error messages you may want to look at the last few lines of the file. Then, we can use `tail`.  
Now, let's try to find out the last two lines of `HeadAndTails.txt`. (The syntax is the same).

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tail -n 2 HeadAndTails.txt  </pre>
</details>
<br/>

Sometimes, you want to remove the first few lines. And you can use `tail` to do that!  
However, we don't have a good manual. So, let's google to get help and try to remove the first line using `tail`!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tail -n +2 Linux.markdown  </pre>
</details>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  <code>head</code> should be able to do similar things, too, but it depends on the version that you have: My laptop isn't capable of that :(.
</details>

<br/>

### Counting Characters, Words and Lines
Sometimes you need to count how many raw reads you got from a sequencing service, or you want to count mamy nucleotides there are in a gene. Then, we can use `wc`.  
Stay in `LinuxIntro/NewStuff/HeadTailAndWordCount` and run 
```
wc HeadsAndTails.txt
```
You can see that there are four columns, the first three are numeric the last one is your file name.  
But what does each number mean? Try to find it out yourself!

You can also use options to specify which number you want to see. Look at manual and play with the four options!

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  You may notice <code>-m</code> and <code>-c</code> are nearly the same. That's because <code>-m</code> is character <code>-c</code> is bytes and normally one character is one byte. But when we use certain coding systems, some characters require two bytes to store, which makes the difference.
</details>
<br/>

Note: It's also not that simple to count nucleotides, but this is a starting point.
<br/>

### Pipes `|`
Pipes `|` are one of the most powerful tool in Linux in my opinion.  

Before we learn about pipe, let's revisit `wc` and `ls`. Go to `LinuxIntro/NewStuff/pipe` and figure out a way to count files in the folder!  

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls -l > listoffiles  
wc -l listoffiles  </pre><br/>
  That gives you 8 files, but there should be 7 only. 
</details>
<br/>

If you did not use `|`, you might get one more file counted due to the temporary file. To avoid this, we can simply not make the temporary file with `|`. Run:

```
ls -l | wc -l
```
What `|` is doing here is storing the "standard output" (STDOUT) from `ls` into memory and directly feed it as "standard input" (STDIN) to the next step. So, not only it saves space, it also saves a lot of time!  

Let's use `|` again to get the 3rd to 8th lines of `BadGuy`!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>head -n 8 BadGuy | tail -n 5  </pre><br/>
  Need some calculations!
</details>
<br/>

### Same and Different
#### Diff
Say today your lab is sharing a dataset and you made some edits, but you forgot what they are exactly. We can use `diff` to solve this issue.  
Head to `LinuxIntro/NewStuff/DiffSort` and compare `AfricanCountriesA` and `AfricanCountriesB`

```
diff AfricanCountriesA AfricanCountriesB
```

Try to figure out what the results mean!  
Note: This is a very simple dataset so you can infer what the command is doing by looking at the dataset. Now, what if you have larger datasets and you want to know what the command is doing without Googling or asking? (It's a useful skill!)
<br/>

#### Comm
`diff` can tell you where there's a difference, but sometimes you want to know what's the same. To do so, we can use `comm`. Let's run the following and see what happens.

```
comm AfricanCountriesA AfricanCountriesB
```

What are the three columns?

We can use the options to suppress certain columns. Play with the three options `-1`, `-2` and `-3`.  
You can also combine the options into `-12`, `-13` and `-23`. 
And so, back to the original problem, how to get the lines common to both `AfricanCountriesA` and `AfricanCountriesB`?  

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>comm -12 AfricanCountriesA AfricanCountriesB  </pre>
</details>
<br/>


### Sort and Unique
#### Sort
`sort` can be useful to organize things. Let's sort `AfricanCountriesA` with 
```
sort AfricanCountriesA
```
How are the countries sorted?

Now, let's sort `numbers`. How are the numbers sorted?  
Try to figure out how to sort it numerically! 

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sort -n numbers  </pre>
</details>
<br/>

#### Unique
`uniq` can be used to remove duplicated items and is often used with `sort`. Why? Run:

```
uniq numbers
```

You'll see that it only removes a `23`. That is because it only compares the two lines next to each other. So `sort` can solve this issue! Try again!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sort -n numbers | uniq  </pre>
</details>

<br/>

### Basic grep and sed
#### grep
`grep` is a tool that you can use to search a pattern in files. There are many uses, but we are going to learn the basic ones first.  
First let's find anything with `Africa` in `AfricanCountriesA`.

```
grep Africa AfricanCountriesA
```

You should see two countries. Now, let's do the inverse: find everything without `Africa`. (Check `-v` in the manual.)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>grep -v Africa AfricanCountriesA  </pre>
</details>

<br/>

We can also count how many hits without `Africa` we got. (There are multiple ways.)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>grep -cv Africa AfricanCountriesA  </pre>
  OR
  <pre>grep -v Africa AfricanCountriesA | wc -l  </pre>
</details>

<br/>

Lastly, check out `-o`. What does it do? And let's search for "c".

```
grep -o c AfricanCountriesA
```

It just print out a bunch of "c". Seems useless right? But there's actually some uses for it. Check the manual and discuss what use there might be!
<details>
  <summary><b><u>Hint</u></b></summary>
  It print out all exact hits. (And multiple times within a line). <br/>
  You can pipe it to <code>wc -l</code> and get a count of the hits!
  <pre>grep -o c AfricanCountriesA | wc -l  </pre>
  There are more uses for it and you'll find it out when you learn about advanced <code>grep</code>! 
</details>

<br/>

#### sed
`sed` is another command with a whole lot of uses. However, it's syntax is quite strange, so practicing it would help you master this useful command. We're covering two most common ones: substitute and delete. 

We'll start with "delete". Let's open `sed` manual with `man` and look at synopsis.
```
sed [-Ealnru] command [-I extension] [-i extension] [file ...]
```
Here we need `command` and `file`. File is simple, but what should `command` be? We can scroll down to `Sed Functions`.  
You will see there's a whole bunch of functions you can use, but to substitute a line, we need `d`. Scroll down and you should see a section start with this:
```
[2addr]d
```

`[2addr]` means that you can provide two addresses where you want the command to act on. The manual do provide information on how to use it but I'll just let you know two common cases.

The first one is a number (or multiple number splitting by `,`). It specifies which `line` the command will take place. Try to remove the third and fifth lines from `AfricanCountriesA`.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed '3,5d' AfricanCountriesA  </pre>
  It's a good practice to add <code>'</code> for sed command because there often are weird characters that bash may interpret differently.
</details>
<br/>

The second one is a query (like `grep`), but you need one `/` on the two sides of the query. And it will remove the lines that match.  
Try to remove lines with `Africa` from `AfricanCountriesA`.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed '/Africa/d' AfricanCountriesA  </pre>
  Remember how to do the same thing with <code>grep</code>?
</details>
<br/>

Now, let's move on to "substitute".  
When we look at the manual, we'll see:
```
[2addr]s/regular expression/replacement/flags
```
Basically the `regular expression` is your query. And you can replace the query with `replacement`. `[2addr]` usage is like its usage in `d`, which we can leave blank here (so that it will do the command on every line). `flags` are some additional options for the command. Let's leave it blank now.
And so, try to replace `a` with `x`

```
sed 's/a/x/' AfricanCountriesA
```

What did you find?  
It doesn't seem to replace every `a` right? Look at the flags and find one that allows you to replace every `a`.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed 's/a/x/g' AfricanCountriesA  </pre>
  "g" stands for global! (I think.)
</details>
<br/>

You can also replace multiple characters and special characters. Howabout replacing "an" with "@$!"? 
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed 's/an/@$!/g' AfricanCountriesA  </pre>
</details>
<br/>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  Sometimes you may want to replace <code>/</code> with something else, but <code>/</code> is used already! <br/>
  If this is the case, you can use other characters except for <code>\</code> to replace <code>/</code>! E.g.
  <pre>sed 's@/@X@g' yourfile  </pre>
</details>
<br/>

Both `grep` and `sed` also allow super-useful fuzzy matching with regular expressions. We will explore them tomorrow!

<br/>

![band](../img/band.png)

<br/>

## Good practice and miscellaneous things you should know

### Paths and Variables
Variables are useful when you need to run same codes with different arguments. Let's say we want to run `cat` and `echo` multiple times. We can use a variable, let's say `file`, and also assign a value `AfricanCountriesA` to `file`. 

```
file=AfricanCountriesA
cat $file
echo $file
```

We first use `=` to assign the variable. Then, we call the variable with `$`. This way, we will be able to see the contents of `AfricanCountriesA` and the file name itself.  
We can further assign different values to `file`. Such as,

```
file=AfricanCountriesB
cat $file
echo $file
```

You can also combine the variables with other strings to create new strings. They will just glue together. For example,

```
char=B
cat AfricanCountries$char
```

It might not seem very useful right now, but if you have complicated codes. You only need to save the codes once instead of multiple times if you use variables. We will also talk about other uses soon (tomorrow!)

<br/>

### Tabs Tabs Tabs!
OK I should have said this before, but if you're stuck, just press `tab`!

Some more details: A normal UNIX syntax is start with a command and add options, arguments etc. If you press `tab` when you are at the command part, it will search in your `PATH` (a special environmental variable that's already defined) and try to find one that fits to fill in. If you press `tab` when you at the options/arguments part it will search in your present working directory and try to find a file (including directories) that fits to fill in.  
If there are more than two hits, it won't give you anything. But then, you can press `tab` another time and it will give you a list of hits.

<br/>

### Don't use Word to store your codes
Word messes up everything! To prove it, try to TYPE in the followings and paste in terminal to run it.

```
echo "stupid" > MicrosoftWord
```

What did you find?  

OK so it's not Word is stupid but it's too smart that it automatically changes some of the characters for the writers. However, it's not good for Bioinformatics.  
So, I suggest you use a text editor or [Visual Studio Code](https://code.visualstudio.com/) to store your codes.  
(Visual Studio Code is quite useful. It understands some computer languages and will highlight things to help you read your codes.)
<br/>

### Space Oddity
Do you know how to read a file `Coinvasion workshop.txt` with `cat`?
The space between `Coinvasion` and `workshop` make your system thinks they are two different files!

No worries, there's a solution. Just add `\` before the space like this:
```
cat Coinvasion\ workshop.txt
```
`\`, the "back slash", is a special character that can suppress other special characters' function (or will give a character a function). We will explore it later. (the next section has some examples, too.)  

My recommendation is to avoid spaces in your file naming system (you probably already know that). Alternatives include using upper cases, hyphens, underscores... Such as,

```
CoinvasionWorkshop.txt
Coinvasion-workshop.txt
Coinvasion_workshop.txt
```

<br/>

### New Line and Carriage Return
Sometimes codes behaves weirdly, why are txt files sometimes have blank lines when loaded into R? This is especially common when you save an Excel file into a txt file.  
So, a new line is actually a character `\n` in Linux (and Unix) (and a tab is `\t`). However, in Windows it's `\r\n`, older MacOS use `\r`. And Office Excel follow the Windows coding system.  

<details>
  <summary><b><u>Fun Fact</u></b></summary>
  Here, <code>\n</code> means New line and <code>\r</code> means carriage Return and it's because in type writer world you need to first return the carriage <code>\r</code> and make a line break <code>\n</code>.
</details>
<br/>

Do you know how to remove `\r`? (Remember `sed`?)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed 's/\r//g' file  </pre>
</details>
<br/>

![band](../img/band.png)

<br/>


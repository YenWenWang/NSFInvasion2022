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

Change Directory to `DennyMaterials/LinuxIntro/Review`.
<details>
  <summary><b><u>Hint</u></b></summary>
  You can use either absolute path or relative path.
  <pre>cd DennyMaterials/LinuxIntro/Review  </pre>
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
First, go to directory `LinuxIntro/Review/FileExploration`. (I'm not writing out `DennyMaterials` from now on.)  
Then, LiSt the files.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls  </pre>
</details>
<br/>

When is `file1` created and which is the largest file?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls -lh  </pre>
  <code>-l</code> is an option, providing the details of the files and <code>-h</code> is a second option, providing human-readable file size etc. <br/>
  We merged the two options together into <code>-lh</code> (This only works with single character options.)
</details>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  You can sort the files by time or size!
  <pre>ls -lht  
ls -lhS  </pre>
</details>
<br/>

You might find that some of the "files" are directories. But how to tell which one is which?  
Look at the first column of your `ls -l` results. If it starts with a `d`, it's a directory!  
Other options include using tab completion (my personal go to), or `ls -p`, if there's a `/` after the name, that's a directory.

Now, what's in `directory"X"`, where "X" can be anything?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls directory*  </pre>
  <code>*</code> is one of the wildcards, it can be anything at any length! However, the syntax is not the same in every situation. We will explore other usage of wildcards later!
</details>
<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  Check Hint about wildcards!
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
  <code>-p</code> is "recursive". This way you can create the parent and child directories at the same time.
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

ReMove `Knowledge/Facts/Math`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>rm Knowledge/Facts/Math  </pre>
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
Usage: gzip [OPTION]... [FILE]...
```

Right now, we don't need `[OPTION]` (usually it's like `-x` or `--xxx` and the manual tells you what they are below.) So, here we only need to replace `[FILE]` with file names.

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

This opens the detailed manual with `less`. You can scroll up and down with your mouse and press `q` to leave. (Check out `Advanced usage`.)

Now, let's complete the task!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>gzip -c mouth > mouth.gzip  
gzip -c pants > pants.gzip</pre>
Check out <code>-c</code> in <code>OPTIONS</code> as well.
</details>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  In different version of <code>gzip</code> you can use <code>-k</code> or <code>--keep</code>. Unfortunately, it's not available here.
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
Now, use `--help` to get some help. (`--help` normally is `-h` but some programs use one or another.)

```
tar --help
```

You will see that `tar` is a lot more complicated, it can do a lot of things! Check out the `Examples` in the beginning!

With all the information, let's try to archive!
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tar -cf stuffs.tar stuffs  </pre>
</details>
<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  As mentioned before, <code>-cf</code> is the same as <code>-c -f</code>, usually you can stack these one-character options together.
  <br/><br/>
  People often use <code>-v</code> to the process verbose. It will tell you which file it is archiving. Could be a good practice!
  <pre>tar -cvf stuffs.tar stuffs  </pre>
</details>
<br/>

List the files, what did you see?

Now, remove the `stuffs` folder, and extract the tar file.  
(Use `tar --help` or `man tar` for information!)

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

Same drill: use `man` or `--help` for help and figure out how to do it! (check out `Compression options`)  

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

Let's look at `Examples` in `tar` manual again!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls -lh stuffs.tar*  </pre>
</details>
<br/>

Now, we want to extract `mouth` only. Because it's hard to find the information in manual, why don't you Google for information? (No, Googling is not cheating! Also, discuss how to Google rather than how to write the codes.) 

<details>
  <summary><b><u>Hint</u></b></summary>
  Remember that you need to provide the full path
  <pre>tar -xzf stuffs.tar.gz stuffs/mouth  </pre>
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
Same drill, go to `LinuxIntro/NewStuff/HeadTailAndWordCount` and try to read file see what's the first three lines of `HeadsAndTails.txt`?

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>head -n 3 HeadsAndTails.txt  </pre>
</details>
<br/>

On the other hand, when you are dealing error messages you may want to look at the last few lines of the file. Then, we can use `tail`.  
Now, let's try to find out the last two lines of `HeadsAndTails.txt`. (The syntax is the same).

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tail -n 2 HeadsAndTails.txt  </pre>
</details>
<br/>

Sometimes, you want to remove the first few lines. And you can use `tail` to do that! (You can use manual or try to Google it!)  

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

Note: It's also not that simple to count nucleotides, but this could be a starting point.
<br/>

### Pipes `|`
Pipe `|` is one of the most powerful tool in Linux in my opinion.  

Before we learn about pipe, let's revisit `wc` and `ls`. Go to `LinuxIntro/NewStuff/pipe` and figure out a way to count files in the folder! (You will need to direct output from `ls` to a file and use `wc` on it.)  

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls -l > listoffiles  
wc -l listoffiles  </pre><br/>
  That gives you 8 files, but there should be 7 only. 
</details>
<br/>

Since we did not use `|`, we will get one more file counted due to the temporary file. To avoid this, we can simply not make the temporary file with `|`. Run:

```
ls -l | wc -l
```

What `|` is doing here is storing the "standard output" (STDOUT) from `ls` into memory and directly feed it as "standard input" (STDIN) to the next step. So, not only it makes your script shorter, it also saves a lot of computational time!  

Let's use `|` again to get the 3rd to 8th lines of `BadGuy`! (Think about which commands we used to get specific lines of a file.)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>head -n 8 BadGuy | tail -n 5  </pre><br/>
  Need to do some calculations!
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

We can use the options to suppress certain columns. Play with the three options `-1`, `-2` and `-3` and try to figure out what's going on. 
You can also combine the options into `-12`, `-13` and `-23`.  
Back to the original problem, how to get the lines common to both `AfricanCountriesA` and `AfricanCountriesB`?  

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
Try to figure out how to `sort` it numerically! (Note that `sort -h` sort of "freeze" your terminal. It's because of weird functionality of sort. Don't worry and use `--help` or `man` instead.)

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

You'll see that it only removes a `23` but not the duplicated `2`. That is because it only compares the two lines next to each other. So `sort` can solve this issue! Try again!

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
</details>

<br/>

#### sed
`sed` is another command with a whole lot of uses. However, it's syntax is quite strange, so practicing it would help you master this useful command. We're covering two most common ones: substitute and delete lines. 

We'll start with "delete lines". We will start with deleting certain positions of lines. Again, `sed` manual is not the best. So let's Google to see how to delete the third to fifth lines from `AfricanCountriesA`.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed '3,5d' AfricanCountriesA  </pre>
</details>

<details>
  <summary><b><u>Click to learn more</u></b></summary>
  It's a good practice to add <code>'</code> in <code>sed</code> command:
  <pre>sed '3,5d' AfricanCountriesA  </pre>
  It's because there often are weird characters that shell may interpret differently. <code>'</code> will suppress those interpretations.
</details>
<br/>

We can also remove lines with a pattern. Same drill, Google again and try to remove lines with `Africa` from `AfricanCountriesA`.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed '/Africa/d' AfricanCountriesA  </pre>
  Remember how to do the same thing with <code>grep</code>?
</details>

<details>
  <summary><b><u>Click to learn more</u></b></summary>
  The idea of all these craziness is that <code>d</code> means delete and anything matches what's before will be deleted. If it's number, it will delete the lines at those position (3,5 means 3~5). If it's things like <code>/XXX/</code>, it's doing a <code>grep</code> like searching.
</details>
<br/>

Now, let's move on to "substitute". I'll help you with this. Instead of `d`, we will use `s`.

```
sed 's/a/x/' AfricanCountriesA
```

It should replace the things between the first `/` pair (`a`) with the things between the second `/` pair `x`. But, what did you find?  

It only replaces the first `a`s in a line right?  
We can add `g` at the end of the `sed` command for globally replacement 

```
sed 's/a/x/g' AfricanCountriesA 
```

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

It might look like that `s` and `d` have completely different syntax, but there's actually a rationale behind. We won't touch on it in this workshop, but you are welcome to discuss with others or me.

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
(Visual Studio Code is quite useful. It understands some computer languages and will highlight things to help you read your codes. We will explore it together.)
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

Do you know how to remove `\r`? (Just think about it and press Hint.)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed 's/\r//g' file  </pre>
</details>
<br/>


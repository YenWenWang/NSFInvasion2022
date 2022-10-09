---
layout: page
permalink: /Linux/Intro
title: "Intro to Linux"
---

## What are we going to learn?

Please press hint if only necessary  

<br/>

![band](../img/band.png)

<br/>

## Review
Should be simple if you have done the exercises before

### Directory Navigation

What's the Present Working Directory? (i.e. which directory are you in?)
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>pwd  </pre>
</details>
<br/>

Change Directory to `Intro/Review`.
<details>
  <summary><b><u>Hint</u></b></summary>
  You can use either absolute path or relative path.
  <pre>cd XXXXXXXXX  </pre>
  OR
  <pre>cd YYYYYYYYY  </pre>
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
First, go to directory `Intro/Review/FileExploration`.  
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

What's in `directoryNovels/TheDoomsDay`?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cat directoryNovels/TheDoomsDay  </pre>
  OR
  <pre>less directoryNovels/TheDoomsday  </pre>
  To leave <code>less</code> press q.<br/>
  There are a lot more choices!
</details>
<br/>

### Super Basic File and Directory Handling
Go to directory `Intro/Review/FileDirHandle`.  
Make a file named `fileX` with `1+1=3` as its content.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>nano fileX  
# type in 1+1=3  
# control C  
# click Y  </pre>
  OR 
  <pre>echo 1+1=3 > fileX  </pre>
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

## New stuff!

### Compressions & Archives

In bioinformatics we often deal with large files, and so we need to compress the files. Also, there will be times you want to package a folder into an archive, so it's easier to move around. Here you'll learn about how to handle these files!
<br/>

#### Compression
The most common compression method is `gzip`. You might be quite familiar with `zip`, but that's mostly used in Windows.   
First, go to `Intro/NewStuff/CompArch`, make two file called `mouth` and `pants`, and try to compress them (You can add any content you want into the two files.)  
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

Let's unzip it with `gunzip` first.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>gunzip *.gz  </pre>
  If you want to do this, you should make sure that there's no other gz files.
</details>
<br/>

What if we want to keep the original file when compressing??  
Go check the manual again to see what you can do!

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
  You can also put the three options altogether!
  <pre>tar -cvf stuffs.tar stuffs  </pre>
</details>
<br/>

List the files, what did you see?

Now, remove the `stuffs` folder, and extract the tar file.  
(Use `-h` for information!)

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

Same drill: use `-h` for help and figure out how to do it!  
(You don't need the patterns)
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

Let's just run the followings
```
echo nonsense > temp.txt
gzip temp.txt
gzcat temp.txt.gz
```

### Head and Tail  
You know `head` already it spits out the first few lines of a file. It could be handy if you want to take a quick glance at a file.  
But do you know `head` can do more than that?  
For example, you can specify how many lines you want it to spit out.  
Let's get some help first. 

```
head -h
```

Uh oh, `head` doesn't have `-h` option. But it still tells you how to use the command!  
Why don't we go to `Intro/NewStuff/HeadTailAndWordCount` and try to read file see what's the first three lines of `HeadAndTails.txt`?

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
<br/>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  <code>head</code> should be able to do similar things, too, but it depends on the version that you have: My laptop isn't capable of that :(.
</details>

<br/>

### Counting Characters, Words and Lines
Sometimes you need to count how many nucleotides there are in a gene, or you want to count how many files there are in a directory.  
Stay in `Intro/NewStuff/HeadTailAndWordCount` and run 
```
wc HeadsAndTails.txt
```
You can see that there are four columns, the first three are numeric the last one is your file name.  
But what does each number mean? Try to find it out yourself!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tail -n +2 Linux.markdown  </pre>
</details>
<br/>

You can also use options to specify which number you want to see. Use `-h` to invoke "manual", and play with the four options!

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  You may notice <code>-m</code> and <code>-c</code> are nearly the same. That's because <code>-m</code> is character <code>-c</code> is bytes and normally one character is one byte. But when we use certain coding systems, some characters require two bytes to store, which makes the difference.
</details>

Now, let's do something else. Try to use `wc` to count the files! (remember `ls`?)  

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>ls -l > listoffiles  
wc -l listoffiles  </pre><br/>
  That gives you 2 files, but there should be one only. You can find out why by running <code>ls</code> again. To avoid this, we can simply not make the file <code>listoffiles</code>. We will talk about how to do it later!
</details>
<br/>

Note: It's also not that simple to count nucleotides, but this is a starting point.

<br/>

### Same and Different
#### Diff
Say today your lab is sharing a dataset and you made some edits, but you forgot what they are exactly. We can use `diff` to solve this issue.  
Head to `Intro/NewStuff/DiffComm` and compare `AfricanCountriesA` and `AfricanCountriesB`

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

![band](../img/band.png)
<br/>

## Good practice and micellaneous things you should know

### Don't use Word to store your codes
Word messes up everything! To prove it, try TYPE in the following and paste in terminal to run it.

```
echo "stupid" > MicrosoftWord
```

What did you find?  

OK so it's not Word is stupid but it's too smart that it automatically changes some of the characters for the writers. However, it's not good for Bioinformatics.  
So, I suggest you use a text editor or [Visual Studio Code](https://code.visualstudio.com/) to store your codes.  
(Visual Studio Code is quite useful. It understand some computer languages and will highlight things to help you read your codes.)

<br/>

### Space Oddity
Do you know how to read a file `Coinvasion workshop.txt` with cat?
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

### New line and Carriage Return
Sometimes codes behaves weirdly, why are txt files sometimes have blank lines when loaded into R? This is especially common when you save an Excel file into a txt file.  
So, a new line is actually a character `\n` in Linux (and Unix) (and a tab is `\t`). However, in Windows it's `\r\n`, older MacOS use `\r`. And Office Excel follow the Windows coding system.  

<details>
  <summary><b><u>Fun Fact</u></b></summary>
  Here, <code>\n</code> means New line and <code>\r</code> means carriage Return and it's because in type writer world you need to first return the carriage <code>\r</code> and make a line break <code>\n</code>.
</details>

You can run something like below to remove `\r` (but it would not work for old MacOS)

```
sed 's/\r//g'
```

We will learn about `sed` more later!

<br/>

## Also see

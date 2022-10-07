---
layout: page
permalink: /Linux/Intro
title: "Intro to Linux"
---

## What are we going to learn?

Please press hint if only necessary
![band](/img/band.png)
<br/>

## Review
Should be simple if you have done the exercises before

### Directory Navigation

What's the Present Working Directory? (i.e. which directory are you in?)
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    pwd
  </pre>
</details>
<br/>

Change Directory to `XXXXXXXXXX`.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cd XXXXXXXXX
  </pre>
  OR
  <pre>
    cd YYYYYYYYY
  </pre>
</details>
<br/>

Go to the parent directory.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cd ..
  </pre>
</details>
<br/>

Go to back to the directory you were in (`XXX`).
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cd -
  </pre>
</details>

<details>
  <summary><b><u>Click here to learn more!</u></b></summary>

  You can use `cd -` to hop back and forth between two directories.
</details>
<br/>

Go to the home directory.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cd
  </pre>
  OR
  <pre>
    cd .  
  </pre>
</details>
<br/>

### File Exploration
First, go to directory `XXXXX`.  
Then, LiSt the files.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    ls
  </pre>
</details>
<br/>

Which is the oldest file and which is the largest file?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    ls -lh
  </pre>
</details>

<details>
  <summary><b><u>Click here to learn more!</u></b></summary>
  You can sort the files by time and size!
  <pre>
    ls -lht 
    ls -lhS
  </pre>
</details>
<br/>

What's in `directory"X"`, where X can be anything?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    ls directory*
  </pre>
  * is one of the wildcards, it can be anything at any length! However, the syntax is not the same in every situation. We will explore other usage of wildcards later!
</details>
<br/>

What's in `directoryA/fileA`?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cat directoryA/fileA 
  </pre>
  OR
  <pre>
    less directoryA/fileA
  </pre>
  There are a lot more choices!
</details>
<br/>

### Super Basic File and Directory Handling

Make a file named `fileX` with `1+1=3` as its content.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>  
    nano fileX 
    # type in 1+1=3
    # control C
    # click Y
  </pre>
  OR 
  <pre>
    echo 1+1=3 > fileX  
  </pre>
</details>
<br/>

Make a directory called `Knowledge` and make two subdirectories in `Knowledge` called `Facts` and `Believes`.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    mkdir Truth
    mkdir Knowledge/Facts
    mkdir Knowledge/Believes
  </pre>
</details>
<details>
  <summary><b><u>Click here to learn more!</u></b></summary>
  You can make all directories at once!
  <pre>
    mkdir -p Knowledge/Facts Knowledge/Believes
  </pre>
  -p is "recursive" this way you can create the parent and child directories at the same time.
</details>
<br/>

ConCATenate `fileY` and `fileZ` and append them to the end of `fileX`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cat fileX fileY fileZ > fileX
  </pre>
</details>
<details>
  <summary><b><u>Click here to learn more!</u></b></summary>

  You can use `>>` to append things to a file, super useful!
  <pre>
    cat fileY fileZ >> fileX
  </pre>
</details>
<br/>

CoPy `fileX` into `Knowledge/Facts` and rename it into `math`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cp fileX Knowledge/Facts
    mv Knowledge/Facts/fileX Knowledge/Facts/Math
  </pre>
  OR
  <pre>
    cp fileX Knowledge/Facts/Math
  </pre>
</details>
<br/>

Make `they're definitely correct` to the end of `fileX` without using `nano`.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    echo "they're definitely correct" >> fileX
  </pre>
  Notice the apostrophe will open a quote, so we need to use the double quotes to suppress it.
</details>
<br/>

ReMove `Knowledge/Facts/math`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    rm Knowledge/Facts/math
  </pre>
</details>
<br/>

ReMove `Knowledge`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    rm -r Knowledge
  </pre>
</details>

![band](/img/band.png)
<br/>

## New stuff!

### Compressions & Archives
In bioinformatics we often deal with large files, and so we need to compress the files. Also, there will be times you want to package a folder into an archive, so it's easier to move around. Here you'll learn about how to handle these files!
<br/>

#### Compression
The most common compression method is `gzip`. You might be quite familiar with `zip`, but that's mostly used in Windows.   
First, make two file called `mouth` and `pants`, and try to compress them (You can add any content you want into the two files.)  
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
  <pre>
    gzip mouth pants
  </pre>
</details>

After zipping it, list all files, what did you find?  

Let's unzip it with `gunzip` first.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    gunzip stuff.zip
  </pre>
</details>

What if we want to keep the original file?  
Go check the manual again to see what you can do!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    gzip -k mouth pants
  </pre>
  OR
  <pre>
    gzip --keep mouth pants
  </pre>
</details>


<details>
  <summary><b><u>Fun Fact</u></b></summary>

  Compressibility can be used to estimate the complexity and relatedness of genomes.  
  See [Chen et al. 2000](/ref/Chen2000.pdf)
</details>
<br/>

#### Archive
We will use `tar` to arcive.  
Let's make a folder called `stuffs` and put `mouth` and `pants` in it. We will arcive `stuffs` into `stuffs.tar`  
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
  <pre>
  tar -c -v -f stuffs.tar stuffs
  </pre>
  You can also put the three options altogether!
  <pre>
  tar -cvf stuffs.tar stuffs
  </pre>
</details>
<br/>

List the files, what did you see?

Now, remove the `stuffs` folder, and extract the tar file.  
(Use `-h` for information!)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
  rm -r stuffs
  tar -x -v -f stuffs.tar stuffs
  </pre>
  OR
  <pre>
  rm -r stuffs
  tar -xvf stuffs.tar stuffs
  </pre>
</details>
<br/>

#### Archive + Compress
You can archive and compress at the same time with `tar`!  
We will archive and compress `stuff` into `stuff.tar.gz`

Same drill: use `-h` for help and figure out how to do it!  
(You don't need the patterns)
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
  tar -czvf stuffs.tar.gz stuffs
  </pre>
</details>

Compare the file size between compressed and uncompressed archives.  
Remember how to do it?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
  ls -lh stuffs.tar*
  </pre>
</details>
<br/>

#### See contents in tar without unpacking
Sometimes an archive is so huge, say 200 GB. You know extracting it will crash your poor laptop, but you want to know what's inside. What should you do?

Let's look at `List` in the `tar` manual! You should be able to figure out how to do it.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
  ls -lh stuffs.tar*
  </pre>
</details>

Now, extract `mouth` only (Same drill)

<details>
  <summary><b><u>Hint</u></b></summary>
  Remember that you need to provide the full path
  <pre>
  tar -xzf stuffs.tar stuffs/mouth
  </pre>
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

### head and tail

![band](/img/band.png)
<br/>

## Good practice and micellaneous things you should know

### Don't use Word to store your codes

### New line and Carriage Return?
Sometimes codes behaves weirdly, why are txt files sometimes have blank lines when loaded into R?  
So, a new line is actually a character `\n` in Linux (and Unix) (and a tab is `\t`). However, in Windows it's `\r\n`, older MacOS use `\r`.

<details>
  <summary><b><u>Fun Fact</u></b></summary>

  Here, `\n` means New line and `\r` means carriage Return and it's because in type writer world you need to first return the carriage `\r` and make a line break `\n`.
</details>

You can run something like below to remove `\r` (but it would not work for old MacOS)

```
sed 's/\r//g'
```

We will learn about `sed` more later!

## Also see

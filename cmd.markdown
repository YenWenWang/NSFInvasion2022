---
layout: page
permalink: /cmd
title: "Unix/Linux course"
---

## What are we going to learn?

Please press hint if only necessary
<br/>

## Review
Should be simple if you have done the exercises before

### 1. Directory Navigation

#### What's the Present Working Directory? (i.e. which directory are you in?)
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    pwd
  </pre>
</details>
<br/>

#### Change Directory to `XXXXXXXXXX`.
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

#### Go to the parent directory.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cd ..
  </pre>
</details>
<br/>

#### Go to back to the directory you were in (`XXX`).
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cd -
  </pre>
</details>

<details>
  <summary><b><u>Click here to learn more!</u></b></summary>
  <pre>
    cd -
  </pre>
  You can use this code to hop back and forth between two directories.
</details>
<br/>

#### Go to the home directory.
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

### 2. File Exploration
#### First, go to directory `XXXXX`.  
#### LiSt the files.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    ls
  </pre>
</details>
<br/>

#### Which is the oldest file and which is the largest file?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    ls -lh
  </pre>
</details>

<details>
  <summary><b><u>Click here to learn more!</u></b></summary>
  <pre>
    ls -lht 
    ls -lhS
  </pre>
</details>
<br/>

#### What's in `directory"X"`, where X can be anything?
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    ls directory*
  </pre>
  * is one of the wildcards, it can be anything at any length! However, the syntax is not the same in every situation. We will explore other usage of wildcards later!
</details>
<br/>

#### What's in `directoryA/fileA`?
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

### 3. Super Basic File and Directory Handling

#### Make a file named `fileX` with `1+1=3` as its content.
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

#### Make a directory called `Knowledge` and make two subdirectories in `Knowledge` called `Facts` and `Believes`.
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

#### ConCATenate `fileY` and `fileZ` and append them to the end of `fileX`
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    cat fileX fileY fileZ > fileX
  </pre>
</details>
<details>
  <summary><b><u>Click here to learn more!</u></b></summary>
  <pre>
    cat fileY fileZ >> fileX
  </pre>
  >> can append things to a file, super useful!
</details>
<br/>

#### CoPy `fileX` into `Knowledge/Facts` and rename it into `math`
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

#### Make `they're definitely correct` to the end of `fileX` without using `nano`.
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>
    echo "they're definitely correct" >> fileX
  </pre>
  Notice the apostrophe will open a quote, so we need to use the double quotes to suppress it.
</details>
<br/>

#### ReMove `Knowledge/Facts/math`
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
<br/>

## Did I say that there's a treasure hunt?!

## Also see

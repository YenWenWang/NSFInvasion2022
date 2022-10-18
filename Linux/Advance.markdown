---
layout: page
permalink: /Linux/Advance
title: '"Advanced" Linux'
---

Notes:

Table related
cut: csv and tsv
more sort: -k 
awk

Crazy stuff:
Process substitution and command substitution


## Loops and ifs
### for
We are using BLAST to learn about loops. And we will be using your favorite genes. First, we will build multiple databases with `for` loops and blast each databases.  
Let's go to folder `LinuxAdvance/forloops` and copy three of your genome assemblies into the folder.

```
for f in *.fasta
do  makeblastdb -dbtype nucl $f
done
```

Let's see what's going on here. The first line uses a wild card and so it's basically `for f in A.fasta B.fasta C.fasta`. This will create a variable call `f`. `A.fasta` will be assigned to `f` for the first iteration, `B.fasta` will be the next, and so on and so forth.  
Move on to the next line. `do` states the things you are going to do for an iteration. And `$f` is calling the variable `f`. So, for the first iteration, we are running `makeblastdb -dbtype nucl A.fasta`. So on and so forth.
Note that you can have multiple lines after do and the for loop will run through all of them. For example: (Don't run)

```
for f in *.fasta
do  echo making database for $f
    makeblastdb -dbtype nucl $f
done
```

How about you try to run blast through all databases now? Copy the fasta with genes of interest into the folder and write a code to complete the task!

<details>
  <summary><b><u>Hint</u></b></summary>
  You can run something like this. (replace <code>blastn</code> with <code>tblastn</code> if you have a protein query.)
  <pre>for f in *.fasta  
do  blastn -db $f -query [&ltyourquery&gt] -outfmt 6 -out tblastn-$f.txt  
done</pre>
</details>
<br/>

Did you get an issue with your query fasta being treated as a database? There are at least three strategies to deal with it. The first one is to avoid `for` assigning it your variable `f`. For example, you can rename it, put it into a different folder or use some clever scheme in your wildcard to exclude the query.  
Or, you can use `if` (I'm still proposing using the former, since it will be cleaner).

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  <code>for</code> loops are also useful if you want to generate a series of number. Try the followings:  
  <pre>for n in {1..20}  
do  echo $n
done</pre>
</details>
<br/>

### if else
I'm not using `if` `else` a lot, but I think it's worth mentioning.
Using our former task as example, we want to avoid your query. Therefore we need a `if` clause saying "if `f` is query, skip it", or "if `f` is not query, do some stuff".  
Let's start with the second strategy with an example.

```
x=somestring
if [ $x != somestring ]
then echo $x is not somestring
fi
```

In this example, we first assign "somestring" to `x`. The second line ask if `x` is not somestring (`!=` is not equal). Now, the `[]` pass a true to if, so the if clause continue to run things from `then` to `fi`. You can try assign something else to `x` and see what happens.
Note: You need the space between `[` and `$x` and between `somestring` and `]`.  

Now, let's try the first strategy.

```
x=somestring
if [ $x == somestring ]
then echo
else echo $x is not somestring
fi
```

Here, there's an else clause to say "if the things in `[]` is false, in this case: `x` is somestring (`==` is equal), run some `echo $x is not somestring`.  
You can see the solution is not elegant. You still need to run something when `[]` is true (I just gave it an `echo`). So, avoid this solution, but `else` is useful when you want to run something dichotomous.

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  There's also <code>elif</code> so you can process multiple if else together. Go learn it yourself!
</details>
<br/>

Try to write a code with `for` and `if` to avoid using query fasta!
<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>for f in *.fasta  
do  if [ $f != [&ltyourquery&gt] ]  
    then blastn -db $f -query [&ltyourquery&gt] -outfmt 6 -out tblastn-$f.txt  
    fi  
done</pre>
</details>
<br/>

### while loops
The third strategy is to use `while` loops.  
The most common usage of `while` loop is to read a file and it will go through each line and assign them to variables.
Let's go to `LinuxAdvance/forloops`, take a look at `testfile` and run this:

```
while read l
do  echo $l is a letter
done < testfile
```


Could you figure out what's going on?

<details>
  <summary><b><u>Hint</u></b></summary>
  The first line saying while you are reading a line from a file, you assign it to <code>l</code> and do the things between <code>do</code> and <code>done</code>.  
  The last line uses <code>&lt</code> to indicate which file you are reading.
</details>
<br/>

Now, your turn, copy three of your genome assemblies and the fasta with genes of interest into the folder. Then, write a code to complete the task.
Note: use `nano` to create the files that you are reading with `while`.

<details>
  <summary><b><u>Hint</u></b></summary>
  It should be something like this:
  <pre>while read l
do makeblastdb -dbtype nucl $l
  blastn -db $l -query [&ltyourquery&gt] -outfmt 6 -out tblastn-$l.txt  
done &lt [&ltyourfastalist&gt] </pre>
Also see that I combined makeblastdb and blast so I don't need two loops! 
</details>
<br/>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  There's also <code>elif</code> so you can process multiple if else together. Go learn it yourself!
</details>
<br/>

## Advance sed and grep
### sed with variables
To make a combined database with multiple genomes, we technically only need to concatenate all the genome files and then use `makeblastdb`. However, it would be hard to know which contig or scaffold is from which sample. So, we are going back to `sed` to label these contigs/scaffolds. And although we do not necessarily need complicated coding to accomplish it, it's a good point to introduce you regular expressions. Just bear with me.

If we look at our assemblies, each sequence have a sequence name start with `>`. The easiest way to add sample information is to replace `>` with `>[<sample name>]`.  
Note that because you are using `''` in `sed` and that will suppress the meaning of `$` for calling variables, so you'll need to use `''` to address it. Basically, if you want to replace variable `X` with variable `Y`, you should code 

```
sed 's/'$X'/'$Y'/g' [<somefile>]
```

Now, you should have all the things you need to figure it out!  
Let's go to `LinuxAdvance/sedblast`, copy a few assembled genomes there and try it out! (Don't stop at making database but also do the blast part.)  

<details>
  <summary><b><u>Hint</u></b></summary>
  I'm skipping the <code>makeblastdb</code> and <code>blast</code>
  <pre>for f in *.fasta  
do  sed 's/>/>'$f'/g' $f > temp  
    mv temp $f
done  
cat *.fasta > compiled.fasta  </pre>
  You will get something that's sort of usable with this script.<br/>
  But it's ugly. you will have <code>.fasta</code> inside your sequences. What can you do? Well, just pipe it to another <code>sed</code> to remove it (and maybe replace it with something sensible!)
</details>
<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  You might find making a temporary file very inelegant. You can check out <code>-i</code>. I just never remember to use it :).
</details>
<br/>

Take a look at the blast results what did you find?

### sed with regular expression (Regex)

#### Beginning and end of a line.

Normally you won't have this problem, but what if there's an additional `>` in the middle of the sequence name? That will also add in the sample name that you don't need right?

So, we can use `^` to specify that `>` needs to be at the beginning. Like:

```
for f in *.fasta  
do  sed 's/^>/>'$f'/g' $f > temp  
    mv temp $f
done 
```

Sometimes you also want to add something to the end of a sequence. You can then use `$` to specify.
For example: (do not run)

```
sed 's/A$/B/g' 
```

This will replace every `A` at end of a line with `B`. 

I hope that you are interested in Regex now. And we will learn some other useful Regex!

#### Wildcards

Let's head to `LinuxAdvance/sedregex`, take a look at the file `ECMspecies` and learn about more Regex.  
First we will learn `.`. `.` means any single character. Let's see what happen if we run these two scripts:

```
sed 's/./XXX/' ECMspecies
sed 's/../XXX/' ECMspecies
```

Notice that I didn't add `g` at the end of the `sed` expression, so it will only replace the first match.

`*` is often used with `.`. What it does is matching the preceding element zero or more times (It's different from `bash`'s wildcard.) 

So what does this do?
```
sed 's/ .*/XXX/g' ECMspecies
```

Let's try to add `feminine` after genus names that end with `a`, add `masculine` after genus names that end with `us`. Also, remove the numbers and species. (Ignore `Tuber`)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed 's/a .*/a feminine/g' ECMspecies | sed 's/us .*/us masculine/g'  </pre>
</details>
<br/>

#### Bracket expressions

Although `.` is useful, we can't do more nuanced edits. For example, it can not do something like only editting `a` and `c` in the file. But, we can use bracket expressions `[]`.

How bracket expression works is that you place everything that you want to match inside the bracket. Such as,

```
sed 's/[ac]/XXX/' ECMspecies
```

Notice that, again, I did not use `g`. Take a look at the results. What happened?

We can also use `-` to replace a series of characters or numbers. For example, 

```
sed 's/[a-c]/XXX/' ECMspecies
sed 's/[0-3]/XXX/' ECMspecies
```

What just happened then? Look at the `Boletus` line. Found anything?

You can also specify the amount of times of these brackets need to appear with `\{\}`. Let's look at how it works without brackets first.

```
sed 's/l{2}/XXX/' ECMspecies
```

What does this do?

You can replace the `l` with brackets. Like,

```
sed 's/[ac]\{2\}/XXX/' ECMspecies
```

You can also specify a range of number of characters. Like:

```
sed 's/[lsu]\{1,\}/XXX/' ECMspecies
sed 's/[lsu]\{1,3\}/XXX/' ECMspecies
```

What does each of these do?

Now, you should know how to replace the numbers only. Let's try to replace them with `N`!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed 's/[0-9]\{1,\}/N/' ECMspecies  </pre>
</details>

<br/>

Lastly, you should also know that you can add `^` at the beginning of the brackets to indicate "not".
For example,

```
sed 's/[^0-9]/X/g' ECMspecies
```
What does it do?

<br/>

#### Marked subexpression

Now, let's say we want move the numbers to the beginning of the line, we can use marked subexpression `\(\)`. 

Run the followings:

```
echo ABCDEFGH | sed 's/^\(.*\)\(F\)/\2\1/'
```

What does it do? Let's ignore the `\(\)` first.  
`^` indicates the match needs to start from the beginning. After `.*` we find `F` and we replace them with `\2` and `\1`.  
`\1` and `\2` are defined by `\(\)`. `\1` corresponds to the first and `\2` correspond to the second.  

If it makes sense, try to move the numbers to the beginning of the line like this:

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed 's/\(.*\) \([0-9]\{1,\}\)/\2 \1/' ECMspecies  </pre>
</details>

<br/>

#### grep
`grep` also supports the usage of Regex. Are you able to find all the genera with species number equal or higher than 10 but lower than 100? (10~99)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>grep ' [0-9]\{2\} ' ECMspecies  </pre>
</details>

<br/>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  The Regex we used was POSIX basic regex. There's also a thing called POSIX extended basic regex. You can use <code>-E</code> to enable it. You don't need <code>\</code> for <code>{}</code> and <code>()</code> if you are using the extended version. And there are a few other functions that you can use. Learn more [here](https://en.wikipedia.org/wiki/Regular_expression)!
</details>

<br/>

![band](../img/band.png)

<br/>

## dealing with tables

cut

sort

awk!


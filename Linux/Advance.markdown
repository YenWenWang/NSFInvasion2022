---
layout: page
permalink: /Linux/Advance
title: '"Advanced" Linux'
---

![band](../img/band.png)

## Loops and Ifs
### for
We are using BLAST to learn about loops. And we will be using your favorite genes. First, we will build multiple databases with `for` loops and blast each databases.  
Let's go to folder `LinuxAdvance/forloops` and copy three of your genome assemblies into the folder.

```
for f in *.fasta
do  makeblastdb -dbtype nucl -in $f
done
```

Let's see what's going on here. The first line uses a wild card and so it's basically `for f in A.fasta B.fasta C.fasta`. This will create a variable called `f`. `A.fasta` will be assigned to `f` for the first iteration, `B.fasta` will be the next, and so on and so forth.  
Move on to the next line. `do` states the things you are going to do for an iteration. And `$f` is calling the variable `f`. So, for the first iteration, we are running `makeblastdb -dbtype nucl A.fasta`. So on and so forth.
Note that you can have multiple lines after do and the for loop will run through all of them. For example: (Don't run)

```
for f in *.fasta
do  echo making database for $f
    makeblastdb -dbtype nucl -in $f
done
```

How about you try to run blast through all databases now? Copy the fasta with genes of interest into the folder and write a code to complete the task!

<details>
  <summary><b><u>Hint</u></b></summary>
  You can run something like this. (replace <code>blastn</code> with <code>tblastn</code> if you have a protein query.)
  <pre>for f in *.fasta  
do  blastn -db $f -query [&lt;yourquery&gt;] -outfmt 6 -out blastn-$f.txt  
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
I don't not use `if` `else` a lot, but I think it's worth mentioning.  
Using our former task as example, we want to avoid your query. Therefore, we need a `if` clause saying "if `f` is query, skip it", or "if `f` is not query, do some stuff".  
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
do  if [ $f != [&lt;yourquery&gt;] ]  
    then blastn -db $f -query [&lt;yourquery&gt;] -outfmt 6 -out tblastn-$f.txt  
    fi  
done</pre>
</details>
<br/>

### while
The third strategy is to use `while` loops.  
The most common usage of `while` loop is to read a file and it will go through each line and assign them to variables.
Let's go to `LinuxAdvance/whileloops`, take a look at `testfile` and run this:

```
while read l
do  echo $l is a letter
done < testfile
```

Could you figure out what while does?

<details>
  <summary><b><u>Hint</u></b></summary>
  The first line saying while you are reading a line from a file, you assign it to <code>l</code> and do the things between <code>do</code> and <code>done</code>.  
  The last line uses <code>&lt;</code> to indicate which file you are reading.
</details>
<br/>

Now, your turn, copy three of your genome assemblies and the fasta with genes of interest into the folder. Then, write a code to complete the task.
Note: use `nano` to create the files that you are reading with `while`.

<details>
  <summary><b><u>Hint</u></b></summary>
  It should be something like this:
  <pre>while read l
do makeblastdb -dbtype nucl $l
  blastn -db $l -query [&lt;yourquery&gt;] -outfmt 6 -out tblastn-$l.txt  
done &lt; [&lt;yourfastalist&gt;] </pre>
Also see that I combined makeblastdb and blast so I don't need two loops! 
</details>
<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  Remember that you can combine the variables with a string and so, you don't need to add <code>.fasta</code> in your fasta list!
  <pre>while read l
do makeblastdb -dbtype nucl $l
  blastn -db $l.fasta -query [&lt;yourquery&gt;] -outfmt 6 -out tblastn-$l.txt  
done &lt; [&lt;yourfastalist&gt;] </pre>
  This way, your output file name won't have the ugly <code>.fasta</code> and be so much cleaner!
</details>
<br/>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  If you type something like 
  <pre>while read A B C  </pre>
  It will treat your read in file like a table and put the three columns into variable <code>A</code>, <code>B</code> and <code>C</code>!
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
do  sed 's/>/>'$f'/g' $f >> compiled.fasta
done  </pre>
  You will get something that's sort of usable with this script.<br/>
  But it's ugly. you will have <code>.fasta</code> inside your sequences. What can you do? Well, just pipe it to another <code>sed</code> to remove it (and maybe replace it with something sensible!) <br/>
  Also, if you already have <code>compiled.fasta</code>, it will just be appended continously. So, make sure you remove it first.
</details>

<br/>

Take a look at the blast results what did you find?

### sed with regular expression (Regex)

#### Start and End of a line

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
sed 's/A$/B/g' somefile
```

This will replace every `A` at end of a line with `B`. 

`^` and `$` are parts of regular expression (Regex). They specify certain search patterns. Using it you can do some more specific or fuzzy searches.
I hope that you are interested in Regex now. And we will learn some other useful Regex!

#### Wild Cards

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

#### Bracket Expressions

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
sed 's/l\{2\}/XXX/' ECMspecies
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

#### Marked Subexpression

Now, let's say we want move the numbers to the beginning of the line, we can use marked subexpression `\(\)`. 

Run the followings:

```
echo ABCDEFGH | sed 's/^\(.*\)\(F\)/\2\1/'
```

What does it do? Let's ignore the `\(\)` first. And so it will look like:
```
echo ABCDEFGH | sed 's/^.*F/\2\1/'
```
`^` indicates the match needs to start from the beginning. After `.*` we find `F` and we replace them with `\2` and `\1`.  
`\1` and `\2` are defined by `\(\)`. `\1` corresponds to the first and `\2` correspond to the second.  

If it makes sense, try to move the numbers to the beginning of lines in `ECMspecies` like this:
```
114 Laccaria species
```

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sed 's/\(.*\) \([0-9]\{1,\}\)/\2 \1/' ECMspecies  </pre>
</details>

<br/>

### grep
`grep` also supports the usage of Regex. Are you able to find all the genera with species number equal or higher than 10 but lower than 100? (10~99)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>grep ' [0-9]\{2\} ' ECMspecies  </pre>
</details>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  The Regex we used was POSIX basic regex. There's also a thing called POSIX extended basic regex. You can use <code>-E</code> to enable it. You don't need <code>\</code> for <code>{}</code> and <code>()</code> if you are using the extended version. And there are a few other functions that you can use. Learn more [here](https://en.wikipedia.org/wiki/Regular_expression)!
</details>

<br/>

![band](../img/band.png)

<br/>

## Dealing with Tables

### cut

After that tangent, let's go back to our Blast results. The format of outfmt is a table, in tab-separated values (`.tsv`). Note: there's also comma-separated values (`.csv`).

Go to `LinuxAdvance/tables` and copy one of your Blast result into the folder. The option that I use the most is `-f` (field). Check the manual with `man` to see how to cut out the E-value.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cut -f 11 [&lt;yourblastresults&gt;]  </pre>
</details>
<br/>

You can also cut out a few columns. Let's try the query sequence id, database sequence id, and the start and end for both query and databases. 

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>cut -f 1,2,7-10 [&lt;yourblastresults&gt;]  </pre>
</details>

<details>
  <summary><b><u>Click to learn more</u></b></summary>
  <code>.csv</code> is often better than <code>.tsv</code> because handling tabs is not the easiest thing to do. You can use <code>-d</code> to let <code>cut</code> to recognize <code>,</code> instead of tabs as delimiter.
</details>
<br/>

### sort

We used `sort` before. However, it sorts by lines. It can sort a table by columns as well.

You can take a look at `-k` (field) in the manual first and see what you find.

```
-k field1[,field2], --key=field1[,field2]
```

Basically you need to specify a range to sort with. And normally we only want one column, so it would be something like `-k 1,1`.

Let's try to sort the identity column. 

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  <pre>sort -k 3,3 [&lt;yourblastresults&gt;]  </pre>
</details>
<br/>

However, you might notice that the sort doesn't make sense at all. It's sorting by characters not numbers.  
To solve this issue, we can add `n` before `k`.

```
sort -nk 3,3 [<yourblastresults>]
```

It's also possible to reverse the order

```
sort -nrk 3,3 [<yourblastresults>]
```

You can also sort by more than one column. By adding more `-k`.

```
sort -k 1,1 -nrk 3,3 [<yourblastresults>]
```

Let's see if you can sort the file by query id, reverse order of database id and a reverse numeric order for the identity.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>sort -k 1,1 -rk 2,2 -nrk 3,3 [&lt;yourblastresults&gt;]  </pre>
</details>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  Like <code>cut</code>, you can let <code>sort</code> to recognize <code>,</code> instead of tabs as delimiter, but with <code>-t</code>.
</details>
<br/>

### awk

#### Variables in awk
Well, `awk` is a beast. To me, it's a computational language just like R, C and python, but simpler.  
We won't be able to cover everything about `awk`. Neither I know much about it, but we'll just go through a few to show case the power of `awk`.

Let's run this and see what happens

```
awk '{print $3, $1}' [<yourblastresults>]
```

As you can see, it prints out the third and first fields linked by a space. The fields were indicated by `$` (Note: `$0` is the whole line). The space is a delimiter introduced by `,`. See what happen if you don't include `,`! 

OK, but what if we want to use something else as delimiter?  
We can set the output field separater `OFS`, with `-v`.

```
awk -v 'OFS=\t' '{print $3, $1}' [<yourblastresults>]
```

The space is now replaced with a tab, which is coded as `\t`.

If you want specifically give a special delimiter between two fields, you can replace `,` with your delimiter and `"`. For example:

```
awk '{print $3 "xxx" $1}' [<yourblastresults>]
```

You may have notice that `awk` treat things in `""` as a string and just glue everything together.

Now, your turn. Try to print out the database sequence ids and start and end of the database sequences of each line using a `.csv` format. And instead comma, let's place `-` between the start and end.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>awk -v 'OFS=,' '{print $2, $9 "-" $10}' [&lt;yourblastresults&gt;] </pre>
</details>
<br/>

#### Calculations

You can do calculations in awk as well.
For example, you can add up a couple numbers:

```
awk '{print $9 + $10 - 3}' [<yourblastresults>]
```

Here, because `3` is a number, you don't need to add `""` around it. 

There are also some functions you can use such as square root.

```
awk '{print sqrt($9 + $10 - 3)}' [<yourblastresults>]
```

Let's calculate the length of each database sequence of each hit (start to end). (There's no absolute function in `awk`. The easy way is to use square and then square root: `sqrt(X^2)`).

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>awk '{print sqrt(($9 - $10)^2) + 1}' [&lt;yourblastresults&gt;] </pre>
</details>

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  You should notice that Blast tells you the position of the start and the position of the end. Therefore, <code>end - start</code> is not accurate. Instead, you'll need to add 1.
  <br/>
  Math is important!!!
</details>
<br/>

#### Begin and End

Notice that `awk` does stuff in `{}` line by line. But sometimes, we want to do things at the beginning or the end of reading a file.

For example, we can print out some stuff to the output file.

```
awk 'BEGIN{print "start!"}{print $3, $1}END{done!}' [<yourblastresults>]
```

You can imagine, if we do some calculation etc. It could be quite powerful. 

Like, we can calculate how many lines there are in the file.

```
awk 'BEGIN{i = 0}{print $3, $1; i = i + 1}END{print "We have " i " lines!"}' [<yourblastresults>]
```

First, we assign `0` to a variable `i` at the beginning. Then we read lines, print out and do the things after `;`, which is assign `i+1` to `i`. (`;` indicates the first job is done, and move on to the next part. Just like the new lines in Linux). And at the end, we print out `i`.

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  We actually don't need to do this to count the lines. This is just an example.
</details>
<br/>

#### if else
You can also use `if` and `else` in `awk`.  
If we want to print out all the lines of `queryA` hits but replace others with `XXX`, we can do something like this

```
awk '{if($1=="queryA"){print $0}else{print "XXX"}}' [<yourblastresults>]
```

Here, `awk` runs the stuff inside the first `{}` when reading each line. And it meets an `if` clause, asking if the first field is `queryA`. If yes, run the things in the second `{}`; if no, run the things in the third `{}`.

Let's see if you can use it to figure out the directions of the hits! (You can use `>`, `<` and do calculations inside the `if` clause too!)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>awk '{if($10>$9){print "+"}else{print "-"}}' [&lt;yourblastresults&gt;]  </pre>
</details>
<br/>

If clause also can use some operators, such as AND `&&` and OR `||`. Guess what happens if you run the code below: (It might not work with your result.)

```
awk '{if($9>100 && $10<3000){print $0}}' [<yourblastresults>]
```

Play with it to get the idea.

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  <code>awk</code> also support <code>sed</code> like expression (something like <code>/ABC/</code>). But I don't use it often since it seems like you can just use if else clauses instead.
</details>
<br/>

#### Line Numbers

There are some native variables in `awk`. I'll only introduce Number of Records `NR`.  
You can think `NR` as the line numbers. Let's see what happen if we run this:

```
awk -v 'OFS=\t' '{print NR, $0}' [<yourblastresults>]
```

What did it do?  
Using `NR`, could you print out the 3rd to 5th lines of your blast results?

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>awk '{if(NR&gt;2 && NR&lt;6){print $0}}' [&lt;yourblastresults&gt;]  </pre>
  You can replace <code>NR&gt;2</code> with <code>NR&gt;=3</code> which could be more intuitive.
</details>
<br/>

Lastly, let's try to write a code to turn fastq files to fasta files! Subset a fastq file with `head -n 40` to your current directory.  
Remember fastqs are in four line blocks. The first line is the sequence name with `@` at the beginning. And the second line is the sequence. Here, `%` will be useful. It outputs remainder from a division. For example, `9 % 3 == 0` and `6 % 5 == 1`.  
Also, you don't need to do it solely with `awk`. Be creative!

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>awk '{if(NR%4==1 || NR%4==2){print}}' [&lt;yourfastqfile&gt;] | sed 's/@/>/g'  </pre>
</details>
<br/>


---
layout: page
permalink: /misc/blast
title: "Blast"
---

![band](../img/band.png)

## Knowing your dataset
### Queries

To start to BLAST on local computers, we will first use two of my favorite genes, encoding DNA polymerase alpha subunit B, and Clathrin heavy chain, as examples. These genes are supposed to be single copied so they would be easier to deal with than many of genes of your interest.  
I've took the coding sequences (CDSs) from <i>Amanita phalloides</i> and stored them in a fasta file: `BLAST/query.fasta`.
So let's head to `BLAST` and see what we are dealing with.

<br/>

### Databases

You should have already played with the genomes already. Pick your favorite one and copy it into the `BLAST` directory. Also, we want to generate a protein database as well. Normally, it would be come from a genome annotation, but we will use BUSCOs instead.  
And so, we need to put all the BUSCOs into a file. Figure out a way to do that with the commands we learned! (Single-copied only should be fine.)

<br/>

## Making databases

Making databases for Blast is quite straightforward. You only need `makeblastdb`, `-dbtype` and `-in`. (You might notice that we there's only one hyphen before these multiple-character options. It's simply because different developers use different syntax. So, you'll need to look at tutorials/manuals to learn these softwares.)

I will help you with the genome database.
(Remember to load module before running `module load ncbi-blast-2.12.0+`)

```
makeblastdb -dbtype nucl -in [<yourfasta>]
```

Basically, you need to specify it's a nucleotide database. Check what's in the directory!

Now, you also know how to make a protein database! (Use `makeblastdb -help` to get help.) 

<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  It is worth noting that you can change output database name with <code>-out</code>. It is useful when you want to build a database for a fasta from a different folder. For example,
  <pre>makeblastdb -dbtype nucl -in somedir/somefasta -out XXX  </pre>
</details>
<br/>

## BLAST!!

We will start with `blastn`, which is using a nucleotide query to search in a nucleotide database. Let's try 

```
blastn -db [<databasename>] -query query.fasta -out blastn.txt
```

`[<databasename>]` is your fasta filename, if you didn't use the `-out` option.

Now, take a look at `blastn.txt`. What did you see? Why is that?

How about we translate the genes into protein using [Expasy](https://web.expasy.org/translate/), save them into fasta format and use the protein sequences to blast? (Which blast should you use?)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tblastn -db [&lt;databasename&gt;] -query [&lt;proteinfasta&gt;] -out tblastn.txt  </pre>
</details>
<br/>

What did you find? Why does it perform differently from `blastn`?

Okay, that is all good, but the output format isn't the best: it's hard to extract information. I like to use `-outfmt 6` instead. It gives you a "tab-delimited file", which is basically a table.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tblastn -db [&lt;databasename&gt;] -query [&lt;proteinfasta&gt;] -outfmt 6 -out tblastn-fmt6.txt  </pre>
</details>
<br/>

Take a look at your output. What does each column mean?  
Why does each query have multiple hits?

Now, let's try to use our protein database. 

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>blastp -db [&lt;databasename&gt;] -query [&lt;proteinfasta&gt;] -outfmt 6 -out blastp-fmt6.txt  </pre>
</details>
<br/>

How's the performance of it? When will it be more or less favored than a nucleotide database?
<br/>

## Get sequence

Often times we want to get the sequences instead of just having the hit range. There are multiple ways to do it. Here, we will use the Blast suite. 

Let's add an option `-parse_seqids`. To your `makeblastdb`.

```
makeblastdb -dbtype nucl -in [<yourfasta>] -parse_seqids
```

Adding this option will provide some more information to the database allowing later sequence extraction.

Then you can run:

```
blastdbcmd -db [<yourfasta>] -dbtype nucl -entry [<hitsequenceid>] -range [<hitsequencerange>]
```

Note that `hitsequencerange` should be typed like `3-21`. 

You can also extract multiple genes at once. Such as, 

```
blastdbcmd -db [<yourfasta>] -dbtype nucl -entry_batch [<yourregionsofinterest>]
```

`yourregionsofinterest` should be a file name including an entry and a range in each line, separated by space. For example, `seqid 3-21`.

Now, try to extract your own genes! Think and discuss what's the most sensible strategy for your study.  

<br/>

## See also
- [Smith Waterman algorithm](https://en.wikipedia.org/wiki/Smith%E2%80%93Waterman_algorithm)
- [Blast output format 6](https://www.metagenomics.wiki/tools/blast/blastn-output-format-6)

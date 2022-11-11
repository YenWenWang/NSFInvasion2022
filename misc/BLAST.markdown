---
layout: page
permalink: /misc/blast
title: "Blast"
---

![band](../img/band.png)

## Knowing your dataset
### Queries

To start to BLAST on local computers, we will first use two of my favorite genes, encoding DNA polymerase alpha subunit B, and Clathrin heavy chain, as examples. These genes are supposed to be single copied so they would be easier to deal with than many of genes of your interest.  
I've took the coding sequences (CDSs; basically the things translated into proteins) from <i>Amanita phalloides</i> (a distantly related <i>Amanita</i> species) and stored them in a fasta file: `DennyMaterials/BLAST/query.fasta`.
So let's head to `DennyMaterials/BLAST` and look at the contents of `query.fasta`.

<br/>

### Databases

You should have already played with the genomes already. Copy the genome assembly (likely in `~/11666_SizeFiltered.fasta` or `~/busco/11666_SizeFiltered.fasta`) into the `~/DennyMaterials/BLAST` directory. Also, we want to generate a protein database as well. Normally, it would be come from a genome annotation, but we will use BUSCOs instead.  
So, we need to put all the BUSCOs into a file, and we will only use single-copied ones. (They should be in `~/busco/home/genhons*/11666_buscoOut/run_basidiomycota_odb10/busco_sequences/single_copy_busco_sequences`). Figure out a way to do that with the commands we learned! (Remember `cat`?)

<details>
  <summary><b><u>Hint</u></b></summary>
  To copy the genome, you do something like
  <pre>cp [&lt;path to genome&gt;] .  </pre>
  To make the protein database, you do something like
  <pre>cat ~/busco/home/genhons*/11666_buscoOut/run_basidiomycota_odb10/busco_sequences/single_copy_busco_sequences/* &gt; busco.fasta  </pre>
  If your busco failed let us know.
</details>
<br/>

## Making databases

Making databases for Blast is quite straightforward. You only need `makeblastdb`, `-dbtype` and `-in`. (You might notice that we there's only one hyphen before these multiple-character options, but normally there should be two. This is simply because different developers use different syntax. So, you'll need to look at tutorials/manuals to learn these softwares.)

I will help you with the genome database.
(Remember to load module first by running `module load ncbi-blast-2.12.0+`)

```
makeblastdb -dbtype nucl -in [<yourfasta>]
```

You want to replace `[<yourfasta>]` with your genome fasta file. And by `-dbtype nucl` you specify that it's a nucleotide database. Check what's in the directory!

Now, you also know how to make a protein database! (Use `makeblastdb -help` to get help.) 
<details>
  <summary><b><u>Click to learn more!</u></b></summary>
  <pre>makeblastdb -dbtype prot -in [&lt;yourfasta&gt;]  </pre>
</details>
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

`[<databasename>]` is your fasta filename if you didn't use the `-out` option.

Now, take a look at `blastn.txt`. What did you see? Why is that? (Talk!!!)

How about we translate the genes into protein using [Expasy](https://web.expasy.org/translate/), save them into fasta format and use the protein sequences to blast? (Which blast should you use?)

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>tblastn -db [&lt;databasename&gt;] -query [&lt;proteinfasta&gt;] -out tblastn.txt  </pre>
</details>
<br/>

What did you find? Why does it perform differently from `blastn`?

Okay, that is all good, but the output format isn't the best: it's hard to extract information. I like to use `-outfmt 6` instead. It gives you a "tab-delimited file", which is basically a table but instead of grids, it uses tabs and new lines.

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
blastdbcmd -db [<yourfasta>] -dbtype nucl -entry [<hitsequenceid>] -range [<hitsequencerange>] -strand [<plus or minus>]
```

Note that `[<hitsequencerange>]` should be typed like `3-21` and `[<plus or minus>]` depends on if you want the forward or reverse strand of the sequence.

You can also extract multiple genes at once. Such as, 

```
blastdbcmd -db [<yourfasta>] -dbtype nucl -entry_batch [<yourregionsofinterest>]
```

`yourregionsofinterest` should be a file name including an entry, a strand direction and a range in each line, separated by a space. For example, `seqid minus 3-21`.

<br/>

### Extract Genes for Phylogenetics

Now, we want to extract genes to make a phylogeny. This way, we can compare our samples to the samples from previous studies. We have prepared the <i>A. muscaria</i> sequences from [Geml et al. 2008](https://www.sciencedirect.com/science/article/pii/S105579030800208X?via%3Dihub) and [Vargas et al. 2008](https://pringlelab.botany.wisc.edu/documents/vargas2019.pdf), so you only need to extract the same four genes from your genome.  

Head to `DennyMaterials`, make a directory called `phyloBLAST` and copy the query (`/home/genhons1/DennyMaterials/Gemlquery.fasta`) to the folder.

Next, copy your genome assembly to the folder, too. Everyone has a different sample. You can figure out the one for which you are responsible by looking into the files in `~/Data/Illumina/`. And copy the corresponding assembly fasta file from `/home/genhons1/PhylogenomicMaterials/genomes/` into `phyloBLAST`.

Use `makeblastdb` to create a database (remember to add `-parse_seqids` to allow sequences retrieval) and `blastn` to search for the four genes from `Gemlquery.fasta` in your genome.

<details>
  <summary><b><u>Hint</u></b></summary>
  <pre>makeblastdb -dbtype nucl -in [&lt;yourgenomefasta&gt;] -parse_seqids  </pre>
  <pre>blastn -db [&lt;yourgenomefasta&gt;] -query Gemlquery.fasta -outfmt 6 -out blastn-Geml.txt  </pre>
</details>
<br/>

Take a quick look at the results. Do you see multiple lines with the same subject ID for the top hit? It shouldn't. But btub and tef1a are protein coding genes, why aren't they fragments? Also, are there any query sequence without any hits? (Let us know if that's the case!)

Use `blastdbcmd` to extract the top hit sequence for each query sequence. Like below: (I'm showing one at a time so that it's not too complicated.)

```
blastdbcmd -db [<databasename>] -dbtype nucl -entry [<subjectid>] -range [<subjectrange>] -strand [<plus or minus>] > [<genename>].fasta
```

`[<subjectid>]` is in the second column of your blast results. `[<subjectrange>]` is `start-end` of the subject (Note the `start` needs to be lower than `end`). And `[<plus or minus>]` is decided by if your blast hit is forward or reverse (if the "subject start" in your result is lower than "subject end", it needs to be `plus`, otherwise it should be `minus`.)

Now, you should get four `[<genename>].fasta`. Rename the sequences with the gene names (its, lsu, tef1a or btub; you can use `sed`, `nano`...) 

Lastly, copy each fasta into corresponding `/home/genhons1/StudentBlastResults/[<genename>]` and change the file name into your sample name. <b>Remember to not copy into the file and then change the name: IT WILL MESS THINGS UP!</b> It should look like this.

```
cp [<genename>].fasta /home/genhons1/StudentBlastResults/[<genename>]/[<samplename>].fasta
```

<br/>

## See also
- [Smith Waterman algorithm](https://en.wikipedia.org/wiki/Smith%E2%80%93Waterman_algorithm)
- [Blast output format 6](https://www.metagenomics.wiki/tools/blast/blastn-output-format-6)

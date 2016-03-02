# Using_liftOver_to_retrieve sequences

# Success

To start you should have:

1. chain file (one for each **species of interest**)
2. .bed file with **regions of interest** from *Drosophila melanogastor*
3. **species of interest** assembly file

### Workflow 

**Step 1**: Use `liftOver` to translate regions of interest from *D. melanogastor* to species of interest. In directory with chain file, use this example command: 

    ~/programs/liftOver/liftOver -minMatch=0.1 -multiple ~/data/testBED.bed Dmel_to_MEMB002A.over.chain ~/data/testOutput.bed ~/data/testUnlifted.bed

Output is put into the file `testOutput.bed`.  If you check this file it will tell you how many regions were translated.  They are labelled in the last column of the output .bed file. Also check how many sequences were not lifted in the `testUnlifted.bed` file.

**Step 2**: Use `bedtools` `fastaFromBed` tool to get sequences in .fasta format from the **species of interest**. Make sure you copy the original .fa file into a folder with write privileges. Run this example command

    fastaFromBed -fi MEMB002A_velvet_gap_closer_reapr_pipeline_break_default_gap_closer_1kbplus_upper_short_header.fa -bed testOutput.bed -fo testOutput.fasta

## Problems

The overall goal is to get all this information back into the large database.

1. The output fasta entry name does not match anything from the database. Although in the intermediate .bed file, the original id name is there. So that could be used as an intermediate step.....
2. When you perform liftOver you often get multiple sequence matches. Make sure you understand what is going on here. 
3. The sequences are going to be different lengths for every species. 

The key is to really specify how you want to be able to use this database....


# How I got to Success

## liftOver

Program that allows you to move annotations from one assembly to another. This tool converts genome coordinates and genome annotation files between assemblies. 

### Installing liftOver application

Used to install liftOver binaries. 

	rsync -aP rsync://hgdownload.cse.ucsc.edu/genome/admin/exe/linux.x86_64/ ./liftOver

To make binary executable
    
    chmod +x liftOver

### Using liftOver

The liftOver usage is located [here](http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/FOOTER)

From Bronski: The application takes as input a BED file of annotated features in the *D. melanogaster* genome, and outputs a BED file of corresponding coordinates in the montium genome.  Here's a sample command that should serve as a decent starting point, but you do need to inspect the accuracy of the "lifts".

**Steps to use liftOver**

Reference liftOver Tutorial: [http://www.geneticlegacies.com/2012/01/basic-guide-to-ucsc-liftover-command.html](http://www.geneticlegacies.com/2012/01/basic-guide-to-ucsc-liftover-command.html)

1. To begin, the data file you want to convert has to be in the [BED Format](https://genome.ucsc.edu/FAQ/FAQformat.html#format1).

I believe I first need to make the BED file of all the features I want from the drosophila genome.  So a list of the enhancer elements that I want to get from Drosophila.

Used in directory of where .chain file is.

`~/programs/liftOver/liftOver -minMatch=0.1 -multiple ~/data/testBED.bed Dmel_to_MEMB002A.over.chain ~/data/testOutput.bed ~/data/testUnlifted.bed`
  
But gave the error:

`Can only lift BED4, BED5, BED6 to multiple regions`

I believe this is refering to the bed file. I think I need a bed file with >3 columns, or BED4 format. Lets try again, but with a BED4 file.  I added a column which refers to the enhancer ID as annotated in [Kvon et al., 2014](http://www.nature.com/nature/journal/v512/n7512/full/nature13395.html).

## Step 2: Making the FASTA file with the sequences

Looks like that worked, but now I am unsure how to **1.** get the sequences...ideally in FASTA. I also need to **2.** test if the liftover was accuratey "lifted". 

### Install Bedtools

Version: bedtools-2.25.0
Date Downloaded: 23 February 2016

    $ wget https://github.com/arq5x/bedtools2/releases/download/v2.25.0/bedtools-2.25.0.tar.gz
    $ tar -zxvf bedtools-2.25.0.tar.gz
    $ cd bedtools2
    $ make

### Using Bedtools

[BEDTOOLs `fataFromBed`](http://bedtools.readthedocs.org/en/latest/content/tools/getfasta.html) is likely the best option.

    fastaFromBed -fi ../montium_genomes/Sample_MEMB002A_index5/MEMB002A_velvet_gap_closer_reapr_pipeline_break_default_gap_closer.fa -bed testOutput.bed -fo testOutput.fasta

**Problem 2.1**:
I get an error: 

    index file ../montium_genomes/Sample_MEMB002A_index5/MEMB002A_velvet_gap_closer_reapr_pipeline_break_default_gap_closer.fa.fai not found, generating...
    could not open index file               ../montium_genomes/Sample_MEMB002A_index5/MEMB002A_velvet_gap_closer_reapr_pipeline_break_default_gap_closer.fa.fai for writing!
    
My first guess is this problem has to do with write privileges in the directory where `MEMB002A_velvet_gap_closer_reapr_pipeline_break_default_gap_closer.fa` is. It is not able to write a .fai file.  But what the fuck is a .fai file anyway? 
- answer: [faidx](http://manpages.ubuntu.com/manpages/vivid/man5/faidx.5.html) - an index enabling random access to FASTA files
- In the future find a way to specify where it write this .fai file. I don't want it in the original `montium_genomes` directory

**Solution**:
I copied this file to a folder that has write privilages and tried again. 

**Problem 2.2**:
That seemed to work, but came through with another problem:

  WARNING. chromosome (22015_130691_13.243315) was not found in the FASTA file. Skipping.

This was repeated many times.  It is thinking that the first column is a chromosome ID, but since these are scaffolds... I believe the problem is that the LiftOver BED output file, `testOutput.fasta`  that was generated looks like this:

    22015_130691_13.243315  12054   12061   VT0009  1
    22015_130691_13.243315  12765   13166   VT0010  1
    22015_130691_13.243315  13914   14513   VT0011  1
    22015_130691_13.243315  16324   17070   VT0013  1
    22015_130691_13.243315  22875   23616   VT0015  1
    22015_130691_13.243315  23991   24613   VT0016  1
    
Question: Where in the hell did that first column id come from? Maybe the chain????  Answer: yes.

Got stuck and asked Mike.  Turns out this wouldn't have worked because the names don't match and these assemblies contain such small scaffolds.  Mike gave me other assemblies that have to be at least 99 bp.  They are place in `montium_data_ciera_new_assemblies`. 
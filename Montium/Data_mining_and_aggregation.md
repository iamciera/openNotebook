# Data_mining_and_aggregation

## Kvon Data

Publication: [Kvon et al., 2014](http://www.nature.com/nature/journal/v512/n7512/full/nature13395.html)

Generated from Vienna Tile GAL4 driver lines: [http://stockcenter.vdrc.at/control/vtlibrary](http://stockcenter.vdrc.at/control/vtlibrary.  These lines were also characterized in the brain, but the online system for this dataset is weird.

-  13.5% of the non-coding genome 
-  27 out of 28 known enhancers were found ([Figure](http://www.nature.com/nature/journal/v512/n7512/fig_tab/nature13395_SF2.html)
-  3557 / 7705 are active

Data Cleaned from site with `kvonDataClean.Rmd`.  File: `kvonClean09_Feb2016`
Dimentions 561096 x 16.  
Missing: TFBS (including PWM scores ect)

![cleaneDataSnapshot](quiver-image-url/D83F854001F2DF381F581BEB06C9201B.png)

## Notes on data preparation 

Downloaded dataset from [http://enhancers.starklab.org/browse/](http://enhancers.starklab.org/browse/). "Download search results as a text file" 

I manually entered the data information to kvonDatabase.csv using the known enhancer .png file from [Supplemental data 2](http://www.nature.com/nature/journal/v512/n7512/fig_tab/nature13395_SF2.html).

The information about the different stages is collapsed into single colums. I need to do some data cleaning to make more accessible.

## To Do

- [ ] find what the `verification_staus` and 'postive' columns mean.  *There are several of the 28 which are not verified/*
- [ ] make the columns for the stages make sense and be usable. 
- [ ] make all the blank columns in the gene names `NA`
- [ ] make bed file to scrape sequences

# Bronski Data

**Questions for Bronski**

1. What are the Read 1 and Read 2 files ex(`MEMB002A...pair_1.fq`, `MEMB002A...pair_2.fq`)? Why are there two?

**Email from Bronski:**

Hi Ciera,

It took a little longer than expected, but I copied a bunch of files to your account on the sever. You can find them in the directory **montium\_genomes**, which contains 12 subdirectories for the 12 different samples / species. I've attached a file (**montium\_readme.txt**) that lists the corresponding species and sample names. (This used to be the README file on our FTP server.)

I'll now take you through the various files in the subdirectories, using *D. rufa* (Sample\_MEMB002A\_index5) as an example.

**MEMB002A\_index5\_ACAGTG\_L007\_R1\_combined\_filtered\_bbduk\_k25\_Q10.fastq.cor.pair\_1.fq
MEMB002A\_index5\_ACAGTG\_L007\_R2\_combined\_filtered\_bbduk\_k25\_Q10.fastq.cor.pair\_2.fq**

These are the Read1 and Read2 files that were adapter trimmed, quality trimmed, and error corrected. Adapter / quality trimming was done using BBDuk, and error correction was done using SOAPec. Assembly [velvet](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC2336801/).

**MEMB002A\_velvet\_gap\_closer\_reapr\_pipeline\_break\_default\_gap\_closer.fa**

These are the final Velvet scaffolds. After the initial assembly (k=49) I filled in gaps using Gap Closer, evaluated the assembly and broke apart mis-assemblies using the [REAPR](http://www.genomebiology.com/2013/14/5/R47) pipeline, and then ran Gap Closer one final time.

**Dmel\_to\_MEMB002A.over.chain**

This is a liftOver chain file that was generated after aligning each *montium* assembly to the *D. melanogaster *genome. (Due to highly fragmented assemblies because of high heterozygosity, I didn't align three assemblies: *D. aurora *(Sample\_MEMB003E\_index16), *D. triauraria* (Sample\_MEMB002B\_index6), and *D. leontia* (Sample\_MEMB003A\_index2).)

You can use this file to remap coordinates from any annotated feature (like an enhancer) in the *D. melanogaster* genome onto a *montium* assembly. 

You'll need to download the **liftOver** application that was written for the UCSC Genome Browser. You can download binaries built for linux here: [http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86\_64/](http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/). (The FOOTER file contains usage instructions.) Then make the application executable (e.g., chmod +x liftOver).

The application takes as input a BED file of annotated features in the *D. melanogaster* genome, and outputs a BED file of corresponding coordinates in the *montium* genome. Here's a sample command that should serve as a decent starting point, but you do need to inspect the accuracy of the "lifts".

**$ liftOver -minMatch=0.1 -multiple input.bed ****Dmel\_to\_MEMB002A.over.chain**** output.bed unMapped**

**
**

Let me know if you have any questions!

Best,

Michael

**To-Do List**

get data from Bronski

 understand liftOver

 identify all the properties of enhancers that can be applied to models 

 get list of known enhancers (coordinates)

 kvon 

 Clean

  **28 enhancers** 

 Combine Data sets 

 Make script that generates BED files

TFBS 

 get list of known binding sites

  Drosophila cis-regualtory database

Visualization

 Look into ways to visualize results which can easily be 

 D3
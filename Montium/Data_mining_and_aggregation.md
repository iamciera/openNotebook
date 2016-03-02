# Data_mining_and_aggregation

Over all goal: To find molecular logic of gene regulation.

Using the Kvon Data assumption: That the enhancers have similar funtion across species. Find the common principles that unite them what divergence patterns are allowd. 

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
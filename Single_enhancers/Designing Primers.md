# Designing Primers

## Approach

Design against 27 species of Drosophila. They already did the alignment. I just need to be able to get the alignment, ideally in fasta format. To do this I need a good way to extract this information easily and reproducibly. I will need to do this again eventually. This is a great datset. 

So far I have.

1. Coordinates of the region I want `ch2R  5861246	5863407`
2. Browse the sequences, by block, aligned but in shitty html in the UCSC.   
3. `.maf` file of alignemt (1.2gb)
4. `.fasta` file of alignment (created from .maf file) (1.2gb)


One approach is to browse the sequences and find the where in the alignment my region of interest is. Then create a `.bed` file to extract the information using fastaFromBed. 

How To Extract Specific Coordinates From Multifasta File: [https://www.biostars.org/p/6337/](https://www.biostars.org/p/6337/)
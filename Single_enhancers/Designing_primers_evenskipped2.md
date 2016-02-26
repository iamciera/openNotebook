# Designing_primers_evenskipped2

## Approach

Design against 27 species of Drosophila. They already did the alignment. I just need to be able to get the alignment, ideally in fasta format. To do this I need a good way to extract this information easily and reproducibly. I will need to do this again eventually. This is a great datset. 

So far I have.

1. Coordinates of the region I want `ch2R  5861246	5863407`
2. Browse the sequences, by block, aligned but in shitty html in the UCSC.   
3. `.maf` file of alignemt (1.2gb)
4. `.fasta` file of alignment (created from .maf file) (1.2gb)


One approach is to browse the sequences and find the where in the alignment my region of interest is. Then create a `.bed` file to extract the information using fastaFromBed. 

I am literally doing it by eye now. Which sucks.

## Designing Degenerate Primers

Where Eisen Lab gets its primers: [IDT](https://www.idtdna.com/site)
Checking primers: [here](http://www.bioinformatics.org/sms2/pcr_primer_stats.html)

1. (https://skeetersays.wordpress.com/2008/07/10/degenerate-pcr-a-guide-and-tutorial/)[https://skeetersays.wordpress.com/2008/07/10/degenerate-pcr-a-guide-and-tutorial/]

Great Summary of eve: [http://www.sdbonline.org/sites/fly/segment/evenskp1.htm](http://www.sdbonline.org/sites/fly/segment/evenskp1.htm)

Eve stripe 2: [http://elifesciences.org/content/2/e01135v1](http://elifesciences.org/content/2/e01135v1)

## Location 

VT14361	chr2R	5861246	5863407	2161	correct	1	eve_260-hsp70lacZ	eve
VT14362	chr2R	5862739	5864868	2129	correct	1	eve_Stripe_3+7	eve

From Redfly: chr2R 9977762 9978245 eve-striped-2 
From NCBI: [http://www.ncbi.nlm.nih.gov/nuccore/3258640/](http://www.ncbi.nlm.nih.gov/nuccore/3258640/)

    >gi|3258640|gb|AF042709.1|AF042709 Drosophila melanogaster even-skipped (eve) gene, stripe 2 enhancer region
    AATATAACCCAATAATTTGAAGTAACTGGCAGGAGCGAGGTATCCTTCCTGGTTACCCGGTACTGCATAA
    CAATGGAACCCGAACCGTAACTGGGACAGATCGAAAAGCTGGCCTGGTTTCTCGCTGTGTGTGCCGTGTT
    AATCCGTTTGCCATCAGCGAGATTATTAGTCAATTGCAGTTGCAGCGTTTCGCTTTCGTCCTCGTTTCAC
    TTTCGAGTTAGACTTTATTGCAGCATCTTGAACAATCGTCGCAGTTTGGTAACACGCTGTGCCATACTTT
    CATTTAGACGGAATCGAGGGACCCTGGACTATAATCGCACAACGAGACCGGGTTGCGAAGTCAGGGCATT
    CCGCCGATCTAGCCATCGCCATCTTCTGCGGGCGTTTGTTTGTTTGTTTGCTGGGATTAGCCAAGGGCTT
    GACTTGGAATCCAATCCTGATCCCTAGCCCGATCCCAATCCCAATCCCAATCCCTTGTCCTTTTCATTAG
    AAAGTCATAAAAACACATAATAATGATGTCGAAGGGATTAGGGGCGCGCAGGTCCAGGCAACGCAATTAA
    CGGACTAGCGAACTGGGTTATTTTTTTGCGCCGACTTAGCCCTGATCCGCGAGCTTAACCCGTTTTGAGC
    CGGGCAGCAGGTAGTTGTGGGTGGACCCCACGACTTTTTTGGCCGAACCTCCAATCTAACTTGCGCAAGT
    GGCAAGTGGCCGGTTTGCTGGCCCAAAAGAGGAGGCACTATCCCGGTCCTGGTACAGTTGGTACGCTGGG
    AATGATTATATCATCATAATAAATGTTT

When I blast and plot I get the same coordinates as above (chr2R:9977762 9978245) How about we try to get primers surrounding this region chr2R:9,977,423-9,979,366.  This is not a good region. Need to zoom out to find a more conserved region. Goal is to make nested degenerate primers. 

---

## Forward Primers - eve striped 2 

### DP_evestriped2_F1
![Screen Shot 2016-02-25 at 3.11.49 PM.png](quiver-image-url/DC5A0266983A1C2DD6EB77698B03B873.png)

    gcaatataacccaataatttgaag
    gcaatataacccaataattttaag
    gcaatataacccaataattttaac
    gcaatataacccaataatttgaac

evestriped2_F1: gcaatataacccaataattt{g,t}aa{g,c}

WARNING: GC content is less than 40%

### DP_evestriped2_F2

![Screen Shot 2016-02-25 at 3.23.46 PM.png](quiver-image-url/69970A442A0A63BB9E1DD8E250078F97.png)

    gtactgcataacaatgg

DP_evestriped2_F2 g{g,a}a{a,t,c}{t,c}tg{g,c}a{c,g}aa{g,c}{a,t}atgg

WARNING: GC content is less than 40%
WARNING: There are more than 3 self-annealing bases in a row:

                  gtactgcataacaatgga
                  ||||              
    aggtaacaatacgtcatg
 
## Forward Primers - eve striped 2 

### eve_VT14361_R1

![Screen Shot 2016-02-25 at 3.42.07 PM.png](quiver-image-url/CFDBFBED378789E3F159F1A076E2F3E2.png)

    gcctgcgggcgggcgagacaaaagattcgctcatccgctatga
                        aaagattcgctcatccgcta
    
![Screen Shot 2016-02-25 at 3.43.41 PM.png](quiver-image-url/9950F515308017B413D560BBE7F28B3E.png)

eve_VT14361_R1 tagcggatgagcgaatcttt

*This sequence is completely conserved.

More primers in the same region:

![Screen Shot 2016-02-25 at 3.46.19 PM.png](quiver-image-url/6C7D3D246A573255FAE2CA8ABCC89D34.png)

### eve_VT14361_R2

![Screen Shot 2016-02-25 at 3.49.36 PM.png](quiver-image-url/DBD84C81F2CFB0663103E6B80B25FCE2.png)

![Screen Shot 2016-02-25 at 3.52.03 PM.png](quiver-image-url/FD73B32BA32A9C4E8D0756CAB302C40D.png)

    cgaattatttgcgcttttatga
    
eve_VT14361_R2  c{g,a}aat{t,a}atttgc{c,g}cttttat{c,g}a

More primers in the same regions

![Screen Shot 2016-02-25 at 4.00.52 PM.png](quiver-image-url/C71DD9997077CF67753D455C64115643.png)

### eve_VT14361_R3

![Screen Shot 2016-02-25 at 4.10.02 PM.png](quiver-image-url/FEB0B1CCA08C8B1C8DA7D9E72D2F0653.png)

    aatgattatatcatcataataaatgttttgcccaa
    
![Screen Shot 2016-02-25 at 4.11.27 PM.png](quiver-image-url/5E601C267120AD4C8E74E4CD81AC66AB.png)

eve_VT14361_R3  {t,c,g}{t,c}{c,g,a,t}{c,g}g{g,c,a}{a,c,g}aaacatttattatgatg

----

## Final Primers

DP_evestriped2_F1 gcaatataacccaataatttkaas
DP_evestriped2_F2 grahytgsasaaswatgg
eve_VT14361_R1 tagcggatgagcgaatcttt
eve_VT14361_R2  craatwatttgcscttttatsa
eve_VT14361_R3  bynsgvvaaacatttattatgatg
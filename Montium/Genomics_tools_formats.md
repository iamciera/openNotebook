# Genomics_tools_formats

### Primers

Where Eisen Lab gets its primers: [IDT](https://www.idtdna.com/site)

### File Formatting


[BioPython Tool](http://biopython.org/wiki/Multiple_Alignment_Format)

[BED](http://mendel.iontorrent.com/ion-docs/BED-File-Formats-and-Examples_64062608.html#BEDFileFormatsandExamples-3-columnTargetRegionsBEDFileFormat)Nice guide to different types of BED formats.

[BED for the UC Brower](http://genome.ucsc.edu/goldenPath/help/customTrack.html)

#### MAF

## Handling maf files are killing me.
### BioPython Approach

    from Bio.AlignIO import MafIO
 
    # idx = MafIO.MafIndex(sqlite_file, maf_file, target_seqname)
    idx = MafIO.MafIndex("chr10.mafindex", "chr10.maf", "mm9.chr10")

### Resources

How To Extract Specific Coordinates From Multifasta File: [https://www.biostars.org/p/6337/](https://www.biostars.org/p/6337/)

Maf Extract tool in bioruby: [http://csw.github.io/bioruby-maf/man/maf_extract.1.html](http://csw.github.io/bioruby-maf/man/maf_extract.1.html)

BioPython MAF reader: [http://biopython.org/wiki/Multiple_Alignment_Format](http://biopython.org/wiki/Multiple_Alignment_Format)

[MAF to FASTA](https://bitbucket.org/galaxy/galaxy-central/src/default/tools/maf/interval_maf_to_merged_fasta.py?fileviewer=file-view-default)

### Alignment

[MAFT](http://mafft.cbrc.jp/alignment/server/) - Looks most updates: 

Alignment from [Hare et al. 2008](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.0020130): Modified the software we use to identify conserved binding sites [39] to recursively recover overlapping binding sites from multiple alignments, and assumed that these were orthologous binding sites.


### Data

[27 Genomes of Drosophila aligned](http://genome.ucsc.edu/cgi-bin/hgGateway?hgsid=476694991_Wf8IeL8fZYaJpMvHD9xnx3hDu15T)
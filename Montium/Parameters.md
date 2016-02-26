# Parameters

## Data 

* N number of transcription factors (TF)
* n number of transcription factor binding sites (TFBS) (PWM scores and Chip-seq) 
* validation score per TFBS)
* 7 Species
* 3 Species Complex (auraia, kikkawai, serrata)
* 6 developmental age
* 27 regions (227 specific)
* 27 (to start) or 3557(try) expression signal during embryogenesis.

---

## Parameters

From [Kim et al. 2013]()

binding of TFs - for instance set PWM value and only include if a certain threshold is achieved. 
steric competition between bound factors (overlapping)
cooperative binding of TFs to DNA 
activation 
short-range repression (also called ‘quenching’)
direct repression, 
coactivation 


---

## Prediction

Predict the expression signal during development by using architectural parameters. The measurements are directed by a few hypothesis. 
  
1.  *higher order binding*. TFBS aggregation patterning. Cooperative binding.
  * Number of TFs within each enhancer (quantified by how many times each unique TF is present) 
  * Length between same and different types of TFs (homo-dimeric or hetero-dimeric factor, and overlapping motifs = competitive binding by steric hindrance)
  * Biased arrangements of TFBS
  
Based on evidence that similar develpmental programs are enriched in the same TFBS. 

## Assumptions and further notes

1. Montium species have similar expression patterns to *Drosophila melanogastor*. 
2. Kvon et al., 2014, found enrichment of motifs within developmental stages (expression patterning). 
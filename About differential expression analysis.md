Everything about differential expression analysis.

# Differential expression analysis
## What is it?

## How was it done?
RNA-seq quantification using RNA-seq quantifiers such as Kallisto, RSEM, salmon, sailfish. 


## Kallisto
RNA-seq quantification method

Kallisto pseudoaligns reads to a reference, producing a list of transcripts that are compatible with each read while avoiding alignment of individual bases
Kallisto is geared towards quantification on the transcript (isoform) level, rather than the gene level 
Kallisto is primarily meant for quantification of an existing set of FASTA sequences. It does not perform transcript assembly and it cannot quantify the expression of novel transcripts that are not in the transcript index that you provide to it
```
https://scilifelab.github.io/courses/rnaseq/labs/kallisto
https://www.nature.com/articles/nbt.3519

```

## RSEM


## EdgeR


## DESeq2

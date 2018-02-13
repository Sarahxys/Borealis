Purpose: to document everything I learn about differential expression analysis.

# Differential expression analysis
## What is it?

## How was it done?
- RNA-seq quantification using RNA-seq quantifiers. RNA-seq quantifiers that use alignment method include. RNA-seq quantifiers that use alignment-free or pseudoalignment method include kallisto, salmon, sailfish. 
- Co


## Kallisto
- RNA-seq quantification method that use pseudoalignment. 
- Kallisto pseudoaligns reads to a reference, producing a list of transcripts that are compatible with each read while avoiding alignment of individual bases. 
- Kallisto is geared towards quantification on the transcript (isoform) level, rather than the gene level. 
- Kallisto is primarily meant for quantification of an existing set of FASTA sequences. It does not perform transcript assembly and it cannot quantify the expression of novel transcripts that are not in the transcript index that you provide to it
- **Output**: The results of the main quantification, i.e. the abundance estimate using kallisto on the data is in the abundance.tsv file. Abundances are reported in “estimated counts” (est_counts) and in Transcripts Per Million (TPM). Below is an example of kallisto output:
```
target_id	length	eff_length	est_counts	tpm
ENST00000513300.5	1924	1746.98	102.328	11129.2
ENST00000282507.7	2355	2177.98	1592.02	138884
```
```
https://scilifelab.github.io/courses/rnaseq/labs/kallisto
https://www.nature.com/articles/nbt.3519

```

## RSEM


## EdgeR


## DESeq2

Purpose: to document everything I learn about differential expression analysis.

# Differential expression analysis
## What is it?

## How was it done?
- RNA-seq quantification using RNA-seq quantifiers. RNA-seq quantifiers that use alignment method include. RNA-seq quantifiers that use alignment-free or pseudoalignment method include kallisto, salmon, sailfish. 
- Co


## Kallisto
- RNA-seq transcript abundance quantification tool that estimates transcripts abundance with pseudo-alignment method. 
- Kallisto pseudoaligns reads to a reference, producing a list of transcripts that are compatible with each read while avoiding alignment of individual bases. 
- Kallisto is geared towards quantification on the transcript (isoform) level, rather than the gene level. 
- Kallisto is primarily meant for quantification of an existing set of FASTA sequences. It does not perform transcript assembly and it cannot quantify the expression of novel transcripts that are not in the transcript index that you provide to it
- below is a brief description of how it works in steps:
  - indexing step: build transcriptome de Bruijn Graph (T-DBG) with k-mers from transcripts in the assembled transcriptome. In a hash table, store the information about the k-mers - which transcripts a k-mer is from and along with information the position of the k-mer in the transcript. 
  - pseudo alignment step: for each k-mer in the read, look for those k-mers in the hash table to found out which transcripts those k-mers could be from. In the case where a read has 5 k-mers and k-mer #1-#3 are from transcript A & B & C but k-mer #4-#5 are from transcript A & B, kallisto will then decide that the read is probably from transcript A &B.      
  - quantification step:  for a multi-mapping read like the example above, the read is fractionally assigned to each transcript based on the expectation-maximization algorithm. With the above example, a fraction of the read will be assigned to transcript A and transcript B.
- **Input**: transcriptome file and trimmed reads
- **Output**: The results of the main quantification, i.e. the abundance estimate using kallisto on the data is in the abundance.tsv file. Abundances are reported in “estimated counts” (est_counts) and in Transcripts Per Million (TPM). The output file is used in in downstream analysis such as differential expression level analysis Below is an example of kallisto output:
```
target_id	length	eff_length	est_counts	tpm
ENST00000513300.5	1924	1746.98	102.328	11129.2
ENST00000282507.7	2355	2177.98	1592.02	138884
```
- Manual and more detail
```
https://scilifelab.github.io/courses/rnaseq/labs/kallisto
https://www.nature.com/articles/nbt.3519

```

## RSEM


## EdgeR


## DESeq2

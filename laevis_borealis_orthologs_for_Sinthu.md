# Finding borealis orthologs for 3 laevis gene primers
## steps
- [x] make a fasta file with the primer sequences
- [x] build a build blastn database for borealise transcriptomes
- [x] blast the primer sequence to the blastn database
- [x] extract the sequence of the transcript that the primers match to

## Primer sequence file
the path to the file
```
/home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer.fa
```
the file:
```
>ef1a_forward
CCAGATTGGTGCTGGATATG
>ef1a_reverse
TTCTGAGCAGACTTTGTGAC
>vlg1_forward
GCTGCCAGAGGCTTGGATAT
>vlg1_reverse
ACTTGCTCTGCTTGCGATTG
>cyp17a1
TGAGTGACAGGAGAATTCTG
>cyp17a1
CGGTGCTACAGGGCGAATGC
```

## Blastn
To build blastn database for borealise transcriptomes
```
makeblastdb -in /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/borealis_denovo_oct2018_trinityout.Trinity.fasta -dbtype nucl -out /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/db_blastn_borealis_denovo_transcriptome_oct2018
```
The path to the blastn database for borealise transcriptomes is 
```
/home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/db_blastn_borealis_denovo_transcriptome_oct2018
```
blastn the primer sequence to the blastn database
```
time blastn -task blastn -db /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/db_blastn_borealis_denovo_transcriptome_oct2018/db_blastn_borealis_denovo_transcriptome_oct2018 -outfmt 6 -evalue 0.05 -query /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer.fa -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer_xb_transcriptome_blastn_out.tsv
```
the path to the output file
```
/home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer_xb_transcriptome_blastn_out.tsv
```
the output file
```
qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore
ef1a_forward    TRINITY_DN145449_c3_g2_i12      100.000 20      0       0       1       20      1895    1914    0.017   37.4
ef1a_forward    TRINITY_DN145449_c3_g2_i10      100.000 20      0       0       1       20      1640    1659    0.017   37.4
ef1a_forward    TRINITY_DN145449_c3_g2_i2       100.000 20      0       0       1       20      1756    1775    0.017   37.4
ef1a_forward    TRINITY_DN145449_c3_g2_i1       100.000 20      0       0       1       20      1548    1567    0.017   37.4
ef1a_reverse    TRINITY_DN139211_c0_g3_i6       100.000 20      0       0       1       20      1256    1237    0.017   37.4
ef1a_reverse    TRINITY_DN139211_c0_g3_i5       100.000 20      0       0       1       20      453     434     0.017   37.4
ef1a_reverse    TRINITY_DN139211_c0_g3_i4       100.000 20      0       0       1       20      1347    1328    0.017   37.4
ef1a_reverse    TRINITY_DN139211_c0_g3_i3       100.000 20      0       0       1       20      453     434     0.017   37.4
ef1a_reverse    TRINITY_DN139211_c0_g3_i2       100.000 20      0       0       1       20      215     196     0.017   37.4
ef1a_reverse    TRINITY_DN139211_c0_g3_i1       100.000 20      0       0       1       20      188     169     0.017   37.4
vlg1_forward    TRINITY_DN139421_c4_g1_i4       100.000 20      0       0       1       20      1975    1994    0.017   37.4
vlg1_forward    TRINITY_DN139421_c4_g1_i2       100.000 20      0       0       1       20      1975    1994    0.017   37.4
cyp17a1 TRINITY_DN121194_c8_g3_i7       100.000 20      0       0       1       20      1790    1771    0.017   37.4
cyp17a1 TRINITY_DN121194_c8_g3_i6       100.000 20      0       0       1       20      1790    1771    0.017   37.4
cyp17a1 TRINITY_DN121194_c8_g3_i4       100.000 20      0       0       1       20      1798    1779    0.017   37.4
cyp17a1 TRINITY_DN121194_c8_g3_i3       100.000 20      0       0       1       20      417     398     0.017   37.4
cyp17a1 TRINITY_DN121194_c8_g3_i1       100.000 20      0       0       1       20      1790    1771    0.017   37.4
```

## extract the sequence of the aligned transcripts 
The perl script that I wrote will read in the blastn out file, find the transcript names (column 2), and extract the sequences of the transcripts.
```
perl ~/script/extract_sequence.pl xl_pcr_primer_xb_transcriptome_blastn_out.tsv /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/borealis_denovo_oct2018_trinityout.Trinity.fasta 2 > transcript_sequence.fa
```
The path to the sequence file is:
```
/home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/transcript_sequence.fa
```



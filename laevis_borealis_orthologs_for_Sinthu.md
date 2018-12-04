# Finding borealis orthologs for laevis gene primers

## steps - Current, might not be the best way
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
Found out where those transcript mapped to
```
#by blastn
time blastn -task blastn -db /home/xue/genome_data/laevis_genome/db_blastn_laevisGenome/Xl9_2_blastn_db -outfmt 6 -evalue 0.05 -query /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/transcript_sequence.fa -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xb_transcript_sequence_xl_genome_blastout.tsv
#by gmap
```



# Second way to do it
## steps
- [x] make a fasta file with the primer sequences
- [x] blast the primer sequence to the laevis genome blastn database
- [ ] find the orthologs
- [ ] extract the sequence of the ortholog transcript 

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

## blastn
blastn the primer sequence to the laevis xl9_2 genome
```
time blastn -task blastn -db /home/xue/genome_data/laevis_genome/db_blastn_laevisGenome/Xl9_2_blastn_db -outfmt 6 -evalue 0.05 -query /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer.fa -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer_xl_genome_blastn_out.tsv
```
the path to the output file
```
/home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer_xl_genome_blastn_out.tsv
```
the output file
```
ef1a_forward    chr1S   100.000 20      0       0       1       20      172086003       172086022       0.046   37.4
ef1a_forward    Scaffold28      100.000 20      0       0       1       20      946694  946675  0.046   37.4
ef1a_forward    chr5S   100.000 20      0       0       1       20      73756436        73756455        0.046   37.4
ef1a_forward    chr5S   100.000 20      0       0       1       20      79735631        79735612        0.046   37.4
ef1a_reverse    Scaffold28      100.000 20      0       0       1       20      946278  946297  0.046   37.4
ef1a_reverse    chr5S   100.000 20      0       0       1       20      73756840        73756821        0.046   37.4
ef1a_reverse    chr5S   100.000 20      0       0       1       20      79735319        79735338        0.046   37.4
vlg1_forward    chr1L   100.000 20      0       0       1       20      195224567       195224548       0.046   37.4
vlg1_reverse    chr1L   100.000 20      0       0       1       20      195218533       195218552       0.046   37.4
cyp17a1 Scaffold61      100.000 20      0       0       1       20      424102  424083  0.046   37.4
cyp17a1 Scaffold61      100.000 20      0       0       1       20      424029  424048  0.046   37.4
```

## borealise orthologs
borealise transcriptome blastn index
```
/home/xue/borealis_transcriptome/borealis_denovo_transcriptome_august2017/db_borrealis_transcriptome_blastn/db_borrealis_transcriptome_blastn
```
blastn xl gene to borealis
```
time blastn -task blastn -db /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_august2017/db_borrealis_transcriptome_blastn/db_borrealis_transcriptome_blastn -outfmt 6 -evalue 0.05 -query /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_primer_xl_genome_blastn_out_gff_match_sequence.fa -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_gene_xb_transcriptome_blastn_out.tsv
```
extract borealis transcripts that xl gene aligned to 
```
perl ~/script/extract_sequence.pl xl_gene_xb_transcriptome_blastn_out.tsv ~/borealis_transcriptome/borealis_denovo_transcriptome_august2017/trinity_out_dir.Trinity.fasta 2 > /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_gene_xb_transcriptome_blastnOut_xbSeq.fa
```
blastn xl_primer to the extracted borealis transcripts
```
#build index
makeblastdb -in /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_gene_xb_transcriptome_blastnOut_xbSeq.fa -dbtype nucl -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/db_xl_gene_xb_transcriptome_blastnOut_xbSeq_blastn

#blastn
time blastn -task blastn -db /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/db_xl_gene_xb_transcriptome_blastnOut_xbSeq_blastn -outfmt 6 -evalue 0.05 -query /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer.fa -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer_xb_orthTrans_blastn_out.tsv
```
Blast out result
```
ef1a_forward    TRINITY_DN148887_c4_g3_i13      100.000 20      0       0       1       20      112     93      3.99e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i10      100.000 20      0       0       1       20      112     93      3.99e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i9       100.000 20      0       0       1       20      112     93      3.99e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i8       100.000 20      0       0       1       20      112     93      3.99e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i6       100.000 20      0       0       1       20      112     93      3.99e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i5       100.000 20      0       0       1       20      97      78      3.99e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i4       100.000 20      0       0       1       20      49      30      3.99e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i3       100.000 20      0       0       1       20      112     93      3.99e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i2       95.000  20      1       0       1       20      112     93      0.002   31.9
ef1a_reverse    TRINITY_DN148887_c4_g2_i3       100.000 20      0       0       1       20      246     227     3.99e-05        37.4
ef1a_reverse    TRINITY_DN148887_c4_g1_i2       100.000 20      0       0       1       20      236     217     3.99e-05        37.4
ef1a_reverse    TRINITY_DN148887_c4_g1_i1       100.000 20      0       0       1       20      231     212     3.99e-05        37.4
vlg1_forward    TRINITY_DN144511_c3_g1_i12      100.000 20      0       0       1       20      1946    1965    3.99e-05        37.4
vlg1_forward    TRINITY_DN144511_c3_g1_i5       100.000 20      0       0       1       20      2145    2164    3.99e-05        37.4
vlg1_forward    TRINITY_DN144511_c3_g1_i1       100.000 20      0       0       1       20      2316    2335    3.99e-05        37.4
vlg1_forward    TRINITY_DN144511_c3_g1_i17      95.000  20      1       0       1       20      2316    2335    0.002   31.9
vlg1_forward    TRINITY_DN144511_c3_g1_i11      95.000  20      1       0       1       20      1946    1965    0.002   31.9
vlg1_forward    TRINITY_DN144511_c3_g1_i6       95.000  20      1       0       1       20      2145    2164    0.002   31.9
vlg1_forward    TRINITY_DN144511_c3_g1_i3       95.000  20      1       0       1       20      1702    1721    0.002   31.9
cyp17a1 TRINITY_DN118693_c4_g1_i12      100.000 19      0       0       1       19      1839    1857    1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i11      100.000 19      0       0       1       19      1837    1855    1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i9       100.000 19      0       0       1       19      1720    1738    1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i8       100.000 19      0       0       1       19      1839    1857    1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i7       100.000 19      0       0       1       19      1720    1738    1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i6       100.000 19      0       0       1       19      466     484     1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i4       100.000 19      0       0       1       19      347     365     1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i3       100.000 19      0       0       1       19      1720    1738    1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i2       100.000 19      0       0       1       19      1718    1736    1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i1       100.000 19      0       0       1       19      1839    1857    1.39e-04        35.6
cyp17a1 TRINITY_DN118693_c4_g1_i12      100.000 20      0       0       1       20      1912    1893    3.99e-05        37.4
cyp17a1 TRINITY_DN118693_c4_g1_i11      100.000 20      0       0       1       20      1910    1891    3.99e-05        37.4
cyp17a1 TRINITY_DN118693_c4_g1_i9       100.000 20      0       0       1       20      1793    1774    3.99e-05        37.4
cyp17a1 TRINITY_DN118693_c4_g1_i8       100.000 20      0       0       1       20      1912    1893    3.99e-05        37.4
cyp17a1 TRINITY_DN118693_c4_g1_i7       100.000 20      0       0       1       20      1793    1774    3.99e-05        37.4
cyp17a1 TRINITY_DN118693_c4_g1_i6       100.000 20      0       0       1       20      539     520     3.99e-05        37.4
cyp17a1 TRINITY_DN118693_c4_g1_i4       100.000 20      0       0       1       20      420     401     3.99e-05        37.4
cyp17a1 TRINITY_DN118693_c4_g1_i3       100.000 20      0       0       1       20      1793    1774    3.99e-05        37.4
cyp17a1 TRINITY_DN118693_c4_g1_i2       100.000 20      0       0       1       20      1791    1772    3.99e-05        37.4
cyp17a1 TRINITY_DN118693_c4_g1_i1       100.000 20      0       0       1       20      1912    1893    3.99e-05        37.4
```

extract borealis transcript sequences that the primers aligned to
```
perl ~/script/extract_sequence.pl xl_pcr_primer_xb_orthTrans_blastn_out.tsv ~/borealis_transcriptome/borealis_denovo_transcriptome_august2017/trinity_out_dir.Trinity.fasta 2 > xl_pcr_primer_xb_orthTrans_blastn_out_xbSeq.tsv
```

repeat the above with GMAP to double check
```

```




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
>cyp17a1_forward
TGAGTGACAGGAGAATTCTG
>cyp17a1_reverse
CGGTGCTACAGGGCGAATGC
```

## Blastn
To build blastn database for borealise transcriptomes
```
#indexing borealis de novo assembly done in oct 2018 


#indexing borealis de novo assembly done in oct 2018 
makeblastdb -in /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/borealis_denovo_oct2018_trinityout.Trinity.fasta -dbtype nucl -out /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/db_blastn_borealis_denovo_transcriptome_oct2018
```
The path to the blastn database for borealise transcriptomes is 
```
#borealis de novo assembly done in oct 2018 
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
- [x] blast the primer sequence to the laevis genome blastn database
- [ ] find the orthologs
- [ ] extract the sequence of the ortholog transcript 

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
identify the annotation of the xl genomic region that the primers aligned to
```
perl ~/script/identify_aligned_annotated_gene.pl > xl_primer_xl_genome_blastn_out_gff_match.tsv 
```
There are mutiple genes that ef1a aligned to, but we just want the ef1a gene and not other potential genes. Hence, a simple filtering step to select only one that match to what we want. I checked the result, it is good that each pair of forward and reversed aligned to the same anotated gene.
```
awk '$11 ~ /ef1a/||$11~/ddx4/||$11~/cyp17/{print}' xl_primer_xl_genome_blastn_out_gff_match.tsv > xl_primer_xl_genome_blastn_out_gff_exactmatch.tsv
```
Below is the result of the above alignment
```
cyp17a1_Scaffold61_424029_424048  Scaffold61:418534-437428  ID=gene632;Name=cyp17a1
cyp17a1_Scaffold61_424102_424083  Scaffold61:418534-437428  ID=gene632;Name=cyp17a1
ef1a_forward_chr5S_73756436_73756455  chr5S:73752902-73758300 ID=gene3404;Name=eef1a1
ef1a_reverse_chr5S_73756840_73756821  chr5S:73752902-73758300 ID=gene3404;Name=eef1a1
vlg1_forward_chr1L_195224567_195224548  chr1L:195218346-195274156 ID=gene16823;Name=ddx4
vlg1_reverse_chr1L_195218533_195218552  chr1L:195218346-195274156 ID=gene16823;Name=ddx4
```
Next, I extracted the sequence of the genes (exons only). I have a fasta file which contains the transcribed sequence of each gene. The gene file was build with `perl ~/script/gff2fasta_gene_allExons.pl ../XL9_2.fa XENLA_9.2_Xenbase.gff3`.
```
#extract the sequence of the gene
perl ~/script/extract_sequence.pl /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_primer_xl_genome_blastn_out_gff_exactmatch.tsv /home/xue/genome_data/laevis_genome/gff3_xl9_2/XENLA_gene_noIntro.fa  2 > /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_primer_xl_genome_gffGenes_seq.fa
```

## borealise orthologs

borealise transcriptome blastn index
```
/home/xue/borealis_transcriptome/borealis_denovo_transcriptome_august2017/db_borrealis_transcriptome_blastn/db_borrealis_transcriptome_blastn
```
blastn xl gene to borealis
```
time blastn -task blastn -db /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_august2017/db_borrealis_transcriptome_blastn/db_borrealis_transcriptome_blastn -outfmt 6 -evalue 0.05 -query /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_primer_xl_genome_gffGenes_seq.fa -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_gene_xb_transcriptome_blastn_out.tsv
```
extract borealis transcripts that xl gene aligned to 
```
perl ~/script/extract_sequence.pl xl_gene_xb_transcriptome_blastn_out.tsv ~/borealis_transcriptome/borealis_denovo_transcriptome_august2017/trinity_out_dir.Trinity.fasta 2 > /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_gene_xb_transcriptome_blastnOut_xbSeq.fa
```
blastn xl_primer to the extracted borealis transcripts
```
#build index
makeblastdb -in /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_gene_xb_transcriptome_blastnOut_xbSeq.fa -dbtype nucl -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/db_xl_gene_xb_transcriptome_blastnOut_xbSeq_blastn

#blastn
time blastn -task blastn -db /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/db_xl_gene_xb_transcriptome_blastnOut_xbSeq_blastn -outfmt 6 -evalue 0.05 -query /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer.fa -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_pcr_primer_xb_orthTrans_blastn_out.tsv
```
Blast out result
```
ef1a_forward    TRINITY_DN148887_c4_g3_i13      100.000 20      0       0       1       20      112     93      1.87e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i10      100.000 20      0       0       1       20      112     93      1.87e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i9       100.000 20      0       0       1       20      112     93      1.87e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i8       100.000 20      0       0       1       20      112     93      1.87e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i6       100.000 20      0       0       1       20      112     93      1.87e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i5       100.000 20      0       0       1       20      97      78      1.87e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i4       100.000 20      0       0       1       20      49      30      1.87e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i3       100.000 20      0       0       1       20      112     93      1.87e-05        37.4
ef1a_forward    TRINITY_DN148887_c4_g3_i2       95.000  20      1       0       1       20      112     93      7.93e-04        31.9
ef1a_reverse    TRINITY_DN148887_c4_g2_i3       100.000 20      0       0       1       20      246     227     1.87e-05        37.4
ef1a_reverse    TRINITY_DN148887_c4_g1_i2       100.000 20      0       0       1       20      236     217     1.87e-05        37.4
ef1a_reverse    TRINITY_DN148887_c4_g1_i1       100.000 20      0       0       1       20      231     212     1.87e-05        37.4
vlg1_forward    TRINITY_DN144511_c3_g1_i12      100.000 20      0       0       1       20      1946    1965    1.87e-05        37.4
vlg1_forward    TRINITY_DN144511_c3_g1_i5       100.000 20      0       0       1       20      2145    2164    1.87e-05        37.4
vlg1_forward    TRINITY_DN144511_c3_g1_i1       100.000 20      0       0       1       20      2316    2335    1.87e-05        37.4
vlg1_forward    TRINITY_DN144511_c3_g1_i17      95.000  20      1       0       1       20      2316    2335    7.93e-04        31.9
vlg1_forward    TRINITY_DN144511_c3_g1_i11      95.000  20      1       0       1       20      1946    1965    7.93e-04        31.9
vlg1_forward    TRINITY_DN144511_c3_g1_i6       95.000  20      1       0       1       20      2145    2164    7.93e-04        31.9
vlg1_forward    TRINITY_DN144511_c3_g1_i3       95.000  20      1       0       1       20      1702    1721    7.93e-04        31.9
vlg1_reverse    TRINITY_DN104003_c0_g1_i2       100.000 14      0       0       5       18      360     347     0.034   26.5
vlg1_reverse    TRINITY_DN104003_c0_g1_i1       100.000 14      0       0       5       18      370     357     0.034   26.5
cyp17a1_forward TRINITY_DN118693_c4_g1_i12      100.000 19      0       0       1       19      1839    1857    6.51e-05        35.6
cyp17a1_forward TRINITY_DN118693_c4_g1_i11      100.000 19      0       0       1       19      1837    1855    6.51e-05        35.6
cyp17a1_forward TRINITY_DN118693_c4_g1_i9       100.000 19      0       0       1       19      1720    1738    6.51e-05        35.6
cyp17a1_forward TRINITY_DN118693_c4_g1_i8       100.000 19      0       0       1       19      1839    1857    6.51e-05        35.6
cyp17a1_forward TRINITY_DN118693_c4_g1_i7       100.000 19      0       0       1       19      1720    1738    6.51e-05        35.6
cyp17a1_forward TRINITY_DN118693_c4_g1_i6       100.000 19      0       0       1       19      466     484     6.51e-05        35.6
cyp17a1_forward TRINITY_DN118693_c4_g1_i4       100.000 19      0       0       1       19      347     365     6.51e-05        35.6
cyp17a1_forward TRINITY_DN118693_c4_g1_i3       100.000 19      0       0       1       19      1720    1738    6.51e-05        35.6
cyp17a1_forward TRINITY_DN118693_c4_g1_i2       100.000 19      0       0       1       19      1718    1736    6.51e-05        35.6
cyp17a1_forward TRINITY_DN118693_c4_g1_i1       100.000 19      0       0       1       19      1839    1857    6.51e-05        35.6
cyp17a1_reverse TRINITY_DN118693_c4_g1_i12      100.000 20      0       0       1       20      1912    1893    1.87e-05        37.4
cyp17a1_reverse TRINITY_DN118693_c4_g1_i11      100.000 20      0       0       1       20      1910    1891    1.87e-05        37.4
cyp17a1_reverse TRINITY_DN118693_c4_g1_i9       100.000 20      0       0       1       20      1793    1774    1.87e-05        37.4
cyp17a1_reverse TRINITY_DN118693_c4_g1_i8       100.000 20      0       0       1       20      1912    1893    1.87e-05        37.4
cyp17a1_reverse TRINITY_DN118693_c4_g1_i7       100.000 20      0       0       1       20      1793    1774    1.87e-05        37.4
cyp17a1_reverse TRINITY_DN118693_c4_g1_i6       100.000 20      0       0       1       20      539     520     1.87e-05        37.4
cyp17a1_reverse TRINITY_DN118693_c4_g1_i4       100.000 20      0       0       1       20      420     401     1.87e-05        37.4
cyp17a1_reverse TRINITY_DN118693_c4_g1_i3       100.000 20      0       0       1       20      1793    1774    1.87e-05        37.4
cyp17a1_reverse TRINITY_DN118693_c4_g1_i2       100.000 20      0       0       1       20      1791    1772    1.87e-05        37.4
cyp17a1_reverse TRINITY_DN118693_c4_g1_i1       100.000 20      0       0       1       20      1912    1893    1.87e-05        37.4

```

extract borealis transcript sequences that the primers aligned to
```
perl ~/script/extract_sequence.pl /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_pcr_primer_xb_orthTrans_blastn_out.tsv ~/borealis_transcriptome/borealis_denovo_transcriptome_august2017/trinity_out_dir.Trinity.fasta 2 > /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_pcr_primer_xb_orthTrans_blastn_out_xbSeq.tsv
```
**Repeat with GMAP**

repeat the above with GMAP to double check
```bash
#indexing the 3 xl gene
gmap_build -D /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap -s none -d db_xl_3_gffGenes_gmap  /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_primer_xl_genome_gffGenes_seq.fa

#indexing the borealis genome with GMAP
gmap_build -D /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_august2017/db_borrealis_transcriptome_gmap/ -s none -d db_borrealis_transcriptome_gmap  /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_august2017/trinity_out_dir.Trinity.fasta
```

align borealis transcriptome to the xl genes
```bash
#align borealis transcriptome to the xl genes -> didn't find any match
time gmap -d db_xl_3_gffGenes_gmap -D /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap -A -B 5 -t 24 -f samse --cross-species /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_august2017/trinity_out_dir.Trinity.fasta | samtools view -S -b > home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xb_transcriptome_xl_gene_gmap.bam

#align xl gene to borealis transcriptome
time gmap -D /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_august2017/db_borrealis_transcriptome_gmap/ -d db_borrealis_transcriptome_gmap -A -B 5 -t 24 -f samse --cross-species /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_primer_xl_genome_gffGenes_seq.fa > /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_gene_xb_transcriptome_gmap.sam

samtools view -S -b /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_gene_xb_transcriptome_gmap.sam > /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_gene_xb_transcriptome_gmap.bam
```
extract borealis transcripts that xl gene aligned to 
```
perl ~/script/extract_sequence.pl /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_gene_xb_transcriptome_gmap.bam ~/borealis_transcriptome/borealis_denovo_transcriptome_august2017/trinity_out_dir.Trinity.fasta 3 > /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_gene_xb_transcriptome_gmapOut_xbSeq.fa
```
blastn xl_primer to the extracted borealis transcripts
```
#build index
makeblastdb -in /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_gene_xb_transcriptome_gmapOut_xbSeq.fa -dbtype nucl -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/db_xl_gene_xb_transcriptome_gmapOut_xbSeq_blastn

#blastn
time blastn -task blastn -db /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/db_xl_gene_xb_transcriptome_gmapOut_xbSeq_blastn -outfmt 6 -evalue 0.05 -query /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/xl_pcr_primer.fa -out /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_pcr_primer_xb_orthTrans_blastn_out.tsv
```
alignment result
```
ef1a_forward    TRINITY_DN148887_c4_g3_i3       100.000 20      0       0       1       20      112     93      4.97e-07        37.4
ef1a_reverse    TRINITY_DN148887_c4_g2_i3       100.000 20      0       0       1       20      246     227     4.97e-07        37.4
vlg1_forward    TRINITY_DN144511_c3_g1_i12      100.000 20      0       0       1       20      1946    1965    4.97e-07        37.4
cyp17a1_forward TRINITY_DN118693_c4_g1_i8       100.000 19      0       0       1       19      1839    1857    1.73e-06        35.6
cyp17a1_reverse TRINITY_DN118693_c4_g1_i8       100.000 20      0       0       1       20      1912    1893    4.97e-07        37.4
```

extract borealis transcript sequences that the primers aligned to
```
same as xl_gene_xb_transcriptome_gmapOut_xbSeq.fa 
```

# orthologs in X. borealis genome
map the xl gene sequence to the X. borealis genome using GMAP (a splice aware aligner)
```
#indexing the borealis genome
gmap_build -D /home/xue/genome_data/borealis_genome/db_borealis_genome_v1_gmap -s none -g -d db_borealis_genome_v1_gmap  /home/xue/genome_data/borealis_genome/Xbo.v1.fa.gz

time gmap -D /home/xue/genome_data/borealis_genome/db_borealis_genome_v1_gmap -d db_borealis_genome_v1_gmap -A -B 5 -t 24 -f samse --cross-species /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_with_exactmatchOnly/xl_primer_xl_genome_gffGenes_seq.fa > /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_gene_xb_genome_gmap.sam

samtools view -S -b /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_gene_xb_genome_gmap.sam > /home/xue/others_side_project/laevis_primer_borealis_orthologs_sinthu/repeat_withGmap/xl_gene_xb_genome_gmap.bam

bedtools bamtobed -i xl_gene_xb_genome_gmap.bam > xl_gene_xb_genome_gmap.bed
```
extract sequence 
```
#index the borealis genome fasta file
gunzip Xbo.v1.fa.gz

bedtools getfasta -fi ~/genome_data/borealis_genome/Xbo.v1.fa -bed xl_gene_xb_genome_gmap.bed -fo xl_gene_xb_genome_gmap_bed.fa
```



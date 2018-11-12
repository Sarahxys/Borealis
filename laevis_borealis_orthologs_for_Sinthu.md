# Finding borealis orthologs for 3 laevis gene primers
## logic
- [ ] build a build blastn database for borealise transcriptomes
- [ ] make a fasta file with the primer sequences
- [ ] blast the primer sequence to the blastn database


To build blastn database for borealise transcriptomes
```
makeblastdb -in /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/borealis_denovo_oct2018_trinityout.Trinity.fasta -dbtype nucl -out /home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/db_blastn_borealis_denovo_transcriptome_oct2018

```
The path to the blastn database for borealise transcriptomes is 
```
/home/xue/borealis_transcriptome/borealis_denovo_transcriptome_oct2018/db_blastn_borealis_denovo_transcriptome_oct2018
```


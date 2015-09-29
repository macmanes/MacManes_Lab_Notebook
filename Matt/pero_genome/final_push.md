Final Push PEER genome
--


```
blat -noHead P_eremicus.genome.v1.0.1.fasta /mnt/data3/macmanes/reference_assemblies/eremicus/transcriptome/Pero.BLTK.fasta bltk.psl

L_RNA_scaffolder.sh -d /home/macmanes/L_RNA_scaffolder/ -j P_eremicus.genome.v1.0.1.fasta -i bltk.psl -o scaff
```
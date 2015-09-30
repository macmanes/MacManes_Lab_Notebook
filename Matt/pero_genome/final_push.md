Final Push PEER genome
--


```
python /share/BESST_RNA/src/Main.py 1 \
-c $RAID/reference_assemblies/eremicus/genome/jelly.opera.peer.fasta \
-f for.rna.bam -e 3 -T 50000 -k 500 -d 1 -z 1000 -o rna_scaff2

This is P_eremicus.genome.v1.0.1.fasta

blat -noHead P_eremicus.genome.v1.0.1.fasta /mnt/data3/macmanes/reference_assemblies/eremicus/transcriptome/Pero.BLTK.fasta bltk.psl

L_RNA_scaffolder.sh \
-d /home/macmanes/L_RNA_scaffolder/ \
-j P_eremicus.genome.v1.0.1.fasta -i bltk.psl -o scaff2
```
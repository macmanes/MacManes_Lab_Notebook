
PASA Training
==

GMAP version 2015-09-21
PASA 2.02
BLAT v. 35x1

To set up PASA - have to make 

in `/mouse/Mya/maker/pasa`


```
seqclean complete.fa -v /home/macmanes/univec.fa

barrnap Mya.genome.v1.01.fasta --kingdom euk --threads 30
```

Run started 22Sept at 0750

```
/share/PASApipeline-2.0.2/scripts/Launch_PASA_pipeline.pl \
-c alignAssembly.config --ALT_SPLICE \
-C -R -g Mya.genome.v1.01.fasta \
-t complete.fa.clean -T -u complete.fa \
-f FL_accs.txt --ALIGNERS blat,gmap --CPU 30
```

augustus
-

```
/share/augustus-3.1/scripts/gff2gbSmallDNA.pl clam_pasa.pasa_assemblies.gff3 Mya.genome.v1.01.fasta 100 clam.gb


/share/augustus-3.1/scripts/randomSplit.pl clam.gb 100

/share/augustus-3.1/scripts/new_species.pl --species=Mya


etraining --species=Mya clam.gb.train


augustus --species=Mya clam.gb.test | tee firsttest.out

/share/augustus-3.1/scripts/optimize_augustus.pl --species=Mya clam.gb.train

```
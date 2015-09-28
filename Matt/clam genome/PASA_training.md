
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


/share/augustus-3.1/scripts/randomSplit.pl clam.gb 500

/share/augustus-3.1/scripts/new_species.pl --species=Mya


etraining --species= clam.gb.train


augustus --species=Mya.genome.v1.1.1 clam.gb.test | tee 4test.out

/share/augustus-3.1/scripts/optimize_augustus.pl \
--species=clam3 \
--cpus=40 \
--UTR=on \
--chunksize=500000 \
test.gb
```

now

```
perl /share/augustus-3.1/scripts/autoAugTrain.pl \
--species=Mya --trainingset=clam.gb.train --utr \
--estali=est.psl --flanking_DNA=1000 --optrounds=3 \
--genome=Mya.genome.v1.01.fasta


perl /share/augustus-3.1/scripts/autoAugTrain.pl \
--genome=Mya.genome.v1.01.fasta \
--trainingset=clam.gb.train \
--species=clam2

```
Mya Maker Run
--

RepeatModeler

in `/mouse/Mya/maker/repeatmodeler/`

```
BuildDatabase -name Mya_repeats -engine ncbi ../../genome/Mya.genome.v1.1.1.fasta
RepeatModeler -pa 40 -database Mya_repeats

```

in `/mouse/Mya/maker/repeatmodeler/RM_43724.MonOct50629212015`

```
RepeatMasker -lib consensi.fa.classified ../../../genome/Mya.genome.v1.1.1.fasta -pa 40
```

Maker for SNAP training

```
mpirun -np 20 maker -fix_nucleotides
```

Braker1: in `/mouse/Mya/maker`

```
perl /share/braker.pl \
--genome ../genome/Mya.genome.v1.1.1.fasta \
--bam ../genome/transcriptome.clam.v.1.11.bam \
--BAMTOOLS_PATH=/share/bamtools/bin/ \
--UTR on --cores 10 --species=Mya --useexisting
```


rfam_scan in `/mouse/Mya/maker`

```
/usr/local/bin/rfam_scan.pl -blastdb ~/share/rfam/rfam ~/share/rfam/Rfam.cm ../genome/Mya.genome.v1.1.1.fasta
```


#NO CUSTOM REPEATS
```
macmanes@davinci:/mouse/Mya/maker/repeatmodeler$ more Mya.genome.v1.1.1.fasta.tbl
==================================================
file name: Mya.genome.v1.1.1.fasta
sequences:        113420
total length: 1380151942 bp  (1313792958 bp excl N/X-runs)
GC level:         34.98 %
bases masked:   18276198 bp ( 1.32 %)
==================================================
               number of      length   percentage
               elements*    occupied  of sequence
--------------------------------------------------
SINEs:             1720       106510 bp    0.01 %
      ALUs            0            0 bp    0.00 %
      MIRs          939        60099 bp    0.00 %

LINEs:             3186       290855 bp    0.02 %
      LINE1         276        20494 bp    0.00 %
      LINE2         753        78608 bp    0.01 %
      L3/CR1       1638       155274 bp    0.01 %

LTR elements:       526       128480 bp    0.01 %
      ERVL           42         3613 bp    0.00 %
      ERVL-MaLRs      5          355 bp    0.00 %
      ERV_classI    152        13350 bp    0.00 %
      ERV_classII    21         1308 bp    0.00 %

DNA elements:      4534       302759 bp    0.02 %
     hAT-Charlie    172        12055 bp    0.00 %
     TcMar-Tigger  3479       231429 bp    0.02 %

Unclassified:       209        14884 bp    0.00 %

Total interspersed repeats:   843488 bp    0.06 %


Small RNA:         4573       331266 bp    0.02 %

Satellites:          64        10085 bp    0.00 %
Simple repeats:  282859     15277877 bp    1.11 %
Low complexity:   37698      1818631 bp    0.13 %
==================================================

* most repeats fragmented by insertions or deletions
  have been counted as one element


The query species was assumed to be homo sapiens
RepeatMasker version open-4.0.5 , default mode

run with rmblastn version 2.2.27+
RepBase Update 20140131, RM database version 20140131
```

#YES CUSTOM REPEATS
```
macmanes@davinci:/mouse/Mya/maker/repeatmodeler/RM_43724.MonOct50629212015$ more Mya.genome.v1.1.1.fasta.tbl
==================================================
file name: Mya.genome.v1.1.1.fasta
sequences:        113420
total length: 1380151942 bp  (1313792958 bp excl N/X-runs)
GC level:         34.98 %
bases masked:  395611112 bp ( 28.66 %)
==================================================
               number of      length   percentage
               elements*    occupied  of sequence
--------------------------------------------------
SINEs:            71668     12202907 bp    0.88 %
      ALUs            0            0 bp    0.00 %
      MIRs            0            0 bp    0.00 %

LINEs:            64505     23844606 bp    1.73 %
      LINE1         839       518509 bp    0.04 %
      LINE2        6544      2660694 bp    0.19 %
      L3/CR1       3641       832083 bp    0.06 %

LTR elements:     23824      6268915 bp    0.45 %
      ERVL            0            0 bp    0.00 %
      ERVL-MaLRs      0            0 bp    0.00 %
      ERV_classI      0            0 bp    0.00 %
      ERV_classII     0            0 bp    0.00 %

DNA elements:    174248     37555006 bp    2.72 %
     hAT-Charlie      0            0 bp    0.00 %
     TcMar-Tigger     0            0 bp    0.00 %

Unclassified:    1379515    301887369 bp   21.87 %

Total interspersed repeats:381758803 bp   27.66 %


Small RNA:         4744       857307 bp    0.06 %

Satellites:        1493       478440 bp    0.03 %
Simple repeats:  207133     12528067 bp    0.91 %
Low complexity:   24948      1234916 bp    0.09 %
==================================================

* most repeats fragmented by insertions or deletions
  have been counted as one element


The query species was assumed to be homo
RepeatMasker version open-4.0.5 , default mode

run with rmblastn version 2.2.27+
The query was compared to classified sequences in "consensi.fa.classified"
RepBase Update 20140131, RM database version 20140131
```
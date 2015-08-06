Analysis of potential DNA contamination in non-DNAse treated samples.

in `/mnt/data3/macmanes/NYGC_August2015/contam`

```
java -Xmx50g -jar \
/share/trinityrnaseq/trinity-plugins/Trimmomatic/trimmomatic-0.32.jar PE \
-threads 8 \
-baseout 2329-Kidney.fastQ \
2329-Kidney_ACAGTG_BC6PR5ANXX_L008_001.R1.fastq.gz \
2329-Kidney_ACAGTG_BC6PR5ANXX_L008_001.R2.fastq.gz \
ILLUMINACLIP:/mnt/data3/macmanes/subsamp/barcodes.fa:2:30:1
```

bwa mapping

```
bwa index -p pero Pero.BLTK.fasta

bwa mem -t20 pero  2329-Kidney.fastQ_1P 2329-Kidney.fastQ_2P | samtools view -@6 -Sub - > 2329.bam

bwa mem -t 6 pero  376.testes_1P.fq 376.testes_2P.fq | samtools view -@6 -Sub - > 376.bam


```

Greater than 85% of reads map to reference transcriptome (Pero.BLTK.fasta), so I think DNAse treatment is no longer a thing.. 
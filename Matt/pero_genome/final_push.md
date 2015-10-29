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

```
version=peer.v1.03
fasta=P_eremicus.genome.v1.0.1.fasta

bwa index -p $version $fasta &


python3 /share/BUSCO_v1.1b1/BUSCO_v1.1b1.py -o peer.genome.$version -in $fasta -l vertebrata -m genome -c 30 --long

	
time seqtk mergepe \
$RAID/pero_annotation/Pero360K.1.fastq.gz \
$RAID/pero_annotation/Pero360K.2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 30 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.kidney.bam -


time seqtk mergepe \
$RAID/pero_annotation/Pero360B.1.fastq.gz \
$RAID/pero_annotation/Pero360B.2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 30 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.brain.bam -

time seqtk mergepe \
$RAID/pero_annotation/Pero360T.1.fastq.gz \
$RAID/pero_annotation/Pero360T.2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.testes.bam -

time seqtk mergepe \
$RAID/pero_annotation/Pero2926.1.fastq.gz \
$RAID/pero_annotation/Pero2926.2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.2926.bam -


time seqtk mergepe \
$RAID/pero_pigeons_ladybugs/2336a.trim_1P.fq.gz \
$RAID/pero_pigeons_ladybugs/2336a.trim_2P.fq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.2326.bam -

time seqtk mergepe \
$RAID/NYGC_pero/2355K.R1.fastq.gz \
$RAID/NYGC_pero/2355K.R2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.2355.bam -

time seqtk mergepe \
$RAID/NYGC_pero/2341K.R1.fastq.gz \
$RAID/NYGC_pero/2341K.R2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.2341.bam -

time seqtk mergepe \
$RAID/NYGC_pero/2335K.R1.fastq.gz \
$RAID/NYGC_pero/2335K.R2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.2335.bam -

time seqtk mergepe \
$RAID/NYGC_August2015/raw_data/3333-testes_GTTTCG_BC6PR5ANXX_L008_001.R1.fastq.gz \
$RAID/NYGC_August2015/raw_data/3333-testes_GTTTCG_BC6PR5ANXX_L008_001.R2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.3333.bam -

time seqtk mergepe \
$RAID/NYGC_August2015/raw_data/349-testes_ACTGAT_BC6PR5ANXX_L008_001.R1.fastq.gz \
$RAID/NYGC_August2015/raw_data/349-testes_ACTGAT_BC6PR5ANXX_L008_001.R2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.349.bam -


time seqtk mergepe \
$RAID/NYGC_August2015/raw_data/376-testes_CGTACG_BC6PR5ANXX_L008_001.R1.fastq.gz \
$RAID/NYGC_August2015/raw_data/376-testes_CGTACG_BC6PR5ANXX_L008_001.R2.fastq.gz \
| skewer -Q 2 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 $version - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o $version.376.bam -

samtools merge $version.rna.bam *bam
```

Blat in 1.0.3
map to 1.0.3
Busco to 1.0.3

--> get list, kill junk contigs --> rename contigs.
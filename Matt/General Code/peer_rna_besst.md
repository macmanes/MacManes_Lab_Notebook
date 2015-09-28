RNA_BESST
--


```
time interleave-reads.py \
$RAID/pero_annotation/Pero360L.1.fastq.gz \
$RAID/pero_annotation/Pero360L.2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o liver.bam -

time interleave-reads.py \
$RAID/pero_annotation/Pero360K.1.fastq.gz \
$RAID/pero_annotation/Pero360K.2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o kidney.bam -


time interleave-reads.py \
$RAID/pero_annotation/Pero360B.1.fastq.gz \
$RAID/pero_annotation/Pero360B.2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o brain.bam -

time interleave-reads.py \
$RAID/pero_annotation/Pero360T.1.fastq.gz \
$RAID/pero_annotation/Pero360T.2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o testes.bam -

time interleave-reads.py \
$RAID/pero_annotation/Pero2926.1.fastq.gz \
$RAID/pero_annotation/Pero2926.2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o 2926.bam -


time interleave-reads.py \
$RAID/pero_pigeons_ladybugs/2336a.trim_1P.fq.gz \
$RAID/pero_pigeons_ladybugs/2336a.trim_2P.fq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o 2326.bam -

time interleave-reads.py \
$RAID/NYGC_pero/2355K.R1.fastq.gz \
$RAID/NYGC_pero/2355K.R2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o 2355.bam -

time interleave-reads.py \
$RAID/NYGC_pero/2341K.R1.fastq.gz \
$RAID/NYGC_pero/2341K.R2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o 2341.bam -

time interleave-reads.py \
$RAID/NYGC_pero/2335K.R1.fastq.gz \
$RAID/NYGC_pero/2335K.R2fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o 2335.bam -

time interleave-reads.py \
$RAID/NYGC_August2015/raw_data/3333-testes_GTTTCG_BC6PR5ANXX_L008_001.R1.fastq.gz \
$RAID/NYGC_August2015/raw_data/3333-testes_GTTTCG_BC6PR5ANXX_L008_001.R2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o 3333.bam -

time interleave-reads.py \
$RAID/NYGC_August2015/raw_data/349-testes_ACTGAT_BC6PR5ANXX_L008_001.R1.fastq.gz \
$RAID/NYGC_August2015/raw_data/349-testes_ACTGAT_BC6PR5ANXX_L008_001.R2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o 349.bam -


time interleave-reads.py \
$RAID/NYGC_August2015/raw_data/376-testes_CGTACG_BC6PR5ANXX_L008_001.R1.fastq.gz \
$RAID/NYGC_August2015/raw_data/376-testes_CGTACG_BC6PR5ANXX_L008_001.R2.fastq.gz \
| skewer -Q 2 -t 10 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 40 peer - \
| samtools view -T . -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 15 -m 22G -o 376.bam -
























```

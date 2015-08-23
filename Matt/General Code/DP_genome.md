DP_genome


in `thomas2/matt-test`

```

sed 's_ 3:_ 2:_g' R3.fq > R2.fq

interleave-reads.py R1.fq R2.fq \
| load-into-countgraph.py --threads 20 --ksize 32 -M 8e10 count.kh -

```


```
java -Xmx10g -jar /opt/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
-threads 8 -baseout dp.Phred5.fq \
R1.fq \
R1.fq \
ILLUMINACLIP:/opt/Trimmomatic-0.32/adapters/TruSeq3-PE.fa:2:30:10 \
SLIDINGWINDOW:4:5 \
LEADING:5 \
TRAILING:5 \
MINLEN:50

Input Read Pairs: 180900324 Both Surviving: 180644382 (99.86%) Forward Only Surviving: 4944 (0.00%) Reverse Only Surviving: 0 (0.00%) Dropped: 250998 (0.14%)

```

**FastqToSam.jar**

```

java -Xmx50g -jar /opt/picard-tools-1.119/FastqToSam.jar \
FASTQ=dp.Phred5_1P.fq \
FASTQ2=dp.Phred5_2P.fq \
OUTPUT=dp.P2.bam SAMPLE_NAME=dp_genome

```

Discovar

```
/opt/discovardenovo-52488/src/DiscovarDeNovo NUM_THREADS=20 \
OUT_DIR=genome READS=dp.P2.bam

```

Discovar not bad...

try khmer instead of trimming
--

```
interleave-reads.py R1.fq R2.fq | normalize-by-median.py --max-memory-usage 8e10 -C 30 -o -  - | trim-low-abund.py -M 8e10 -o dp.2pass.fq --cutoff 2 -
```


busco
--

```
python3 /home/macmanes/BUSCO_v1.1b1/BUSCO_v1.1b1.py \
-m genome -in /thomas2/matt_test/genome/a.final/a.lines.fasta \
--cpu 16 -l metazoa -o dp_genome
```
Mya genome
--

bfc v181
khmer version 1.4.1
screed 0.8
NextClip v1.3
Trimmomatic-0.32


in `/mouse/Mya`

for NYGC PE reads

	interleave-reads.py \
	clam-no-leukemia_ATTACTCG_AC730GANXX_L003_001.R1.fastq.gz \
	clam-no-leukemia_ATTACTCG_AC730GANXX_L003_001.R2.fastq.gz -o inter
	
	bfc -s 800m -k 55 -t 16 inter.fq
	
	

and

    java -Xmx50g -jar \
    /share/trinityrnaseq/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 24 -baseout clam500.P2.fq.gz \
    clam-no-leukemia_ATTACTCG_AC730GANXX_L003_001.R1.fastq.gz \
    clam-no-leukemia_ATTACTCG_AC730GANXX_L003_001.R2.fastq.gz  \
    ILLUMINACLIP:/share/trinityrnaseq/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 \
    LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:50
    
	Input Read Pairs: 299805502 Both Surviving: 297619937 (99.27%) Forward Only Surviving: 1956415 (0.65%) Reverse Only Surviving: 202488 (0.07%) Dropped: 26662 (0.01%)


for hcgs PE reads

    java -Xmx50g -jar \
    /share/trinityrnaseq/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 24 -baseout clam300.P2.fq.gz \
    mya.corr.trim.1.fq \
    mya.corr.trim.2.fq  \
    ILLUMINACLIP:/share/trinityrnaseq/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 \
    LEADING:5 TRAILING:5 SLIDINGWINDOW:4:5 MINLEN:50
    
	Input Read Pairs: 490889174 Both Surviving: 480446743 (97.87%) Forward Only Surviving: 7473313 (1.52%) Reverse Only Surviving: 2492373 (0.51%) Dropped: 476745 (0.10%)
    




for NYGC MP reads

	nextclip \
	-i <(gzip -cd clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R1.fastq.gz) \
	-j <(gzip -cd clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R2.fastq.gz) \
	-o clam5kb -e -n 100000000


results

```
  R1 Num reads with adaptor: 91760936  30.50 %
   R1 Num with external also: 581850    0.19 %
       R1 long adaptor reads: 65248485  21.69 %
          R1 reads too short: 26512451  8.81 %
     R1 Num reads no adaptor: 209075227 69.50 %
  R1 no adaptor but external: 3936342   1.31 %

   R2 Num reads with adaptor: 92223735  30.66 %
   R2 Num with external also: 602646    0.20 %
       R2 long adaptor reads: 65304747  21.71 %
          R2 reads too short: 26918988  8.95 %
     R2 Num reads no adaptor: 208612428 69.34 %
  R2 no adaptor but external: 3880213   1.29 %

   Total pairs in category A: 2485200   0.83 %
         A pairs long enough: 1380135   0.46 %
           A pairs too short: 1105065   0.37 %
A external clip in 1 or both: 256       0.00 %
     A bases before clipping: 621300000
       A total bases written: 181358858

   Total pairs in category B: 89719982  29.82 %
         B pairs long enough: 63436419  21.09 %
           B pairs too short: 26283563  8.74 %
B external clip in 1 or both: 80995     0.03 %
     B bases before clipping: 22429995500
       B total bases written: 10776428586

   Total pairs in category C: 89259017  29.67 %
         C pairs long enough: 63350400  21.06 %
           C pairs too short: 25908617  8.61 %
C external clip in 1 or both: 59642     0.02 %
     C bases before clipping: 22314754250
       C total bases written: 10771139127

   Total pairs in category D: 119336692 39.67 %
         D pairs long enough: 115443373 38.37 %
           D pairs too short: 3893319   1.29 %
D external clip in 1 or both: 3921559   1.30 %
     D bases before clipping: 29834173000
       D total bases written: 24471688504

   Total pairs in category E: 35272     0.01 %
         E pairs long enough: 23090     0.01 %
           E pairs too short: 12182     0.00 %
E external clip in 1 or both: 1797      0.00 %
     E bases before clipping: 8818000
       E total bases written: 3554894

          Total usable pairs: 128190044 42.61 %
             All long enough: 243633417 80.99 %
    All categories too short: 57202746  19.01 %
      Duplicates not written: 0 0.00 %

         Category B became E: 18553     0.01 %
         Category C became E: 16719     0.01 %
          Overall GC content: 36.01 %


```

and

	nextclip \
	-i <(gzip -cd clam-no-leukemia-MP-10k_CGATGTAT_BC7A4MANXX_L002_001.R1.fastq.gz) \
	-j <(gzip -cd clam-no-leukemia-MP-10k_CGATGTAT_BC7A4MANXX_L002_001.R2.fastq.gz) \
	-o clam10kb -e -n 100000000
	
```
   R1 Num reads with adaptor: 102899211 31.96 %
   R1 Num with external also: 1631325   0.51 %
       R1 long adaptor reads: 73336848  22.78 %
          R1 reads too short: 29562363  9.18 %
     R1 Num reads no adaptor: 219042464 68.04 %
  R1 no adaptor but external: 6389558   1.98 %

   R2 Num reads with adaptor: 103984222 32.30 %
   R2 Num with external also: 1666121   0.52 %
       R2 long adaptor reads: 73627558  22.87 %
          R2 reads too short: 30356664  9.43 %
     R2 Num reads no adaptor: 217957453 67.70 %
  R2 no adaptor but external: 6183778   1.92 %

   Total pairs in category A: 7236074   2.25 %
         A pairs long enough: 3950112   1.23 %
           A pairs too short: 3285962   1.02 %
A external clip in 1 or both: 1028      0.00 %
     A bases before clipping: 1809018500
       A total bases written: 510981547

   Total pairs in category B: 96690386  30.03 %
         B pairs long enough: 68226444  21.19 %
           B pairs too short: 28463942  8.84 %
B external clip in 1 or both: 139223    0.04 %
     B bases before clipping: 24172596500
       B total bases written: 11573932315

   Total pairs in category C: 95616000  29.70 %
         C pairs long enough: 67831184  21.07 %
           C pairs too short: 27784816  8.63 %
C external clip in 1 or both: 101248    0.03 %
     C bases before clipping: 23904000000
       C total bases written: 11517315604

   Total pairs in category D: 122294316 37.99 %
         D pairs long enough: 116020126 36.04 %
           D pairs too short: 6274190   1.95 %
D external clip in 1 or both: 6346730   1.97 %
     D bases before clipping: 30573579000
       D total bases written: 24590341276

   Total pairs in category E: 104899    0.03 %
         E pairs long enough: 65557     0.02 %
           E pairs too short: 39342     0.01 %
E external clip in 1 or both: 6972      0.00 %
     E bases before clipping: 26224750
       E total bases written: 9853543

          Total usable pairs: 140073297 43.51 %
             All long enough: 256093423 79.55 %
    All categories too short: 65848252  20.45 %
      Duplicates not written: 0 0.00 %

         Category B became E: 57762     0.02 %
         Category C became E: 47137     0.01 %
          Overall GC content: 36.10 %


Done. Completed in 40445 seconds.
```



ALLPATHS
--

in_groups.csv

```
file_name, library_name, group_name  
/mouse/Mya/hcgs_reads/pe/clam300.P2_*P.fq,L1,      frags1  
/mouse/Mya/nygc_reads/pe/clam500.P2_*P.fq,L2,      frags2  
/mouse/Mya/nygc_reads/mp/clam5kb_*.fastq,5kb,      jumps5  
/mouse/Mya/nygc_reads/mp/clam10kb_*.fastq,10kb,      jumps10  

```

in_libs.csv

```
library_name, project_name, organism_name,     type, paired, frag_size, frag_stddev, insert_size, insert_stddev, read_orientation, genomic_start, genomic_end
L1,mya_v1,mya, fragment,1,300,50,            ,              ,           inward,0,0
L2,mya_v1,mya, fragment,1,550,50,            ,              ,           inward,0,0
5kb,mya_v1,mya,  jumping,1,          ,            ,5000,500,          outward,0,0
10kb,mya_v1,mya,  jumping,1,          ,            ,10000,1000,          outward,0,0

```

PreprareInputs

```
/usr/local/bin/PrepareAllPathsInputs.pl \
DATA_DIR=/mouse/Mya/allpaths/v1/ \
GENOME_SIZE=1000000000 OVERWRITE=True PLOIDY=2 \
HOSTS=30 \
TMP_DIR=/mouse \
JAVA_MEM_GB=100 | tee prepare.out
```

RunAllp

```
RunAllPathsLG THREADS=40 FIX_ASSEMBLY_BASE_ERRORS=TRUE \
PRE=/mouse/Mya/allpaths/ \
DATA_SUBDIR=v1 \
RUN=mya_v1 \
REFERENCE_NAME=clam \
TARGETS=standard \
CONNECT_SCAFFOLDS=TRUE HAPLOIDIFY=TRUE | tee assembly.out

```


ABYSS
--

./configure --enable-maxk=128 --prefix=/share/ --with-mpi=/usr/lib/openmpi/

	export TMPDIR=/mnt/data0/   


    split -l 156000000 --additional-suffix=aaa <(zcat /mouse/Mya/hcgs_reads/pe/clam300.P2_*P.fq.gz) &
    split -l 156000000 --additional-suffix=zzz <(zcat /mouse/Mya/nygc_reads/pe/clam500.P2_*P.fq.gz) &
    
    for k in 61 81 71; do
        mkdir /mouse/Mya/abyss/k$k
        cd /mouse/Mya/abyss/k$k
        mpirun -np 42 ABYSS-P -v -k$k \
        --coverage-hist=coverage.hist \
        -o Mya$k-1.fa /mouse/Mya/split/* |& tee $k_assembly.out;
    done




    for k in 71 81 61; do
        abyss-pe -C k$k np=40 k=$k name=Mya$k l=25 n=5 \
        lib='pe1 pe2' mp1_l=25 mp2_l=25 \
        mp='mp1 mp2' long='long1 long2' v=-vv \
        pe1='/mouse/Mya/hcgs_reads/pe/clam300.P2_1P.fq.gz /mouse/Mya/hcgs_reads/pe/clam300.P2_2P.fq.gz' \
        pe2='/mouse/Mya/nygc_reads/pe/clam500.P2_1P.fq.gz /mouse/Mya/nygc_reads/pe/clam500.P2_2P.fq.gz' \
        mp1='/mouse/Mya/nygc_reads/mp/clam5kb_1.fastq /mouse/Mya/nygc_reads/mp/clam5kb_2.fastq' \
        mp2='/mouse/Mya/nygc_reads/mp/clam10kb_1.fastq /mouse/Mya/nygc_reads/mp/clam10kb_2.fastq' \
        long1='/mouse/Mya/output_lsc/corrected_LR.fa' \
        long2='/mnt/data3/macmanes/Mya/clam.Trinity.fasta' |& tee k$kassembly.out;
    done  


    for k in 61; do
        abyss-pe -C k$k np=40 k=$k name=Mya$k l=25 n=5 \
        lib='pe1 pe2' mp1_l=25 mp2_l=25 aligner=bwa \
        mp='mp1 mp2' long='long1 long2' \
        pe1='/mouse/Mya/hcgs_reads/pe/clam300.P2_1P.fq.gz /mouse/Mya/hcgs_reads/pe/clam300.P2_2P.fq.gz' \
        pe2='/mouse/Mya/nygc_reads/pe/clam500.P2_1P.fq.gz /mouse/Mya/nygc_reads/pe/clam500.P2_2P.fq.gz' \
        mp1='/mouse/Mya/nygc_reads/mp/clam5kb_1.fastq /mouse/Mya/nygc_reads/mp/clam5kb_2.fastq' \
        mp2='/mouse/Mya/nygc_reads/mp/clam10kb_1.fastq /mouse/Mya/nygc_reads/mp/clam10kb_2.fastq' \
        long1='/mouse/Mya/output_lsc/corrected_LR.fa' \
        long2='/mnt/data3/macmanes/Mya/clam.Trinity.fasta' |& tee $kassembly.out;
    done  



masurca
--

```
DATA  
PE= aa 550 50 /mouse/Mya/nygc_reads/pe/clam500.P2_1P.fq.gz /mouse/Mya/nygc_reads/pe/clam500.P2_2P.fq.gz  
PE= ab 300 40 /mouse/Mya/hcgs_reads/pe/clam300.P2_1P.fq.gz /mouse/Mya/hcgs_reads/pe/clam300.P2_2P.fq.gz   
JUMP= af 7000 600 mouse/Mya/nygc_reads/mp/clam5kb_1.fastq /mouse/Mya/nygc_reads/mp/clam5kb_2.fastq  
JUMP= ac 6000 600 /mouse/Mya/nygc_reads/mp/clam10kb_1.fastq /mouse/Mya/nygc_reads/mp/clam10kb_2.fastq   
OTHER=clam.pacbio.frg  
END  

PARAMETERS
SOAP_ASSEMBLY=1
GRAPH_KMER_SIZE = auto  
USE_LINKING_MATES = 1  
LIMIT_JUMP_COVERAGE = 300  
CA_PARAMETERS = cgwErrorRate=0.15
KMER_COUNT_THRESHOLD = 2  
NUM_THREADS = 40  
JF_SIZE = 16244928491  
DO_HOMOPOLYMER_TRIM = 0  
END  
```





PBcR
--

```
PBcR -l Mya -s config ---length 1000 -t 20 -pbCNS \
-fastq clam.longreads.fastq \
```

runCA
--

```
runCA -p Mya_asm -d Mya_asm -s config tempMya/Mya.frg 
```



BUSCO
--

in `/mouse/Mya/assemblies/long`

```
for i in $(ls *fa); do F=$(basename $i .fa); python3 /share/BUSCO_v1.1b1/BUSCO_v1.1b1.py -o $F -in $i -l metazoa -m genome -c 20; done

for i in $(ls *fa); do F=$(basename $i .fa); python3 /share/BUSCO_v1.1b1/BUSCO_v1.1b1.py -f -o $F -in $i -l eukaryota -m genome -c 20; 
done


```


ABYSS with 2pass PE reads
--

```
export TMPDIR=/mnt/data0/   


split -l 156000000 --additional-suffix=aaa <(zcat /mouse/Mya/hcgs_reads/pe/clam300.2pass.fq.gz) &
split -l 156000000 --additional-suffix=zzz <(zcat /mouse/Mya/nygc_reads/pe/clam500.2pass.fq.gz) &



for k in 109 97 91 61 81 71; do
    mkdir /mouse/Mya/abyss-khmer/k$k
    cd /mouse/Mya/abyss-khmer/k$k
    mpirun -np 42 ABYSS-P -v -k$k \
    --coverage-hist=coverage.hist \
    -o Mya$k-1.fa /mouse/Mya/split/*zzz | tee $k_assembly.out;
done


for k in 71 81 61; do
    abyss-pe -C k$k np=40 k=$k name=Mya$k l=25 n=5 \
    lib='pe2' mp1_l=25 mp2_l=25 \
    mp='mp1 mp2' long='long1 long2' v=-vv \
    pe2='/mouse/Mya/nygc_reads/pe/clam500.2pass.fq.gz' \
    mp1='/mouse/Mya/nygc_reads/mp/clam5kb_1.fastq /mouse/Mya/nygc_reads/mp/clam5kb_2.fastq' \
    mp2='/mouse/Mya/nygc_reads/mp/clam10kb_1.fastq /mouse/Mya/nygc_reads/mp/clam10kb_2.fastq' \
    long1='/mouse/Mya/output_lsc/corrected_LR.fa' \
    long2='/mnt/data3/macmanes/Mya/clam.Trinity.fasta' |& tee k$kassembly.out;
done  

```

PBJelly
--

in `/mouse/Mya/blasr`

```
Jelly.py setup Protocol.xml
Jelly.py mapping Protocol.xml
Jelly.py support Protocol.xml -x "--minMapqv=100"
Jelly.py extraction Protocol.xml
Jelly.py assembly Protocol.xml -x "--nproc=40"
Jelly.py output Protocol.xml



```

     > Jelly.py <stage> yourProtocol.xml

<<<<<<< Updated upstream
picking khmer k81
=================

```
for k in 81; do
    /mouse/Mya/abyss-khmer/k97/new/abyss-pe.pacbio -C k$k np=40 k=$k name=Mya$k l=25 n=5 \
    lib='pe1 pe2' mp1_l=50 mp2_l=50 pacbio='long1' \
    mp='mp1 mp2' long='long2' \
    pe1='/mouse/Mya/hcgs_reads/pe/clam300.P2_1P.fq.gz /mouse/Mya/hcgs_reads/pe/clam300.P2_2P.fq.gz' \
    pe2='/mouse/Mya/nygc_reads/pe/clam500.P2_1P.fq.gz /mouse/Mya/nygc_reads/pe/clam500.P2_2P.fq.gz' \
    mp1='/mouse/Mya/nygc_reads/mp/clam5kb_1.fastq /mouse/Mya/nygc_reads/mp/clam5kb_2.fastq' \
    mp2='/mouse/Mya/nygc_reads/mp/clam10kb_1.fastq /mouse/Mya/nygc_reads/mp/clam10kb_2.fastq' \
    long1='/mouse/Mya/output_lsc/corrected_LR.fa' \
    long2='/mnt/data3/macmanes/Mya/clam.Trinity.fasta' | tee $kassembly.out;
done
```

opera
--

```
perl /share/opera_v2.0.2/bin/preprocess_reads.pl \
Mya81-contigs.fa \
/mouse/Mya/hcgs_reads/pe/clam300.P2_1P.fq.gz /mouse/Mya/hcgs_reads/pe/clam300.P2_2P.fq.gz \
lib_300.map

perl /share/opera_v2.0.2/bin/preprocess_reads.pl \
Mya81-contigs.fa \
/mouse/Mya/nygc_reads/pe/clam500.P2_1P.fq.gz /mouse/Mya/nygc_reads/pe/clam500.P2_2P.fq.gz \
lib_500.map

perl /share/opera_v2.0.2/bin/preprocess_reads.pl \
Mya81-contigs.fa \
/mouse/Mya/nygc_reads/mp/clam5kb_1.fastq /mouse/Mya/nygc_reads/mp/clam5kb_2.fastq \
lib_5kb.map

perl /share/opera_v2.0.2/bin/preprocess_reads.pl \
Mya81-contigs.fa \
/mouse/Mya/nygc_reads/mp/clam10kb_1.fastq /mouse/Mya/nygc_reads/mp/clam10kb_2.fastq \
lib_10kb.map

```
and

```
/share/opera_v2.0.1/bin/opera Mya81-contigs.fa \
lib_300.map lib_500.map lib_5kb.map lib_10kb.map \
opera_results
```

opera taking too long, also, see BESST paper

besst
--

```

interleave-reads.py \
/mouse/Mya/nygc_reads/mp/clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R1.fastq.gz \
/mouse/Mya/nygc_reads/mp/clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R2.fastq.gz \
| skewer -Q 5 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 30 Mya81-contigs.fa - \
| samtools view -Sb - \
| samtools sort -@ 10 -m 20G - clam.5kb


interleave-reads.py \
/mouse/Mya/nygc_reads/mp/clam-no-leukemia-MP-10k_CGATGTAT_BC7A4MANXX_L002_001.R1.fastq.gz \
/mouse/Mya/nygc_reads/mp/clam-no-leukemia-MP-10k_CGATGTAT_BC7A4MANXX_L002_001.R2.fastq.gz \
| skewer -Q 5 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 30 Mya81-contigs.fa - \
| samtools view -Sb - \
| samtools sort -@ 10 -m 20G - clam.10kb


interleave-reads.py \
/mnt/data3/macmanes/Mya/nygc_reads/raw_reads/clam-no-leukemia_ATTACTCG_AC730GANXX_L003_001.R1.fastq.gz \
/mnt/data3/macmanes/Mya/nygc_reads/raw_reads/clam-no-leukemia_ATTACTCG_AC730GANXX_L003_002.R1.fastq.gz \
| skewer -Q 5 -t 20 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 30 Mya81-contigs.fa - \
| samtools view -Sb - \
| samtools sort -@ 10 -m 20G - clam.500


samtools index clam.5kb.bam
samtools index clam.10kb.bam
samtools index clam.500.bam


/share/BESST/runBESST -c Mya81-contigs.fa -f clam.500.bam clam.5kb.bam clam.10kb.bam -o /mouse/Mya/besst --orientation fr rf rf


```






























=======
     The stages, in order, and their descriptions are
       1. setup       Tag sequence names, find gaps, and index the reference
       2. mapping     Use blasr to map the sequences to the reference
       3. support     Identify which reads support which gaps
       4. extraction  For each gap, consolidate all reads supporting it into a local-assembly folder.
       5. assembly    Build the consensus gap-filling sequence
       6. output      Stitch the reference sequences and gap-fillling sequences together
>>>>>>> Stashed changes

BESST on PBJelly
--

```
time interleave-reads.py \
/mouse/Mya/nygc_reads/mp/clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R1.fastq.gz \
/mouse/Mya/nygc_reads/mp/clam-no-leukemia-MP-5k_CGATGTAT_BC7A4MANXX_L001_001.R2.fastq.gz \
| skewer -Q 5 -t 8 -x $SCRATCH/adapters.fa - -1 \
| bwa mem -p -t 30 jelly - \
| samtools view -T . -F4 -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 8 -m 22G -o jelly.clam.5kb.bam -


time interleave-reads.py \
/mouse/Mya/nygc_reads/mp/clam-no-leukemia-MP-10k_CGATGTAT_BC7A4MANXX_L002_001.R1.fastq.gz \
/mouse/Mya/nygc_reads/mp/clam-no-leukemia-MP-10k_CGATGTAT_BC7A4MANXX_L002_001.R2.fastq.gz \
| skewer -Q 5 -t 8 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 30 jelly - \
| samtools view -T . -F4 -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 8 -m 22G -o jelly.clam.10kb.bam -


time interleave-reads.py \
/mnt/data3/macmanes/Mya/nygc_reads/raw_reads/clam-no-leukemia_ATTACTCG_AC730GANXX_L003_001.R1.fastq.gz \
/mnt/data3/macmanes/Mya/nygc_reads/raw_reads/clam-no-leukemia_ATTACTCG_AC730GANXX_L003_001.R2.fastq.gz \
| skewer -Q 5 -t 8 -x $SCRATCH/adapters.fa - -1 \
| extract-paired-reads.py -p - -s /dev/null - \
| bwa mem -p -t 30 jelly - \
| samtools view -T . -F4 -bu - \
| samtools sort -l 0 -O bam -T tmp -@ 8 -m 22G -o jelly.clam.500.bam -


samtools index jelly.clam.5kb.bam
samtools index jelly.clam.10kb.bam
samtools index jelly.clam.500.bam



/share/BESST/runBESST -c Mya81-contigs.fa \
-f jelly.clam.500.bam jelly.clam.5kb.bam jelly.clam.10kb.bam \
-o /mouse/Mya/besst/besst_jelly \
--orientation fr rf rf \


```

<<<<<<< Updated upstream
RNAscaffolding
==
=======
LINKS on jelly > BESST scaffolded genome

in `/mouse/Mya/links` file is `jelly.besst.fasta -> /mouse/Mya/besst/besst_jelly/BESST_output/pass3/Scaffolds_pass3.fa`

pacbio is `/mouse/Mya/output_lsc/corrected_LR.fastq` and `/mouse/Mya/output_lsc/uncorrected_LR.fasta`


```
LINKS -d 500 -f jelly.besst.fasta -s files -b iter500
LINKS -d 600 -f iter500.scaffolds.fa -s files -b iter600
LINKS -d 800 -f iter500.scaffolds.fa -s files -b iter800
LINKS -d 1000 -f iter800.scaffolds.fa -s files -b iter1000
LINKS -d 1500 -f iter1000.scaffolds.fa -s files -b iter1500
LINKS -d 2000 -f iter1500.scaffolds.fa -s files -b iter2000
LINKS -d 2500 -f iter2000.scaffolds.fa -s files -b iter2500
LINKS -d 3000 -f iter2500.scaffolds.fa -s files -b iter3000
LINKS -d 3500 -f ite3000.scaffolds.fa -s files -b iter3500
LINKS -d 4000 -f iter3500.scaffolds.fa -s files -b iter4000





```

>>>>>>> Stashed changes

in `/mouse/Mya/genome`

```
python /share/BESST_RNA/src/Main.py 1 -c jelly.best.fasta -f rna.clam.bam -e 3 -T 20000 -k 500 -d 1 -z 1000 -o rna_scaff
```

results -> jelly.best.RNAscaff.fasta

```
n	n:1000	L50	LG50	NG50	min	N80	N50	N20	E-size	max	sum	name
316572	311616	49881	9800	23312	1000	4124	9600	24101	17839	247712	1.923e9	jelly.best.fasta
308262	303486	46366	8881	25604	1000	4209	10068	26468	19205	250147	1.923e9	jelly.best.RNAscaff.fasta
```

working on L_RNA_scff in `/mouse/Mya/LRNA_scaff`

```
blat -noHead ../genome/jelly.best.RNAscaff.fasta /mnt/data3/macmanes/reference_assemblies/Mya/transcriptome/clam.Trinity.fasta output.psl
```
and 

```
L_RNA_scaffolder.sh -d /home/macmanes/L_RNA_scaffolder/ -j ../genome/jelly.best.RNAscaff.fasta -i clam.psl -o scaff
```

after that - move 


in `/mouse/Mya/genome`

```
samtools flagstat rna.clam.bam
341877012 + 0 in total (QC-passed reads + QC-failed reads)
0 + 0 secondary
59952703 + 0 supplementary
0 + 0 duplicates
341877012 + 0 mapped (100.00% : N/A)
281924309 + 0 paired in sequencing
141105253 + 0 read1
140819056 + 0 read2
240869804 + 0 properly paired (85.44% : N/A)
281529632 + 0 with itself and mate mapped
394677 + 0 singletons (0.14% : N/A)
26571678 + 0 with mate mapped to a different chr
2769139 + 0 with mate mapped to a different chr (mapQ>=5)
```

rm Mya81-contigs.long.fasta.sa


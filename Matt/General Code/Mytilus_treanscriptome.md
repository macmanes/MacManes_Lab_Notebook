Mytilus Transcriptome
--

in `/mouse/Mytilus/raw_reads`

in `/mouse/Mytilus/working_reads/`

	at LesserM*R2*gz > mytilus.muscle.2.fq.gz
	at LesserM*R1*gz > mytilus.muscle.1.fq.gz
	at LesserG*R1*gz > mytilus.gill.1.fq.gz
	at LesserG*R2*gz > mytilus.gill.2.fq.gz	
	
> error Correction

	lighter -t 48 -r mytilus.muscle.1.fq.gz -r mytilus.muscle.2.fq.gz -k 25 6000000000 .1
	lighter -t 48 -r mytilus.gill.1.fq.gz -r mytilus.gill.2.fq.gz -k 25 6000000000 .1	

error corrected reads in `/mouse/Mytilus/working_reads/corrected`

> fastqc
		
	fastqc -t 24 mytilus.muscle.2.fq.gz
	fastqc -t 24 mytilus.muscle.1.fq.gz
	fastqc -t 24 mytilus.gill.1.fq.gz
	fastqc -t 24 mytilus.gill.2.fq.gz
	
> trimming

in `/mouse/Mytilus/working_reads/corr_trim`

    java -Xmx50g -jar /share/trinityrnaseq-code/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 48 -baseout mytilus.muscle.lighter25.trimP2.fastq \
    ../corrected/mytilus.muscle.1.fq.cor.fq.gz \
    ../corrected/mytilus.muscle.2.fq.cor.fq.gz  \
    ILLUMINACLIP:/share/trinityrnaseq-code/trinity-plugins/Trimmomatic-0.32/adapters/TruSeq3-PE.fa:2:30:10 \
    SLIDINGWINDOW:4:2 \
	LEADING:2 \
	TRAILING:2 \
	MINLEN:25

Input Read Pairs: 128884968 Both Surviving: 87677737 (68.03%) Forward Only Surviving: 41205876 (31.97%) Reverse Only Surviving: 0 (0.00%) Dropped: 1355 (0.00%) 

    java -Xmx50g -jar /share/trinityrnaseq-code/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 48 -baseout mytilus.gill.lighter25.trimP2.fastq \
    ../corrected/mytilus.gill.1.fq.cor.fq.gz \
    ../corrected/mytilus.gill.2.fq.cor.fq.gz  \
    ILLUMINACLIP:/share/trinityrnaseq-code/trinity-plugins/Trimmomatic-0.32/adapters/TruSeq3-PE.fa:2:30:10 \
    SLIDINGWINDOW:4:2 \
	LEADING:2 \
	TRAILING:2 \
	MINLEN:25

Input Read Pairs: 45155908 Both Surviving: 29798779 (65.99%) Forward Only Surviving: 15356935 (34.01%) Reverse Only Surviving: 0 (0.00%) Dropped: 194 (0.00%)


> trinity muscle + gill

    Trinity --seqType fq --JM 150G --SS_lib_type RF \
    --left mytilus.muscle.lighter25.trimP2_1P.fastq,mytilus.gill.lighter25.trimP2_1P.fastq  \
    --right mytilus.muscle.lighter25.trimP2_2P.fastq,mytilus.gill.lighter25.trimP2_2P.fastq \
    --CPU 30 --output MG.lighter.P2 --group_pairs_distance 999 --inchworm_cpu 10

in `/mouse/Mytilus/working_reads/bwa`

	bwa index -p index MG.lighter.P2.Trinity.fasta
	bwa mem -t40 index  /mouse/Mytilus/working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_1P.fastq /mouse/Mytilus/working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_2P.fastq | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - muscle
	bwa mem -t40 index  /mouse/Mytilus/working_reads/corr_trim/mytilus.gill.lighter25.trimP2_1P.fastq /mouse/Mytilus/working_reads/corr_trim/mytilus.gill.lighter25.trimP2_2P.fastq | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - gill
	
eXpress

	express MG.lighter.P2.Trinity.fasta gill.bam -o gill_express --rf-stranded
	express MG.lighter.P2.Trinity.fasta muscle.bam -o muscle_express --rf-stranded
	
sort by TPM > 1


CD-HIT_EST

	cd-hit-est -M 5000 -T 24 -c .97 -i MG.lighter.P2.expressfilt.Trinity.fasta -o MG.lighter.P2.expressfilt.cdhit.Trinity.fasta
	
remap reduced dataset with BWA

	bwa index -p index2 MG.lighter.P2.expressfilt.cdhit.Trinity.fasta
	bwa mem -t40 index2  /mouse/Mytilus/working_reads/corr_trim/mytilus.gill.lighter25.trimP2_1P.fastq /mouse/Mytilus/working_reads/corr_trim/mytilus.gill.lighter25.trimP2_2P.fastq | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - gill_reduced
	bwa mem -t40 index2  /mouse/Mytilus/working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_1P.fastq /mouse/Mytilus/working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_2P.fastq | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - muscle_reduced	
	
TransDecoder in `/mouse/Mytilus/express`

	TransDecoder -t MG.lighter.P2.expressfilt.cdhit.Trinity.fasta --CPU 20 --search_pfam /home/macmanes/cpg_project/prot/Pfam-A.hmm
	

BLAST

in `/mouse/Mytilus/blast`

Downloaded invert protein and RNA databases to run blastP and blastN

	blastp -db invertprot -query ../express/MG.lighter.P2.expressfilt.cdhit.Trinity.fasta.transdecoder.pep -outfmt 6 -evalue 1e-2 -num_threads 20 -out invert.blastp
	blastn -db invert -query Trinity.fasta -outfmt 6 -evalue 1e-2 -num_threads 20 -out invert.blastnq

The assemblies are pretty crappy for so many reads.. I'm going to try different assembly. **This is using r3999**

    Trinity --seqType fq --JM 150G --SS_lib_type FR \
    --left mytilus.muscle.lighter25.trimP2_1P.fastq,mytilus.gill.lighter25.trimP2_1P.fastq  \
    --right mytilus.muscle.lighter25.trimP2_2P.fastq,mytilus.gill.lighter25.trimP2_2P.fastq \
    --CPU 20 --output MG.lighter.P2 --group_pairs_distance 999 --inchworm_cpu 10 --bflyHeapSpaceMax 50G

	
in `/mouse/Mytilus/express` will run new transdecoder

	TransDecoder -t ../assembly/new.MG.lighter.P2/Trinity.fasta --CPU 20 --search_pfam /home/macmanes/cpg_project/prot/Pfam-A.hmm
	

in `/mouse/Mytilus/bwa`

will test the protien coding things with a small read dataset. 

	ln -s ../express/Trinity.fasta.transdecoder.mRNA .
	bwa index -p mrna Trinity.fasta.transdecoder.mRNA
	head -800000 /mouse/Mytilus/working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_1P.fastq > test.1.fq
	head -800000 /mouse/Mytilus/working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_2P.fastq > test.2.fq	

	bwa mem -t40 mrna  test.1.fq test.2.fq | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - mrnatest	

OK, so 90% of the reads map to the transdecoder predicted mRNA's. COOL!

lets run cd-hit in `express/`

	cd-hit-est -M 5000 -T 24 -c .97 -i Trinity.fasta.transdecoder.mRNA -o MG.lighter.P2.TransDec.cdhit.Trinity.mrna

full run

    bwa mem -t20 mrna  /mouse/Mytilus/working_reads/corr_trim/mytilus.gill.lighter25.trimP2_1P.fastq /mouse/Mytilus/working_reads/corr_trim/mytilus.gill.lighter25.trimP2_2P.fastq | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - gill_mrna
    bwa mem -t20 mrna  /mouse/Mytilus/working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_1P.fastq /mouse/Mytilus/working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_2P.fastq | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - muscle_mrna    

about 90% of reads mapping. 


express

	express MG.lighter.P2.TransDec.cdhit.Trinity.mrna muscle_mrna.bam -o muscle_mrna_express --rf-stranded
	

Muscle versus gill

    awk '{print $2 "\t" $15}' muscle_mrna_express/results.xprs | sed '1,1d' | sort -k1 > muscle.exp
    awk '{print $2 "\t" $15}' gill_mrna_express/results.xprs | sed '1,1d' | sort -k1 > gill.exp
    paste muscle.exp gill.exp > MG.expression
    awk '{print $1 "\t" $2 "\t" $4"\t" $2-$4}' MG.expression > MG.exp
    awk 'NR>2 {sum+=$2; array[NR]=$2} END {for(x=1;x<=NR;x++){sumsq+=((array[x]-(sum/NR))^2);}print sqrt(sumsq/NR)}' MG.exp
    awk 'NR>2 {sum+=$3; array[NR]=$3} END {for(x=1;x<=NR;x++){sumsq+=((array[x]-(sum/NR))^2);}print sqrt(sumsq/NR)}' MG.exp


Things more than 2SD more highly expressed in muscle

	awk '600>$4{next}1' MG.exp | wc -l
	105 things..
	
Things more than 2SD more highly expressed in gill

BLAST


    blastn -db invert -query MG.lighter.P2.TransDec.cdhit.Trinity.mrna -outfmt 6 -evalue 1e-2 -num_threads 20 -out invert.blastn
    

need to make pep file out of new mrna file:

in `Transdecoder/`

	TransDecoder -t MG.lighter.P2.TransDec.cdhit.Trinity.mrna --CPU 20 --search_pfam /home/macmanes/cpg_project/prot/Pfam-A.hmm
	
then, in `blast/`

    blastp -db invertprot -query MG.lighter.P2.TransDec.cdhit.Trinity.mrna.transdecoder.pep \
    -outfmt 6 -evalue 1e-2 -num_threads 10 -out invert.blastp
    

Good, about 60k hits to proteins in the 75k things. this is a pretty good number. Next I'll work on the gene ontology stuff..

>**Pull out things highly expressed in muscle and gill**

>in `/mouse/Mytilus/go`


	awk '1>$3{next}1' MG.exp | awk -F "|" '{print $1}' > highexp.in.muscle
	awk '1>$2{next}1' MG.exp | awk -F "|" '{print $1}' > highexp.in.gill

>extract out GI's

	grep -w -f highexp.in.muscle invert.blastp | awk '{print $2}' | awk -F "|" '{print $2}' > highexp.in.muscle.gis
	
	grep -w -f highexp.in.gill invert.blastp | awk '{print $2}' | awk -F "|" '{print $2}' > highexp.in.gill.gis
	

final
--

```
transrate -a new.MG.lighter.P2.Trinity.fasta -t 20 -o myt -l ../working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_1P.fastq.gz,../working_reads/corr_trim/mytilus.gill.lighter25.trimP2_1P.fastq.gz -r ../working_reads/corr_trim/mytilus.muscle.lighter25.trimP2_2P.fastq.gz,../working_reads/corr_trim/mytilus.gill.lighter25.trimP2_2P.fastq.gz
/share/transrate-1.0.0-linux-x86_64/lib/app/ruby/lib/ruby/gems/2.2.0/gems/bundler-1.7.12/lib/bundler/runtime.rb:222: warning: Insecure world writable dir /share in PATH, mode 040777
[ INFO] 2015-12-01 10:21:14 : Loading assembly: new.MG.lighter.P2.Trinity.fasta
[ INFO] 2015-12-01 10:23:21 : Analysing assembly: new.MG.lighter.P2.Trinity.fasta
[ INFO] 2015-12-01 10:23:21 : Calculating contig metrics...
[ INFO] 2015-12-01 10:25:14 : Contig metrics:
[ INFO] 2015-12-01 10:25:14 : -----------------------------------
[ INFO] 2015-12-01 10:25:14 : n seqs                       369738
[ INFO] 2015-12-01 10:25:14 : smallest                        200
[ INFO] 2015-12-01 10:25:14 : largest                       18179
[ INFO] 2015-12-01 10:25:14 : n bases                   262407705
[ INFO] 2015-12-01 10:25:14 : mean len                     709.71
[ INFO] 2015-12-01 10:25:14 : n under 200                       0
[ INFO] 2015-12-01 10:25:14 : n over 1k                     72024
[ INFO] 2015-12-01 10:25:14 : n over 10k                       10
[ INFO] 2015-12-01 10:25:14 : n with orf                    69649
[ INFO] 2015-12-01 10:25:14 : mean orf percent              50.93
[ INFO] 2015-12-01 10:25:14 : n90                             280
[ INFO] 2015-12-01 10:25:14 : n70                             568
[ INFO] 2015-12-01 10:25:14 : n50                            1210
[ INFO] 2015-12-01 10:25:14 : n30                            2081
[ INFO] 2015-12-01 10:25:14 : n10                            3691
[ INFO] 2015-12-01 10:25:14 : gc                             0.33
[ INFO] 2015-12-01 10:25:14 : gc skew                       -0.06
[ INFO] 2015-12-01 10:25:14 : at skew                       -0.03
[ INFO] 2015-12-01 10:25:14 : cpg ratio                      1.49
[ INFO] 2015-12-01 10:25:14 : bases n                           0
[ INFO] 2015-12-01 10:25:14 : proportion n                    0.0
[ INFO] 2015-12-01 10:25:14 : linguistic complexity          0.12
[ INFO] 2015-12-01 10:25:14 : Contig metrics done in 113 seconds
[ INFO] 2015-12-01 10:25:14 : Calculating read diagnostics...
[ INFO] 2015-12-01 12:10:54 : Read mapping metrics:
[ INFO] 2015-12-01 12:10:54 : -----------------------------------
[ INFO] 2015-12-01 12:10:54 : fragments                 117476516
[ INFO] 2015-12-01 12:10:54 : fragments mapped          108590228
[ INFO] 2015-12-01 12:10:54 : p fragments mapped             0.92
[ INFO] 2015-12-01 12:10:54 : good mappings              91860161
[ INFO] 2015-12-01 12:10:54 : p good mapping                 0.78
[ INFO] 2015-12-01 12:10:54 : bad mappings               16730067
[ INFO] 2015-12-01 12:10:54 : potential bridges             83407
[ INFO] 2015-12-01 12:10:54 : bases uncovered            38372881
[ INFO] 2015-12-01 12:10:54 : p bases uncovered              0.15
[ INFO] 2015-12-01 12:10:54 : contigs uncovbase            266214
[ INFO] 2015-12-01 12:10:54 : p contigs uncovbase            0.72
[ INFO] 2015-12-01 12:10:54 : contigs uncovered             46656
[ INFO] 2015-12-01 12:10:54 : p contigs uncovered            0.13
[ INFO] 2015-12-01 12:10:54 : contigs lowcovered            57381
[ INFO] 2015-12-01 12:10:54 : p contigs lowcovered           0.16
[ INFO] 2015-12-01 12:10:54 : contigs segmented             24796
[ INFO] 2015-12-01 12:10:54 : p contigs segmented            0.07
[ INFO] 2015-12-01 12:10:54 : Read metrics done in 6340 seconds
[ INFO] 2015-12-01 12:10:54 : No reference provided, skipping comparative diagnostics
[ INFO] 2015-12-01 12:10:55 : TRANSRATE ASSEMBLY SCORE     0.1495
[ INFO] 2015-12-01 12:10:55 : -----------------------------------
[ INFO] 2015-12-01 12:10:55 : TRANSRATE OPTIMAL SCORE      0.3813
[ INFO] 2015-12-01 12:10:55 : TRANSRATE OPTIMAL CUTOFF     0.1315
[ INFO] 2015-12-01 12:10:56 : good contigs                 267787
[ INFO] 2015-12-01 12:10:56 : p good contigs                 0.72
[ INFO] 2015-12-01 12:10:56 : Writing contig metrics for each contig to myt_new.MG.lighter.P2.Trinity.fasta_contigs.csv
[ INFO] 2015-12-01 12:13:00 : Writing analysis results to myt_assemblies.csv
```

busco on aws

```
python3 ~/BUSCO_v1.1b1/BUSCO_v1.1b1.py -o full -in ../assembly/new.MG.lighter.P2.Trinity.fasta -l metazoa -m Trans -c 32
90% complete both

```


Trandecoder
--

```
TransDecoder.LongOrfs -t ../assembly/good.new.MG.lighter.P2.Trinity.fasta -S
BAD
```

Counting

```
mkdir /mnt/quant
cd /mnt/quant
kallisto index -i transcripts.idx ../assembly/good.new.MG.lighter.P2.Trinity.fasta
kallisto quant -t 32 -i transcripts.idx -o kallisto_muscle -b 100 \
/mnt/reads/mytilus.muscle.lighter25.trimP2_1P.fastq.gz \
/mnt/reads/mytilus.muscle.lighter25.trimP2_2P.fastq.gz

kallisto index -i transcripts.idx ../assembly/good.new.MG.lighter.P2.Trinity.fasta
kallisto quant -t 32 -i transcripts.idx -o kallisto_gill -b 100 \
/mnt/reads/mytilus.gill.lighter25.trimP2_1P.fastq.gz \
/mnt/reads/mytilus.gill.lighter25.trimP2_2P.fastq.gz


cd $HOME/quant
~/salmon-0.5.1/bin/salmon index -t ../assembly/good.new.MG.lighter.P2.Trinity.fasta -i transcripts_index --type quasi -k 31
~/salmon-0.5.1/bin/salmon quant -p 32 -i transcripts_index -l MSR \
-1 /mnt/reads/mytilus.gill.lighter25.trimP2_1P.fastq.gz \
-2 /mnt/reads/mytilus.gill.lighter25.trimP2_2P.fastq.gz -o salmon_gill

~/salmon-0.5.1/bin/salmon index -t ../assembly/good.new.MG.lighter.P2.Trinity.fasta -i transcripts_index --type quasi -k 31
~/salmon-0.5.1/bin/salmon quant -p 32 -i transcripts_index -l MSR \
-1 /mnt/reads/mytilus.muscle.lighter25.trimP2_1P.fastq.gz \
-2 /mnt/reads/mytilus.muscle.lighter25.trimP2_2P.fastq.gz -o salmon_muscle

```



	

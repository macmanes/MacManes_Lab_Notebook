Mya Genome
--

in `/mnt/data3/macmanes/Mya`
	
	lighter -t 48 -r <1914-KO-1_1_sequence.fastq  -r 1914-KO-1_2_sequence.fastq -k 25 6000000000 .1
	
results

    [2014-11-20 17:18:46] =============Start====================
    [2014-11-20 17:18:59] Bad quality threshold is #
    [2014-11-20 17:54:24] Finish sampling kmers
    [2014-11-20 17:54:24] Bloom filter A's error rate: 0.000008
    [2014-11-20 20:22:22] Finish storing trusted kmers
    [2014-11-20 22:16:45] Finish error correction
    Processed 1189278362 reads:
            921900471 are error-free
            Corrected 204929593 bases(0.766442 corrections for reads with errors)
            Trimmed 0 reads with average trimmed bases 0.000000
            Discard 0 reads
            
> Trimming

	java -Xmx50g -jar /share/trinityrnaseq-code/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
	-threads 48 -baseout mya.lighter25.trimP2.fastq \
	1914-KO-1_1_sequence.cor.fq \
	1914-KO-1_2_sequence.cor.fq  \
	ILLUMINACLIP:/share/trinityrnaseq-code/trinity-plugins/Trimmomatic-0.32/adapters/TruSeq3-PE.fa:2:30:10

Input Read Pairs: 594639181 Both Surviving: 592762879 (99.68%) Forward Only Surviving: 1875579 (0.32%) Reverse Only Surviving: 0 (0.00%) Dropped: 723 (0.00%)



> normalize

	interleave-reads.py /mnt/data3/macmanes/Mya/mya.lighter25.trimP2_1P.fastq \
	/mnt/data3/macmanes/Mya/mya.lighter25.trimP2_2P.fastq -o mya.lighter25.trimP2.fq  

	# Normalize	

	normalize-by-median.py -p -k 21 -C 50 -N 4 -x 15e9 mya.lighter25.trimP2.fq.gz -o mya.lighter25.trimP2.C50norm.fq  

	normalize-by-median.py -p -k 21 -C 50 -N 4 -x 15e9 <(interleave-reads.py /mnt/data3/macmanes/Mya/mya.lighter25.trimP2_1P.fastq /mnt/data3/macmanes/Mya/mya.lighter25.trimP2_2P.fastq) -o mya.lighter25.trimP2.C50norm.fq  



> split

	split --lines=72000000 --additional-suffix .fastq \
	mya.lighter25.trimP2.C50norm.fq

> Assembly

-ABySS

	for k in 61 67 75; do
	     mkdir k$k;
	     abyss-pe -C k$k np=40 k=$k name=clam$k n=5 long=long1 \
	     in='../x*.fastq' \
	     long1='../clam.Trinity.fasta'; 
	done



spades list
	
	bwa mem -a -t40 -S -P spades clam.Trinity.fasta > spades.sam
	samtools view -S -F4 spades.sam > spades-filtered.sam
	awk '{print $1}' spades-filtered.sam | grep c | sort | uniq | wc -l
	awk '{print $3}' spades-filtered.sam | grep NODE | sort | uniq > list	
	split -l 7000 list
	
	for i in `cat xaa`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp1.fa; done &
	for i in `cat xab`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp2.fa; done &
	for i in `cat xac`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp3.fa; done &
	for i in `cat xad`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp4.fa; done &
	for i in `cat xae`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp5.fa; done &
	for i in `cat xaf`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp6.fa; done &
	for i in `cat xag`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp7.fa; done &
	for i in `cat xah`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp8.fa; done &
	for i in `cat xai`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp9.fa; done &
	for i in `cat xaj`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp10.fa; done &
	for i in `cat xak`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp12.fa; done &
	for i in `cat xal`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp13.fa; done &
	for i in `cat xam`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp14.fa; done &
	for i in `cat xan`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp15.fa; done &
	for i in `cat xao`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp16.fa; done &
	for i in `cat xap`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp17.fa; done &
	for i in `cat xaq`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp18.fa; done &
	for i in `cat xar`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp19.fa; done &
	for i in `cat xas`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp20.fa; done &

	for i in `cat xat`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp21.fa; done &
	for i in `cat xau`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp22.fa; done &
	for i in `cat xav`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp23.fa; done &
	for i in `cat xaw`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp24.fa; done &
	for i in `cat xax`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp25.fa; done &
	for i in `cat xay`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp26.fa; done &
	for i in `cat xaz`; do grep -A1 --max-count=1 -w $i scaffolds.fa >> temp27.fa; done &
	
abyss list
	
	bwa mem -a -t40 -S -P abyss clam.Trinity.fasta > abyss.sam
	samtools view -S -F4 abyss.sam > abyss-filtered.sam
	awk '{print $1}' abyss-filtered.sam | grep c | sort | uniq | wc -l
	awk '{print $3}' abyss-filtered.sam | grep ^[0-9] | sort | uniq > abyss.list	
	split -l 7000 list


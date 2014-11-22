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

	for k in 71 81 91; do
		mkdir k$k
		abyss-pe -C k$k np=40 k=$k name=clam$k n=5 lib='clam' \  
		clam='../x*.fastq'  
	done
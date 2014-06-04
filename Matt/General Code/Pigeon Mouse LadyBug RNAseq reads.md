Pigeon, Mouse, Ladybugs RNAseq

How many reads?

	gzip -cd *gz | grep -c '@HSQ'
	
Trimming


	java -Xmx30g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
	-threads 8 -baseout 2342.trim.fq 2342.1.fastq 2342.2.fastq ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
	LEADING:0 TRAILING:0 SLIDINGWINDOW:4:0 MINLEN:25
	
Input Read Pairs: 11560935 Both Surviving: 9601037 (83.05%) Forward Only Surviving: 1959435 (16.95%) Reverse Only Surviving: 372 (0.00%) Dropped: 91 (0.00%)

For 2345

Input Read Pairs: 5465209 Both Surviving: 4094647 (74.92%) Forward Only Surviving: 1370324 (25.07%) Reverse Only Surviving: 191 (0.00%) Dropped: 47 (0.00%)

For 2346

Input Read Pairs: 6217376 Both Surviving: 4734619 (76.15%) Forward Only Surviving: 1482592 (23.85%) Reverse Only Surviving: 115 (0.00%) Dropped: 50 (0.00%)

For 2336

Input Read Pairs: 2370219 Both Surviving: 1816086 (76.62%) Forward Only Surviving: 554094 (23.38%) Reverse Only Surviving: 25 (0.00%) Dropped: 14 (0.00%)
TrimmomaticPE: Completed successfully

BWA Mapping ladybugs
-

	bwa mem -t25 lb $RAID/pero_pigeons_ladybugs/MM1.trim_1P.fq $RAID/pero_pigeons_ladybugs/MM1.trim_1P.fq | samtools view -@6 -Sub - | samtools sort -m3G -@8 - MM1

Trimming new reads:

in `/mnt/data3/macmanes/pero_pigeons_ladybugs`

	java -Xmx80g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
	-threads 30 -baseout 2346a.trim.fq.gz raw_reads_run2/MM46a.1.fq.gz \
	raw_reads_run2/MM46a.2.fq.gz \
	ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
	LEADING:0 TRAILING:0 SLIDINGWINDOW:4:0 MINLEN:25
	
46

Input Read Pairs: 12,673,036 Both Surviving: 9657940 (76.21%) Forward Only Surviving: 3014798 (23.79%) Reverse Only Surviving: 250 (0.00%) Dropped: 48 (0.00%)


45

Input Read Pairs: 17,676,152 Both Surviving: 13259038 (75.01%) Forward Only Surviving: 4416402 (24.99%) Reverse Only Surviving: 621 (0.00%) Dropped: 91 (0.00%)

36

Input Read Pairs: 21738363 Both Surviving: 16587505 (76.31%) Forward Only Surviving: 5150458 (23.69%) Reverse Only Surviving: 316 (0.00%) Dropped: 84 (0.00%)



Trimming

	
	java -Xmx400g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
	-phred33 -threads 64 -baseout oyster_trim \
	$RAID/macmanes/oyster_genome/1914-KO-1_1_sequence.fq \
	$RAID/macmanes/oyster_genome/1914-KO-1_2_sequence.fq \
	ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
	LEADING:2 \
	TRAILING:2 \
	SLIDINGWINDOW:4:2 \
	MINLEN:55  
	

	Input Read Pairs: 594639181 Both Surviving: 492330600 (82.79%) Forward Only Surviving: 2599252 (0.44%) Reverse Only Surviving: 98602465 (16.58%) Dropped: 1106864 (0.19%)

split

	cat oyster_trim_* | split -l 80000000
	
Assemble:

	for k in 71 81 91 101
		do ABYSS-P -k$k --coverage-hist=k$k.hist \
		/reads/x*
	done 
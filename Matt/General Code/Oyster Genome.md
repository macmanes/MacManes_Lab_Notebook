Trimming

	
	java -Xmx400g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
	-phred33 -threads 64 -baseout oyster_trim \
	1914-KO-1_1_sequence.fq \
	1914-KO-1_2_sequence.fq \
	ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
	LEADING:2 \
	TRAILING:2 \
	SLIDINGWINDOW:4:2 \
	MINLEN:55  
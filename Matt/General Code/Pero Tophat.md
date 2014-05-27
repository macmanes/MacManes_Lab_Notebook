Pero tophat
-

in `/mnt/data3/macmanes/tophat`

	bowtie2-build /mnt/data0/macmanes/maker/pero.genes.fa pero-genome
	
Find input files:

	../pero_annotation/Pero2926.1.fastq
	../pero_annotation/Pero2926.2.fastq
	## and 
	../pero_annotation/Pero2925.1.fastq
	../pero_annotation/Pero2925.2.fastq
	
Tophat

	tophat -p4 -o 2926 --library-type fr-firststrand \
	pero_genome ../pero_annotation/Pero2926.1.fastq ../pero_annotation/Pero2926.2.fastq
Clam genome
--

Discovar make BAM

	java -jar /share/picard-tools-1.121/FastqToSam.jar \
	FASTQ=clam_trim_1P \
	FASTQ2=clam_trim_2P \
	OUTPUT=clam.bam \
	SAMPLE_NAME=Mya_genome TMP_DIR=/mouse
	

Discovar assembly in `/mouse/clam` started 10/8 at 0600

	DiscovarExp READS=clam.bam OUT_DIR=disc_assembly
	
Maybe I should try SPAdes? Shoudld first normalize:


	interleave-reads.py clam_trim_1P.gz clam_trim_2P.gz -o paired.fq.gz


	normalize-by-median.py -p -k 20 -C 50 -N 4 -x 15e9 \
	--savetable normC50k20.kh paired.fq


Spades

	spades.py -t 30 -m 250  --careful \
	--pe1-1 clam_trim_1P.gz \
	--pe1-2 clam_trim_2P.gz \
	-o clam_SPAdes
	


	interleave-reads.py clam_trim_1P.gz clam_trim_2P.gz -o paired.fq.gz | \
	normalize-by-median.py -p -k 20 -C 50 -N 4 -x 15e9 \
	--savetable normC50k20.kh /dev/stdin

Tophat Notes
-

I was an early user of Tophat, way back before there were many good tools for quantitating expression from NGS reads. I was just learning how to process these types of data (e.g., learning a scripting language), so I thought that many of the problems I encountered were a result of my inadequacy -- and maybe they were.. Anyway, I've come full circle, and am again trying to use the Tuxedo package for the RNAseq work. Suffice it to say that I have, thus far, not been impressed with Bowtie2/Tophat. I would have thought that these very popular software packages would have been tighter.. NOT

>> Installation

I began by installing Tophat and Cufflinks - this step was easy.

>> Test Run

I began by running a small test dataset:

	tophat -p8 -o 2926 --library-type fr-firststrand pero ../pero_annotation/Pero2926.1.fastq ../pero_annotation/Pero2926.2.fastq
	
Whoops, there were several issues.

1. I have the samtools developmental version installed (which leverages htslib). Tophat does not recognize this version, and errors out. There is no way to get around this error, save editing the code or installing an older version of samtools. From reading, this looks like an issue with `samtools --version` rather than something about the software itself. Seems like an easy fix, but no..

2. Having resolved the samTools issue, I think I'm good to go - but now there is segfault issue with bowtie2-inspect that causes Tophat to crash. The bug was reported, claimed fixed, but it not.. https://sourceforge.net/p/bowtie-bio/bugs/314/. Ok, so now I have to find a older version of `bowtie2-inspect` that works.. Pain in the ass!

3. Now that is resolved, the next issue. 



		macmanes@davinci:/mnt/data3/macmanes/tophat$ tophat -p8 -o 2926 pero ../pero_annotation/Pero2926.1.fastq ../pero_annotation/Pero2926.2.fastq

		[2014-05-28 07:46:31] Beginning TopHat run (v2.0.11)
	
		-----------------------------------------------
		[2014-05-28 07:46:31] Checking for Bowtie
	 	  Bowtie version:	 2.2.2.0
	
		[2014-05-28 07:46:31] Checking for Samtools
			Samtools version:	 0.1.19.0
		[2014-05-28 07:46:31] Checking for Bowtie index files (genome)..
		[2014-05-28 07:46:31] Checking for reference FASTA file
			Warning: Could not find FASTA file pero.fa
		[2014-05-28 07:46:31] Reconstituting reference FASTA file from Bowtie index
 		 Executing: /share/bin/bowtie2-inspect pero > 2926/tmp/pero.fa
		[2014-05-28 07:49:08] Generating SAM header for pero
		[2014-05-28 07:49:08] Preparing reads
			 left reads: min. length=151, max. length=151, 22922811 kept reads (8500 discarded)
			right reads: min. length=151, max. length=151, 22918434 kept reads (12877 discarded)
		[2014-05-28 08:12:36] Mapping left_kept_reads to genome pero with Bowtie2
			[FAILED]
		Error running bowtie:
		Error while flushing and closing output
		Error while flushing and closing output
		terminate called after throwing an instance of 'int'
		(ERR): bowtie2-align died with signal 6 (ABRT) (core dumped)


	I can dig into the log files, and see that the command that is failing is this one:

		/share/tophat-2.0.11.Linux_x86_64/bam2fastx --all 2926/tmp/left_kept_reads.bam | /share/bin/bowtie2 -k 20 -D 15 -R 2 -N 0 -L 20 -i S,1,1.25 --gbar 4 --mp 6,2 --np 1 --rdg 5,3 --rfg 5,3 --score-min C,-14,0 -p 8 --sam-no-hd -x pero - | /share/tophat-2.0.11.Linux_x86_64/fix_map_ordering --bowtie2-min-score 15 --read-mismatches 2 --read-gap-length 2 --read-edit-dist 2 --read-realign-edit-dist 3 --index-outfile 2926/tmp/left_kept_reads.mapped.bam.index --sam-header 2926/tmp/pero_genome.bwt.samheader.sam - 2926/tmp/left_kept_reads.mapped.bam 2926/tmp/left_kept_reads_unmapped.bam
		

	What you run this command alone, you get:
		
		[sam_read1] missing header? Abort!
		(ERR): bowtie2-align died with signal 13 (PIPE)
		

So, what to do... it seems like mature software like the tuxedo package should be much smoother than this.. I wonder if rolling back to an earlier version of Tophat would work.. 	

EDIT
--

So I downloaded 2.0.9- this version does not recognize Bowtie2 even though it's in my path:

	tophat -p8 -o 2926 --library-type fr-firststrand pero ../pero_annotation/Pero2926.1.fastq ../pero_annotation/Pero2926.2.fastq

	[2014-05-28 12:06:59] Beginning TopHat run (v2.0.9)
	-----------------------------------------------
	[2014-05-28 12:06:59] Checking for Bowtie
 	 Bowtie 2 not found, checking for older version..
			  Bowtie version:	 1.0.0.0
	[2014-05-28 12:06:59] Checking for Samtools
			Samtools version:	 0.1.19.0
	[2014-05-28 12:06:59] Checking for Bowtie index files (genome)..
	Error: Could not find Bowtie index files (pero.*.ebwt)



	$ which bowtie2
	/share/bin/bowtie2
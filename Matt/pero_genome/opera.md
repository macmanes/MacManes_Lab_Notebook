Opera
--

in `/mouse/pero_genome/opera`

	cp /mnt/data3/macmanes/pero-genome/jelly.out.fasta .
	
preprocess
	
	perl /share/opera_v2.0.1/bin/preprocess_reads.pl \
	jelly.out.fasta \
	/mnt/data3/macmanes/pero_genome/raw_reasd/peer5kb.clipped.1.fq \
	/mnt/data3/macmanes/pero_genome/raw_reasd/peer5kb.clipped.2.fq \
	lib_5kb.map bowtie
	

	perl /share/opera_v2.0.1/bin/preprocess_reads.pl \
	jelly.out.fasta \
	/mnt/data3/macmanes/pero_genome/raw_reasd/peer8kb.clipped.1.fq \
	/mnt/data3/macmanes/pero_genome/raw_reasd/peer8kb.clipped.2.fq \
	lib_8kb.map bowtie

	perl /share/opera_v2.0.1/bin/preprocess_reads.pl \
	jelly.out.fasta \
	/mnt/data3/macmanes/pero_genome/raw_reasd/peer7kb.clipped.1.fq \
	/mnt/data3/macmanes/pero_genome/raw_reasd/peer7kb.clipped.2.fq \
	lib_7kb.map bowtie

	perl /share/opera_v2.0.1/bin/preprocess_reads.pl \
	jelly.out.fasta \
	/mnt/data3/macmanes/pero_genome/raw_reasd/peer3kb.clipped.1.fq \
	/mnt/data3/macmanes/pero_genome/raw_reasd/peer3kb.clipped.2.fq \
	lib_3kb.map bowtie

opera


	/share/opera_v2.0.1/bin/opera jelly.out.fasta \
	lib_5kb.map opera5kb_results



	/share/opera_v2.0.1/bin/opera jelly.out.fasta \
	lib_5kb.map,lib_8kb.map \
	opera58kb_results


	/share/opera_v2.0.1/bin/opera jelly.out.fasta \
	lib_5kb.map,lib_8kb.map,lib_7kb.map,lib_3kb.map \
	opera5kb_results


/mnt/data3/macmanes/pero_genome/raw_reasd/peer3kb.clipped.1.fq
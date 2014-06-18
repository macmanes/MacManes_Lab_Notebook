GZIP-TEST
-

in `/mnt/data0/macmanes/zip-test`

This is on SCRATCH, a SSD
28,349,068 PE reads

	time bwa mem -t30 pero_final Pero2925.1.fastq Pero2925.2.fastq > 2925.sam
	
		real	14m47.165s
		user	300m49.346s
		sys	7m38.231s
	time bwa mem -t20 pero_final Pero2925.1.fastq Pero2925.2.fastq > 2925.sam
	
        real	18m25.553s
        user	423m13.094s
        sys	9m58.836s

	time bwa mem -t10 pero_final Pero2925.1.fastq Pero2925.2.fastq > 2925.sam
	
	real	38m34.495s
	user	331m8.599s
	sys	9m18.295s
	
	time bwa mem -t5 pero_final Pero2925.1.fastq Pero2925.2.fastq > 2925.sam
	

GZIPPED FILES

	time bwa mem -t30 pero_final Pero2925.1.fastq.gz Pero2925.2.fastq.gz > 2925.sam
	
        real	18m4.258s
        user	337m9.150s
        sys	9m56.355s
	
	time bwa mem -t20 pero_final Pero2925.1.fastq.gz Pero2925.2.fastq.gz > 2925.sam

        real	21m19.402s
        user	304m19.990s
        sys	6m44.061s
	
	time bwa mem -t10 pero_final Pero2925.1.fastq.gz Pero2925.2.fastq.gz > 2925.sam
		
		real	35m28.982s
		user	298m14.713s
		sys	6m1.854s
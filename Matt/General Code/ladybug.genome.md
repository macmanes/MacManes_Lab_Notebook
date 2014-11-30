ladybug
--

split
	
	split --lines=16000000 --additional-suffix .fastq \
	genome.khmer_normalized.fq


abyss

	for k in 61 71 81 91 101 111 121; do
	     mkdir k$k;
	     abyss-pe -C k$k np=40 k=$k name=k$k n=5 \
	     in='../x*.fastq'; 
	done

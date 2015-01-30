INSTALL Maker


/usr/lib/openmpi/include/mpi.h
/usr/bin/mpicc

2.31.8

Ran CEGMA on AWS, downloaded results to `/mouse/Starling/cegma`

	cegma2zff output.cegma.gff ../genome/Starling_MacManes_AllPathsLG.fasta
	fathom genome.ann genome.dna -categorize 1000
	fathom -export 1000 -plus uni.ann uni.dna  
	forge export.ann export.dna  
	hmm-assembler.pl jelly.out.fasta . > cegmasnap.hmm
	
Barrnap 0.4.2

	barrnap --kingdom euk --threads 10 ../genome/Starling_MacManes_AllPathsLG.fasta



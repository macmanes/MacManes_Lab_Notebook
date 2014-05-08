MPI Maker on workstation
--

	export LD_PRELOAD=/usr/lib/openmpi/lib/libmpi.so

	export OMPI_MCA_mpi_warn_on_fork=0
	
I run maker like this: 

	nohup time mpirun -np 12 ~/maker/bin/maker -fix_nucleotides
	
It seems to be going really fast - annotating 1k contigs in a few hours. 

25 Apr 14
--
About 24,000 contigs annotated (of 37,000)

	nohup time mpirun -np 8 ~/maker/bin/maker -fix_nucleotides &> maker.out &
	

8 May 14 11AM
--
Maker finished!

	~/maker/bin/gff3_merge -d pero.genes_master_datastore_index.log
	
Now I'm going to make a new SNAP hmm using the maker output.

in `/media/macmanes/hd3/maker/pero.genes.maker.output/snap_maker1`


	~/maker/bin/maker2zff ../pero.genes.all.gff
	~/snap/fathom genome.ann genome.dna -categorize 1000
	~/snap/fathom -export 1000 -plus uni.ann uni.dna
	~/snap/forge export.ann export.dna
	/home/macmanes/maker/exe/snap/hmm-assembler.pl ../pero.genes.all.gff . > maker1.snap.hmm
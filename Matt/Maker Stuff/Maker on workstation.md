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
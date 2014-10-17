Install New Version of Trinity on Blacklight
-

Switch to your SCRATCH

	cd $SCRATCH
	
Download, extract, make Trinity

	wget http://downloads.sourceforge.net/project/trinityrnaseq/trinityrnaseq_r20140717.tar.gz
	tar -zxf trinityrnaseq_r20140717.tar.gz
	cd trinityrnaseq_r20140717
	make -j8 LIBCURSES=-lncurses
	#at the end of make, you'll see
	#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    #
	#Performing Unit Tests of Build
    #
	#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
	#JellyFish:               has been Installed Properly
	#Inchworm:                has been Installed Properly
	#Chrysalis:               has been Installed Properly
	#QuantifyGraph:           has been Installed Properly
	#GraphFromFasta:          has been Installed Properly
	#ReadsToTranscripts:      has been Installed Properly
	#fastool:                 has been Installed Properly
	#parafly:                 has been Installed Properly
	#slclust:                 has been Installed Properly
	#collectl:                has been Installed Properly


Tweak Trinity to play nicely with Java

	sed -i 's_java -jar_java -XX:ParallelGCThreads=15 -jar_g' Trinity

Run test data

	cd sample_data/test_Trinity_Assembly/
	module load bowtie samtools blat
	sh runMe.sh
	#should see message "Butterfly assemblies are written to..."
	sh test_FL.sh
	#should see "Trinity.fasta.pslx.map ..."
	
Assuming these tests are passed, you are now ready for the real assembly, which requires a submission script:

	nano assembly.pbs
	
	#!/bin/bash
	#PBS -l ncpus=48 # this gives you 512Gb RAM - should be plenty
	#PBS -l walltime=96:00:00 #you might want 48 hours, shorter queue, probably enough time.
	#PBS -j oe
	#PBS -q batch
	#PBS -m abe -M your_email@gmail.com

	set -x
	source /usr/share/modules/init/bash
	ulimit -u unlimited #critical! Chrysalis will fail if you don't set this. 
	module load bowtie samtools

	cd $SCRATCH/your_dir

	PATH=$PATH:$SCRATCH/trinityrnaseq_r20140717

	ja
	
	Trinity --seqType fq \
	--JM 100G --trimmomatic \
	--bflyHeapSpaceMax 100G \
	--inchworm_cpu 10 \
	--left /path/to/your.left.fastq.gz  \
	--right /path/to/your.right.fastq.gz \
	--CPU 48 \
	--output my_assembly \
	--bflyGCThreads 15 \
	--group_pairs_distance 999 \
	--quality_trimming_params "ILLUMINACLIP:$SCRATCH/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 \
	LEADING:2 TRAILING:2 MINLEN:25" >> my_assembly.log

	ja -chlst
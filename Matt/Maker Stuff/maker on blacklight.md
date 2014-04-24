I run maker on backlight using SNAP and the high quality transcripts. In 48 hours, I annotated 1000 transcripts

    #!/bin/bash
    #PBS -l ncpus=128
    #PBS -l walltime=48:00:00
    #PBS -j oe
    #PBS -q batch
    #PBS -m abe -M macmanes@gmail.com
    
    
    source /usr/share/modules/init/bash
    module load openmpi/1.6/gnu
    module list
    set -x
    echo $LD_PRELOAD
    echo $OMPI_MCA_mpi_warn_on_fork
    which maker
    which mpicc
    which mpirun
    which perl
    
    cd /brashear/macmanes/runs/maker/
    export HMMER_NCPU=16
    export TMPDIR=$SCRATCH_RAMDISK
    export TMP=$SCRATCH_RAMDISK
    
    ja
    mpirun -np 128 /brashear/macmanes/maker-exp/maker/bin/maker -q \ 
    -base mpi128 -fix_nucleotides > maker128.out 2>&1
    ja -chlst`
    

After this, I need to make a single gff file using: 

	/brashear/macmanes/maker-exp/maker/bin/gff3_merge \
	-d mpi128.maker.output/mpi128_master_datastore_index.log -o peer.gff

Then this file I will use in augustus (in `/media/macmanes/hd3/maker/augustus`)

	nohup ~/augustus-3.0.2/scripts/autoAug.pl --genome=../../pero-genome/jelly.out.fasta --species=peer \
	--cdna=../augustus.complete.cds --trainingset=pero.gff --singleCPU -v --useexisting

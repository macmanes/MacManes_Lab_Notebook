PacBio
--


Install stuff

	 pip install numpy --upgrade
	 CFLAGS="-I/usr/lib/openmpi/include/" pip install mpi4py
	 CFLAGS="-I/usr/lib/openmpi/include/" pip install h5py
	 in /share/
	 git clone https://github.com/PacificBiosciences/pbcore.git
	 in pbcore
	 python setup.py install
	 in pbh5tools
	 python setup.py install 

in `/mouse/Mya/pacbio/h5`


	bash5tools.py \
	m141030_013153_42156_c100725792550000001823153204301560_s1_p0.bas.h5 \
	--outFilePrefix myreads --outType fasta --readType subreads

in `/mouse/Mya/pacbio`

	tar -xf A01_1.Clam_2_20kb_BP_HG003_BP_P6_C4_102914_MB_542.tar
	cp sc/orga/projects/pacbio/userdata_permanent/raw/Clam_2_20kb_BP_HG003_BP_P6_C4_102914_MB_542/A01_1/Analysis_Results/*fastq fastq/
	cp sc/orga/projects/pacbio/userdata_permanent/raw/Clam_2_20kb_BP_HG003_BP_P6_C4_102914_MB_542/A01_1/Analysis_Results/*fasta fasta/
	cp sc/orga/projects/pacbio/userdata_permanent/raw/Clam_2_20kb_BP_HG003_BP_P6_C4_102914_MB_542/A01_1/Analysis_Results/*h5 h5/
		
	tar -xf A01_1.Clam_Mya_1_Singapore_MSW_IRRI_P6_C4_MB_4.tar
	cp sc/orga/projects/pacbio/userdata_permanent/raw/Clam_Mya_1_Singapore_MSW_IRRI_P6_C4_MB_4/A01_1/Analysis_Results/m141203_023445_42163R_c100749932550000001823153407081503_s1_p0.* h5/
	

extract fasta

	for i in `ls *bas.h5`; do
		bash5tools.py $i --outFilePrefix $i --outType fasta --readType unrolled;
	done

extract fastq

	for i in `ls *bas.h5`; do
		bash5tools.py $i --outFilePrefix $i --outType fastq --readType unrolled;
	done

	
ectools

	mkdir /mouse/Mya/ectools
	mkdir ectools/organism_correct
	cd organism_correct
	ln -s ../../abyss/k67/clam67-long-scaffs.fa .
	cat *fasta > mya.pacbio.fasta (in `Mya/pacbio/fasta`
	python /share/ectools/partition.py 20 500 /mouse/Mya/pacbio/fasta/mya.pacbio.fasta
	cp /share/ectools/correct.sh . #must modify this substantially, though it is easy)
	

Actually do the correction-- have to do this for each of 100 folders. 

**This command actually works, but have to cd into each directory**
**Ectools aborted, will take months to finish, and breaks down many of the PB reads into shorter pieces, ? maybe because Illumina assembly is not good enough.**


	for i in {1..500}; do 
		SGE_TASK_ID=$i TMPDIR=/tmp ../correct.sh; 
	done

Trying to run the correction: 

    /mouse/Mya/ectools/0001$ ../correct.sh
    + set -e
    + source /home/macmanes/.bashrc
    ++ '[' -z '' ']'
    ++ return
    + CORRECT_SCRIPT=/share/ectools/pb_correct.py
    + PRE_DELTA_FILTER_SCRIPT=/share/ectools/pre_delta_filter.py
    + MIN_ALIGNMENT_LEN=200
    + WIGGLE_PCT=0.05
    + CONTAINED_PCT_ID=0.80
    + UNITIG_FILE=/mouse/Mya/ectools/organism_correct/clam67-long-scaffs.fa
    + CLR_PCT_ID=0.96
    + MIN_READ_LEN=3000
    + NUCMER_BREAK_LEN=2000
    + PRE_DELTA_FILTER=true
    ++ printf %04d
    + suffix=0000
    + FILE=p0000
    ++ pwd
    + ORIGINAL_DIR=/mouse/Mya/ectools/0001
    + [[ -n '' ]]
    + cp /mouse/Mya/ectools/0001/p0000 .
    cp: cannot stat ‘/mouse/Mya/ectools/0001/p0000’: No such file or directory

In folder `0001` and all others, there is no `p0000`, it starts with `p0001`

Please advise. 


trying another method

	for j in {1..500}; do 
		echo "SGE_TASK_ID=$j TMPDIR=/tmp ../correct.sh"; 
		done  | parallel -j 20
		
Lordec

	lordec-correct -threads 20 /mouse/Mya/mya.corr.trim.fq 21 2 \
	/mouse/Mya/pacbio/fasta/mya.pacbio.fasta \
	/mouse/Mya/pacbio/fasta/mya.lordec.pacbio.fasta


>Maybe try PBcR

	fastqToCA -insertsize 200 30 -libraryname mya.illumina -technology illumina \
	-type sanger -mates /mouse/Mya/mya.corr.trim.fq > mya.illumina.frg

	PBcR -pbCNS -s spec.txt -fastq /mouse/Mya/pacbio/fastq/mya.pacbio.fastq \
	-length 1000 -partitions 20 -l mya.pacbio.pbcr -t 20 -genomeSize 550000000 \
	/mouse/Mya/pbcr/mya.illumina.frg
	


whoops, building pbdagcon

	http://downloads.sourceforge.net/project/log4cpp/log4cpp-1.1.x%20%28new%29/log4cpp-1.1/log4cpp-1.1.1.tar.gz
	./configure --prefix=/share/bin/
	make
	make check
	make install
	
	git clone https://github.com/PacificBiosciences/pbdagcon.git
	cd pbdagcon
	git submodule init
	git submodule update
	
>**dbg2olc on AWS**

>**Must have all python scripts in same folder**

	DBG2OLC_Linux k 17 KmerCovTh 2 MinOverlap 10 AdaptiveTh 0.001 LD1 0 \
	Contigs /mnt/clam67-6.fa RemoveChimera 1 MinLen 500 \
	f /mnt/mya.pacbio.fasta
	

	cat /mnt/clam67-6.fa /mnt/mya.pacbio.fasta > ctg_pb.fasta
	$HOME/dbg2olc/split_and_run_pbdagcon.sh backbone_raw.fasta  \
	DBG2OLC_Consensus_info.txt ctg_pb.fasta ./consensus_dir >consensus_log.txt &


**RUN THIS COMMAND FOR PBcR WHEN TIME**
**IT WILL TAKE A MONTH OR MORE**

in `/mouse/Mya/pbcr`

	PBcR -s spec2.txt -fastq /mouse/Mya/pacbio/fastq/mya.pacbio.fastq -length 1000 \
	-partitions 40 -l mya.pacbio.pbcr -t 40 -pbCNS -genomeSize 550000000 \
	/mouse/Mya/pbcr/mya.illumina.frg
	

LSC
--

**aln command**
	-n 0.01 -o 20 -e 3 -d 0 -i 0 -M 1 -O 0 -E 1 -N
	
	-n NUM    max #diff (int) or missing prob under 0.02 err rate (float) [0.04
	-o INT    maximum number or fraction of gap opens [1]
	-e INT    maximum number of gap extensions, -1 for disabling long gaps [-1]
	-i INT    do not put an indel within INT bp towards the ends [5]	
	-d INT    maximum occurrences for extending a long deletion [10]
	-M INT    mismatch penalty [3]
	-O INT    gap open penalty [11]
	-E INT    gap extension penalty [4]
	-N        non-iterative mode: search for all n-difference hits (slooow)


**mem commands**

	-k14 -W20 -r10 -A1 -B1 -O1 -E1 -L0
	


































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
	

extract fastq

	for i in `ls *bas.h5`; do
		bash5tools.py $i --outFilePrefix $i --outType fasta --readType unrolled;
	done
	
ectools

	mkdir /mouse/Mya/ectools
	mkdir ectools/organism_correct
	cd organism_correct
	ln -s ../../abyss/k67/clam67-long-scaffs.fa .
	cat *fasta > mya.pacbio.fasta (in `Mya/pacbio/fasta`
	python /share/ectools/partition.py 20 500 /mouse/Mya/pacbio/fasta/mya.pacbio.fasta
	cp /share/ectools/correct.sh . #must modify this substantially, though it is easy)
	

Actually do teh correction



	for i in {0001..000N}; do 
		cd $i; SGE_TASK_ID=1 TMPDIR=/tmp ../correct.sh; cd ..; 
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





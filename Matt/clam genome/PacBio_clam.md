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
	
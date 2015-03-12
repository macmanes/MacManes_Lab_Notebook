Mc_Transcriptome
--

in `$RAID/Mc_transcriptome`

       lighter -t 60 \
    -r Thomas_McOr3_R2.PF.fastq \
    -r Thomas_McOr3_R1.PF.fastq \
    -r Thomas_McOr2_R2.PF.fastq \
    -r Thomas_McOr2_R1.PF.fastq \
    -r Thomas_McOr1_R2.PF.fastq \
    -r Thomas_McOr1_R1.PF.fastq \
    -r Thomas_McBr3_R1.PF.fastq \
    -r Thomas_McBr3_R2.PF.fastq \
    -r Thomas_McBr1_R1.PF.fastq \
    -r Thomas_McBr1_R2.PF.fastq \
    -r Thomas_McBr2_R1.PF.fastq \
    -r Thomas_McBr2_R2.PF.fastq \
    -k 32 600000000 .05
    
trinity

	Trinity --seqType fq --max_memory 200G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McBr3_R1.PF.cor.fq,\
	Thomas_McOr1_R1.PF.cor.fq,\
	Thomas_McOr2_R1.PF.cor.fq,\
	Thomas_McOr3_R1.PF.cor.fq,\
	Thomas_McBr2_R1.PF.cor.fq,\
	Thomas_McBr1_R1.PF.cor.fq \
	--right Thomas_McBr3_R2.PF.cor.fq,\
	Thomas_McOr1_R2.PF.cor.fq,\
	Thomas_McOr2_R2.PF.cor.fq,\
	Thomas_McOr3_R2.PF.cor.fq,\
	Thomas_McBr2_R2.PF.cor.fq,\
	Thomas_McBr1_R2.PF.cor.fq \
	--CPU 60 --output mc_lighter_trinity --group_pairs_distance 999
	
Phylosift

mcbr3


	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McBr3_R1.PF.cor.fq \
	--right Thomas_McBr3_R2.PF.cor.fq \
	--CPU 16 --output mcbr3_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcbr3 mcbr3_lighter_trinity/Trinity.fasta


	#McBr2

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McBr2_R1.PF.cor.fq \
	--right Thomas_McBr2_R2.PF.cor.fq \
	--CPU 16 --output mcbr2_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check


	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcbr2 mcbr2_lighter_trinity/Trinity.fasta


	#McBr1

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McBr1_R1.PF.cor.fq \
	--right Thomas_McBr1_R2.PF.cor.fq \
	--CPU 16 --output mcbr3_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcbr1 mcbr1_lighter_trinity/Trinity.fasta


	#McOr3

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McOr1_R1.PF.cor.fq \
	--right Thomas_McOr1_R2.PF.cor.fq \
	--CPU 16 --output mcor1_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcor1 mcor1_lighter_trinity/Trinity.fasta



	#McOr2

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McOr2_R1.PF.cor.fq \
	--right Thomas_McOr2_R2.PF.cor.fq \
	--CPU 16 --output mcor2_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcor2 mcor2_lighter_trinity/Trinity.fasta


	#McOr3

	Trinity --seqType fq --max_memory 20G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McOr3_R1.PF.cor.fq \
	--right Thomas_McOr3_R2.PF.cor.fq \
	--CPU 16 --output mcor3_lighter_trinity --group_pairs_distance 999 --bypass_java_version_check

	phylosift all --debug --bayes --besthit --extended --threads 16 --output mcor3 mcor3_lighter_trinity/Trinity.fasta


phylosift 




AWS Install Stuff
--

	cd
	apt-get update
	
	apt-get -y upgrade
	
	apt-get -y install subversion tmux git curl bowtie libncurses5-dev samtools gcc make g++ python-dev unzip dh-autoreconf default-jre python-pip zlib1g-dev
	
	git clone https://github.com/trinityrnaseq/trinityrnaseq.git
	
	cd trinityrnaseq
	
	make -j8

change in plans: this this after trinity completes
--


	cd /mnt
	wget http://edhar.genomecenter.ucdavis.edu/~koadman/phylosift/phylosift_latest.tar.bz2
	
	tar -jxf phylosift_latest.tar.bz2
	
	PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/ubuntu/trinityrnaseq:/mnt/phylosift_20140419

	nano /mnt/phylosift_20140419/lib/Phylosift/pplacer.pm


mod phylosift config file
--

	mkdir /mnt/markers/
	nano /mnt/config
	
contents

	$marker_dir='/mnt/markers/';
	$markers_extended_dir='/mnt/markers/';
	$ncbi_dir = '/mnt/markers/';
	$marker_path='/mnt/markers/';
	$ncbi_path='/mnt/markers/';
	$marker_base_url = 'http://edhar.genomecenter.ucdavis.edu/~koadman/phylosift_markers';
	$ncbi_url = 'http://edhar.genomecenter.ucdavis.edu/~koadman/ncbi.tgz';
	$pplacer_groups = 10;
	$pplacer_verbosity = 1;

run phylosift

	tmux new -s phylosift
	phylosift all --debug --bayes --besthit --extended --config config --threads 16 --output mcor3 mcor3_lighter_trinity/Trinity.fasta
	phylosift all --debug --bayes --besthit --extended --config config --threads 16 --output mcor2 mcor2_lighter_trinity/Trinity.fasta
	phylosift all --debug --bayes --besthit --extended --config config --threads 16 --output mcor1 mcor1_lighter_trinity/Trinity.fasta
	phylosift all --debug --bayes --besthit --extended --config config --threads 16 --output mcbr3 mcbr3_lighter_trinity/Trinity.fasta
	phylosift all --debug --bayes --besthit --extended --config config --threads 16 --output mcbr2 mcbr2_lighter_trinity/Trinity.fasta








Feeding Final
--

on davinci

    /mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_2.fastq.gz
    /mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_2.fastq.gz
    /mnt/data3/macmanes/subsamp/10M_corr/raw.10M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/10M_corr/raw.10M.SRR797058_2.fastq.gz
    /mnt/data3/macmanes/subsamp/50M_corr/raw.50M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/50M_corr/raw.50M.SRR797058_2.fastq.gz
    


aws stuff

	sudo mkfs -t ext4 /dev/xvdb
	sudo mount /dev/xvdb /mnt
	sudo chown -R ubuntu:ubuntu /mnt
	

	sudo bash
	apt-get update
	apt-get -y upgrade
	apt-get -y install openmpi* sparsehash libboost-atomic1.55-dev libboost1.55-dbg subversion tmux git curl bowtie libncurses5-dev samtools gcc make g++ python-dev unzip dh-autoreconf default-jre python-pip zlib1g-dev
	
	
	easy_install -U setuptools
	git clone https://github.com/ged-lab/khmer.git
	cd khmer 
	make
	
	git clone https://github.com/trinityrnaseq/trinityrnaseq.git
	wget http://downloads.sourceforge.net/project/bless-ec/bless.v0p17.tgz
	PATH=$PATH:/home/ubuntu/v0p17:/home/ubuntu/trinityrnaseq:/home/ubuntu/khmer/scripts

download data

	scp macmanes@davinci.unh.edu:/mnt/data3/macmanes/subsamp/10M_corr/raw.10M.SRR797058_*.fastq.gz .
	scp macmanes@davinci.unh.edu:/mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_*.fastq.gz .

	scp macmanes@davinci.unh.edu:/mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_*.fastq.gz .


on AWS 10M

    ~/trinityrnaseq/Trinity --seqType fq --max_memory 40G --trimmomatic \
        --left /mnt/raw.10M.SRR797058_1.fastq.gz  \
        --right /mnt/raw.10M.SRR797058_2.fastq.gz \
        --CPU 32 --output trinity_10M_raw

on AWS 20M

    ~/trinityrnaseq/Trinity --seqType fq --max_memory 40G --trimmomatic \
        --left /mnt/raw.20M.SRR797058_1.fastq.gz  \
        --right /mnt/raw.20M.SRR797058_2.fastq.gz \
        --CPU 32 --output trinity_20M_raw

        
100M

    ~/trinityrnaseq/Trinity --seqType fq --max_memory 40G --trimmomatic \
        --left /mnt/raw.100M.SRR797058_1.fastq.gz \
        --right /mnt/raw.100M.SRR797058_2.fastq.gz \
        --CPU 32 --output trinity_100M_raw


lets see if 100M run can work with 60Gb RAM...

10M

	bless -kmerlength 19 -read1 raw.10M.SRR797058_1.fastq \
	-read2 raw.10M.SRR797058_2.fastq -verify -notrim -prefix 10M
	
    Trinity --seqType fq --max_memory 20G --trimmomatic \
        --left /mnt/raw.10M.SRR797058_2.fastq  \
        --right /mnt/raw.10M.SRR797058_2.fastq \
        --CPU 16 --output trinity_10M_raw

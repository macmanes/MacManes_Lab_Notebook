Transcriptome error correction
--

    /mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_2.fastq.gz
    /mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_2.fastq.gz


	sudo mkfs -t ext4 /dev/xvdb
	sudo mount /dev/xvdb /mnt
	sudo chown -R ubuntu:ubuntu /mnt
	

	sudo bash
	apt-get update
	apt-get -y upgrade
	apt-get -y install sparsehash libboost-atomic1.55-dev libibnetdisc-dev libboost1.55-all-dev libboost1.55-dbg subversion tmux git curl bowtie libncurses5-dev samtools gcc make g++ python-dev unzip dh-autoreconf default-jre python-pip zlib1g-dev



	wget https://www.open-mpi.org/software/ompi/v1.8/downloads/openmpi-1.8.4.tar.gz
	tar -zxf openmpi-1.8.4.tar.gz
	cd openmpi-1.8.4/
	./configure --prefix="/home/$USER/.openmpi"
	make -j8
	make install
	export PATH=$PATH:/home/root/.openmpi/bin/
	export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/$USER/.openmpi/lib/

bless: 
lighter
bfc
sga

	
	

	cd $HOME
	git clone https://github.com/lh3/seqtk.git
	cd seqtk
	make
	PATH=$PATH:$(pwd)

	cd $HOME
	git clone https://github.com/lh3/bfc.git
	cd bfc
	make
	PATH=$PATH:$(pwd)
	
	cd $HOME
	wget http://downloads.sourceforge.net/project/bio-bwa/bwakit/bwakit-0.7.12_x64-linux.tar.bz2
	tar -jxf bwakit-0.7.12_x64-linux.tar.bz2
	cd bwa.kit
	PATH=$PATH:$(pwd)

	cd $HOME
	git clone https://github.com/mourisl/Lighter.git
	make -j8
	PATH=$PATH:$(pwd)/scripts
	
	cd $HOME
	git clone https://github.com/lh3/bwa.git
	cd bwa
	make -j4
	PATH=$PATH:$(pwd)
	
	cd $HOME
	wget http://downloads.sourceforge.net/project/bless-ec/bless.v0p24.tgz
	tar -zxf bless.v0p24.tgz
	cd v0p24
	make
	PATH:$PATH:$(pwd)
	
	mkdir -p /mnt/kmc/bin/
	sudo cp /home/ubuntu/v0p24/kmc/bin/kmc /mnt/kmc/bin/

mouse genome
	
make reference

	mkdir /mnt/genome
	cd /mnt/genome
	wget ftp://ftp.ensembl.org/pub/release-79/fasta/mus_musculus/dna/Mus_musculus.GRCm38.dna.chromosome.1.fa.gz
	gzip -d Mus_musculus.GRCm38.dna.chromosome.1.fa.gz
	bwa index -p mus Mus_musculus.GRCm38.dna.chromosome.1.fa
	
bless

	/home/root/.openmpi/bin/mpirun -np 16 bless -read1 raw.20M.SRR797058_1.fastq \
	-read2 raw.20M.SRR797058_2.fastq -prefix 20M_bless55 -kmerlength 55	

	/home/root/.openmpi/bin/mpirun -np 16 bless -read1 raw.20M.SRR797058_1.fastq \
	-read2 raw.20M.SRR797058_2.fastq -prefix 20M_bless33 -kmerlength 33
	

bwa mapping

	mkdir /mnt/bwa_mapping
	cd /mnt/bwa_mapping
	bwa mem -t16 ../genome/mus /mnt/raw.20M.SRR797058_1.fastq /mnt/raw.20M.SRR797058_2.fastq > 20M.raw.sam

	bwa mem -t16 ../genome/mus /mnt/20M_bless55.1.corrected.fastq.gz /mnt/20M_bless55.2.corrected.fastq.

	bwa mem -t16 ../genome/mus /mnt/20M_bless33.1.corrected.fastq /mnt/20M_bless33.2.corrected.fastq > 20M.bless33.sam
	
k8

	k8 ~/bfc/errstat.js 20M.bless55.sam 20M.raw.sam

    # reads:             40000000
    # perfect reads:     1902838
    # unmapped reads:    29219422
    # chimeric reads:    370718
    # chimeric events:   371521
    # reads w/ base err: 5959119
    # error bases:       26777572
    # clipped reads:     5287908
    # clipped bases:     279050125
    # better reads:      1862583
    # worse reads:       99880
    

	k8 ~/bfc/errstat.js 20M.bless33.sam 20M.raw.sam
	
    # reads:             40000000
    # perfect reads:     2014767
    # unmapped reads:    29158963
    # chimeric reads:    368648
    # chimeric events:   369392
    # reads w/ base err: 5844652
    # error bases:       26003521
    # clipped reads:     5239811
    # clipped bases:     278053353
    # better reads:      2307223
    # worse reads:       197733

lighter

	lighter -K 31 60000000 -r /mnt/raw.20M.SRR797058_1.fastq \
	-r /mnt/raw.20M.SRR797058_2.fastq -t 16
	
	bwa mem -t16 /mnt/genome/mus /mnt/raw.20M.SRR797058_1.cor.fq \
	/mnt/raw.20M.SRR797058_2.cor.fq > 20M.lighter31.sam


	k8 ~/bfc/errstat.js 20M.lighter31.sam 20M.raw.sam > table
	
    # reads:             40000000
    # perfect reads:     1878203
    # unmapped reads:    29034509
    # chimeric reads:    391436
    # chimeric events:   392439
    # reads w/ base err: 5922533
    # error bases:       26436534
    # clipped reads:     5513367
    # clipped bases:     294112709
    # better reads:      2166194
    # worse reads:       83052



bfc

	seqtk mergepe raw.20M.SRR797058_1.fastq raw.20M.SRR797058_2.fastq > inter.fq
	bfc -s 50m -k55 -t 16 inter.fq > corr.fq
	
	awk (https://github.com/ged-lab/khmer/issues/873)
	split-paired-reads.py

	bwa mem -t16 /mnt/genome/mus /mnt/corrected.fq.1 /mnt/corrected.fq.2 > 20M.bfc55.sam
	
	k8 ~/bfc/errstat.js 20M.bfc55.sam 20M.raw.sam > table

    # reads:             40000000
    # perfect reads:     2033584
    # unmapped reads:    29073457
    # chimeric reads:    387414
    # chimeric events:   388399
    # reads w/ base err: 5726859
    # error bases:       26274863
    # clipped reads:     5493765
    # clipped bases:     291986996
    # better reads:      2443002
    # worse reads:       90034
    
    
    bfc -s 50m -k33 -t 16 inter.fq > corr.fq
    

Gonna do the 100M read set
---

bless

	/home/root/.openmpi/bin/mpirun -np 16 ~/v0p24/bless -read1 raw.100M.SRR797058_1.fastq \
	-read2 raw.100M.SRR797058_2.fastq -prefix 100M_bless55 -kmerlength 55	

	/home/root/.openmpi/bin/mpirun -np 16 ~/v0p24/bless -read1 raw.100M.SRR797058_1.fastq \
	-read2 raw.100M.SRR797058_2.fastq -prefix 2100M_bless33 -kmerlength 33
	

bwa mapping

	mkdir /mnt/bwa_mapping
	cd /mnt/bwa_mapping
	bwa mem -t16 ../genome/mus /mnt/raw.100M.SRR797058_1.fastq /mnt/raw.100M.SRR797058_2.fastq \
	| gzip > 100M.raw.sam.gz


	bwa mem -t16 ../genome/mus /mnt/100M_bless55.1.corrected.fastq.gz /mnt/100M_bless55.2.corrected.fastq.gz \
	| gzip > 100M.bless55.sam.gz

	bwa mem -t16 ../genome/mus /mnt/100M_bless33.1.corrected.fastq.gz /mnt/100M_bless33.2.corrected.fastq.gz |
	| gzip > 100M.bless33.sam.gz



	k8 ~/bfc/errstat.js 100M.bless55.sam.gz 100M.raw.sam.gz  > table
	
    # reads:             200000000
    # perfect reads:     9,923,992
    # unmapped reads:    145876528
    # chimeric reads:    1860610
    # chimeric events:   1864467
    # reads w/ base err: 29200430
    # error bases:       132748547
    # clipped reads:     26562322
    # clipped bases:     1408470565
    # better reads:      10,315,307
    # worse reads:       771,255
    
	k8 ~/bfc/errstat.js 100M.bless33.sam.gz 100M.raw.sam.gz

    # reads:             200000000
    # perfect reads:     10,428,169
    # unmapped reads:    145465179
    # chimeric reads:    1860982
    # chimeric events:   1864896
    # reads w/ base err: 28646781
    # error bases:       128263100
    # clipped reads:     26507294
    # clipped bases:     1413132813
    # better reads:      11,991,342
    # worse reads:       1,658,332


Lighter 100M
--

	lighter -K 31 60000000 -r /mnt/raw.100M.SRR797058_1.fastq.gz \
	-r /mnt/raw.100M.SRR797058_2.fastq.gz -t 16
	

	mkdir /mnt/bwa_mapping
	cd /mnt/bwa_mapping
	
	bwa mem -t16 ../genome/mus /mnt/raw.100M.SRR797058_1.fastq.gz /mnt/raw.100M.SRR797058_2.fastq.gz \
	| gzip > 100M.raw.sam.gz


	bwa mem -t16 ../genome/mus /mnt/raw.100M.SRR797058_1.cor.fq.gz /mnt/raw.100M.SRR797058_2.cor.fq.gz \
	| gzip > 100M.lighter31.sam.gz


    # reads:             200000000
    # perfect reads:     9,347,302
    # unmapped reads:    145159777
    # chimeric reads:    1953884
    # chimeric events:   1958799
    # reads w/ base err: 29677760
    # error bases:       132383274
    # clipped reads:     27538598
    # clipped bases:     1469774504
    # better reads:      10,642,995
    # worse reads:       402,821


bfc55

    # reads:             200000000
    # perfect reads:     9,811,554
    # unmapped reads:    145333166
    # chimeric reads:    1934044
    # chimeric events:   1938785
    # reads w/ base err: 29047569
    # error bases:       132214049
    # clipped reads:     27625805
    # clipped bases:     1464690941
    # better reads:      11,454,234
    # worse reads:       433,424







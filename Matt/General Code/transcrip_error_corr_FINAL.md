Transcriptome error correction
--

khmer version 2.0
bwa 0.7.12-r1039
sga 0.10.13
lighter Lighter v1.0.7
bless v0.24
bfc r181
seqtc 1.0-r82-dirty
bwakit-0.7.12
seecer 0.1.3 (does not take gz files)






    /mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/100M_corr/raw.100M.SRR797058_2.fastq.gz
    /mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_1.fastq.gz
    /mnt/data3/macmanes/subsamp/20M_corr/raw.20M.SRR797058_2.fastq.gz
git

	sudo mkfs -t ext4 /dev/xvdb
	sudo mount /dev/xvdb /mnt
	sudo chown -R ubuntu:ubuntu /mnt
	

	sudo apt-get update && apt-get -y upgrade
	sudo apt-get -y install cmake sparsehash valgrind libboost-atomic1.55-dev libibnetdisc-dev ruby-full gsl-bin libgsl0-dev libgsl0ldbl libboost1.55-all-dev libboost1.55-dbg subversion tmux git curl bowtie libncurses5-dev samtools gcc make g++ python-dev unzip dh-autoreconf default-jre python-pip zlib1g-dev


	curl -LO https://www.open-mpi.org/software/ompi/v1.10/downloads/openmpi-1.10.0.tar.gz
	tar -zxf openmpi-1.10.0.tar.gz
	cd openmpi-1.10.0
	

 
	curl -LO https://www.open-mpi.org/software/ompi/v1.8/downloads/openmpi-1.8.4.tar.gz
	tar -zxf openmpi-1.8.4.tar.gz
	cd openmpi-1.8.4/
	./configure --prefix="/openmpi"
	make -j16
	sudo make install
	export PATH=$PATH:/openmpi/bin/
	export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/openmpi/lib/

bless: 
lighter
bfc
sga

	easy_install -U setuptools
	pip install khmer

	cd $HOME
	wget http://sb.cs.cmu.edu/seecer/downloads/SEECER-0.1.3.tar.gz
	tar -zxf SEECER-0.1.3.tar.gz
	cd SEECER-0.1.3/SEECER
	./configure
	make
	PATH=$PATH:$(pwd)/bin
	

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
	cd Lighter
	make -j8
	PATH=$PATH:$(pwd)
	
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

	cd $HOME
	wget http://www.canonware.com/download/jemalloc/jemalloc-3.4.1.tar.bz2
	tar -jxf jemalloc-3.4.1.tar.bz2
	cd jemalloc-3.4.1 && ./configure && make -j4 && cd ../
	git clone git://github.com/pezmaster31/bamtools.git
	cd bamtools && mkdir build && cd build && cmake .. && make	
	git clone git://github.com/jts/sga
	cd sga/src && ./autogen.sh &&./configure --with-sparsehash=/home/ubuntu/sparsehash-2.0.2 \
	--with-bamtools=/home/ubuntu/bamtools \
	--with-jemalloc=/home/ubuntu/jemalloc-3.4.1/lib && make -j6 && sudo make all install
	
	cd 
	git clone https://github.com/mourisl/Rcorrector.git
	cd Rcorrector
	make && sudo make all install
	PATH:$PATH:$(pwd)

	cd
	git clone https://github.com/trinityrnaseq/trinityrnaseq.git
	cd trinityrnaseq
	make -j6
	PATH:$PATH:$(pwd)


mouse genome
	
make reference

	mkdir /mnt/genome
	cd /mnt/genome
	wget ftp://ftp.ensembl.org/pub/release-79/fasta/mus_musculus/dna/Mus_musculus.GRCm38.dna.chromosome.1.fa.gz
	bwa index -p mus Mus_musculus.GRCm38.dna.chromosome.1.fa.gz
	
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


SGA
--

	/home/ubuntu/sga/src/SGA/sga preprocess -p 1 /mnt/raw.20M.SRR797058_1.fastq.gz /mnt/raw.20M.SRR797058_2.fastq.gz | gzip -1 > out.pe.fq.gz
	/home/ubuntu/sga/src/SGA/sga index -a ropebwt -t 8 --no-reverse out.20M.SGA.pe.fq.gz
	/home/ubuntu/sga/src/SGA/sga correct -t 8 -k 55 --learn out.20M.SGA.pe.fq.gz


	cd /mnt/mapping

	bwa mem -t16 ../genome/mus /mnt/raw.20M.SRR797058_1.fastq.gz /mnt/raw.20M.SRR797058_2.fastq.gz \
	| gzip > 20M.raw.sam.gz

	k8 ~/bfc/errstat.js 20M.SGA55.sam.gz 20M.raw.sam.gz  > table

    # reads:             33486854
    # perfect reads:     1,543,738
    # unmapped reads:    24410947
    # chimeric reads:    320410
    # chimeric events:   321238
    # reads w/ base err: 4952410
    # error bases:       22478052
    # clipped reads:     4599337
    # clipped bases:     242303001
    # better reads:      7,805,357
    # worse reads:       7,633,699

	k8 ~/bfc/errstat.js 20M.SGA33.sam.gz 20M.raw.sam.gz  > table

    # reads:             33486854
    # perfect reads:     1489045
    # unmapped reads:    24378787
    # chimeric reads:    323725
    # chimeric events:   324572
    # reads w/ base err: 5025140
    # error bases:       22435348
    # clipped reads:     4610195
    # clipped bases:     243991080
    # better reads:      7830762
    # worse reads:       7632490

<<<<<<< Updated upstream
	k8 ~/bfc/errstat.js 100M.SGA33.sam.gz 100M.raw.sam.gz | tail -20
=======

k8 ~/bfc/errstat.js 100M.SGA33.sam.gz 100M.raw.sam.gz  > table
>>>>>>> Stashed changes

    # reads:             167447694
    # perfect reads:     7079803
    # unmapped reads:    122099171
    # chimeric reads:    1600880
    # chimeric events:   1604674
    # reads w/ base err: 25688949
    # error bases:       113449996
    # clipped reads:     22866030
    # clipped bases:     1202474283
    # better reads:      38997782
    # worse reads:       38199036
<<<<<<< Updated upstream
    



	bwa mem -t16 ../genome/mus /mnt/sga/100M.out.SGA55.pe.fq.gz.1 /mnt/sga/100M.out.SGA55.pe.fq.gz.2 \
	| gzip > 100M.SGA55.sam.gz

    k8 ~/bfc/errstat.js 100M.SGA55.sam.gz 100M.raw.sam.gz | tail -20
    
    # reads:             167447694
    # perfect reads:     7168656
    # unmapped reads:    122197057
    # chimeric reads:    1590052
    # chimeric events:   1593782
    # reads w/ base err: 25496358
    # error bases:       113427762
    # clipped reads:     22871670
    # clipped bases:     1199875980
    # better reads:      38917160
    # worse reads:       38207285
    



SEECER

	~/SEECER-0.1.3/SEECER/bin/run_seecer.sh -t . -k 31 ../raw.10M.SRR797058_1.fastq ../raw.10M.SRR797058_2.fastq
	


    k8 ~/bfc/errstat.js 10M.seecer31.sam.gz 10M.raw.sam.gz | tail -20
    
    # reads:             20000000
    # perfect reads:     1072867
    # unmapped reads:    14543190
    # chimeric reads:    191814
    # chimeric events:   192283
    # reads w/ base err: 2811791
    # error bases:       13061261
    # clipped reads:     2744455
    # clipped bases:     145834784
    # better reads:      1241908
    # worse reads:       59882
    
RAW READ ANALYSIS
--

    k8 ~/bfc/errstat.js  10M.raw.sam.gz | tail -20
    
    # reads:             20000000
    # perfect reads:     717061
    # unmapped reads:    14654974
    # chimeric reads:    185905
    # chimeric events:   186342
    # reads w/ base err: 3226227
    # error bases:       14105615
    # clipped reads:     2721570
    # clipped bases:     139446263
    
    
    k8 ~/bfc/errstat.js  20M.raw.sam.gz | tail -20
    # reads:             40000000
    # perfect reads:     1428466
    # unmapped reads:    29311281
    # chimeric reads:    373601
    # chimeric events:   374488
    # reads w/ base err: 6454755
    # error bases:       28223069
    # clipped reads:     5444611
    # clipped bases:     278966692
    
    k8 ~/bfc/errstat.js  100M.raw.sam.gz | tail -20
    # reads:             200000000
    # perfect reads:     7153105
    # unmapped reads:    146551366
    # chimeric reads:    1863889
    # chimeric events:   1868108
    # reads w/ base err: 32265352
    # error bases:       141119210
    # clipped reads:     27209498
    # clipped bases:     1394228538
=======
>>>>>>> Stashed changes


	cd /mnt/bless

	/home/root/.openmpi/bin/mpirun -np 16 bless -read1 /mnt/raw.10M.SRR797058_1.fastq \
	-read2 /mnt/raw.10M.SRR797058_2.fastq -prefix 10M_bless55 -kmerlength 55 

	/home/root/.openmpi/bin/mpirun -np 16 bless -read1 /mnt/raw.10M.SRR797058_1.fastq \
	-read2 /mnt/raw.10M.SRR797058_2.fastq -prefix 10M_bless33 -kmerlength 33


	cd /mnt/lighter

	lighter -K 31 60000000 -r /mnt/raw.10M.SRR797058_1.fastq \
	-r /mnt/raw.10M.SRR797058_2.fastq -t 16

	cd /mnt/bfc

	seqtk mergepe /mnt/raw.10M.SRR797058_1.fastq /mnt/raw.10M.SRR797058_2.fastq > inter.fq
	bfc -s 50m -k55 -t 16 inter.fq > bfc55.corr.fq
	bfc -s 50m -k33 -t 16 inter.fq > bfc33.corr.fq

	awk '{print $1}' bfc55.corr.fq > bfc55.corr.fastq
	awk '{print $1}' bfc33.corr.fq > bfc33.corr.fastq

	split-paired-reads.py bfc55.corr.fastq
	split-paired-reads.py bfc33.corr.fastq

	cd /mnt/sga/

	/home/ubuntu/sga/src/SGA/sga preprocess -p 1 /mnt/raw.10M.SRR797058_1.fastq.gz /mnt/raw.10M.SRR797058_2.fastq.gz | gzip -1 > 10M.out.pe.fq.gz
	/home/ubuntu/sga/src/SGA/sga index -a ropebwt -t 8 --no-reverse 10M.out.pe.fq.gz
	/home/ubuntu/sga/src/SGA/sga correct -t 8 -k 55 --learn 10M.out.pe.fq.gz



	cd /mnt/bless

	bwa mem -t16 /mnt/genome/mus /mnt/bless/10M_bless55.1.corrected.fastq /mnt/bless/10M_bless55.2.corrected.fastq \
	| gzip > 10M.bless55.sam.gz

	bwa mem -t16 /mnt/genome/mus /mnt/bless/10M_bless33.1.corrected.fastq /mnt/bless/10M_bless33.2.corrected.fastq \
	| gzip > 10M.bless33.sam.gz

	cd /mnt/lighter

	bwa mem -t16 /mnt/genome/mus raw.10M.SRR797058_1.cor.fq raw.10M.SRR797058_2.cor.fq \
	| gzip > 10M.lighter31.sam.gz

	cd /mnt/bfc

	bwa mem -t16 /mnt/genome/mus bfc55.corr.fastq.1 bfc55.corr.fastq.2 \
	| gzip > 10M.bfc55.sam.gz

	bwa mem -t16 /mnt/genome/mus bfc33.corr.fastq.1 bfc33.corr.fastq.2 \
	| gzip > 10M.bfc33.sam.gz

	cd /mnt/sga

	bwa mem -t16 /mnt/genome/mus 10M.SGA55.out.pe.ec.fa.1 10M.SGA55.out.pe.ec.fa.2 \
	| gzip > 10M.sga55.sam.gz

	bwa mem -t16 /mnt/genome/mus 10M.SGA33.out.pe.ec.fa.1 10M.SGA33.out.pe.ec.fa.2 \
	| gzip > 10M.sga33.sam.gz



	k8 ~/bfc/errstat.js bless/10M.bless55.sam.gz mapping/10M.raw.sam.gz | tail -20

	# reads:             20000000
	# perfect reads:     940122
	# unmapped reads:    14616126
	# chimeric reads:    183860
	# chimeric events:   184256
	# reads w/ base err: 3000477
	# error bases:       13426097
	# clipped reads:     2642702
	# clipped bases:     139127391
	# better reads:      875529
	# worse reads:       45918

	k8 ~/bfc/errstat.js bless/10M.bless33.sam.gz mapping/10M.raw.sam.gz | tail -20

	# reads:             20000000
	# perfect reads:     987534
	# unmapped reads:    14591976
	# chimeric reads:    182225
	# chimeric events:   182652
	# reads w/ base err: 2957997
	# error bases:       13084776
	# clipped reads:     2616376
	# clipped bases:     138413822
	# better reads:      1075067
	# worse reads:       82014

	k8 ~/bfc/errstat.js lighter/10M.lighter31.sam.gz mapping/10M.raw.sam.gz | tail -20

	# reads:             20000000
	# perfect reads:     974037
	# unmapped reads:    14514662
	# chimeric reads:    194564
	# chimeric events:   195053
	# reads w/ base err: 2924919
	# error bases:       13122575
	# clipped reads:     2754647
	# clipped bases:     147043308
	# better reads:      1174719
	# worse reads:       42747


	k8 ~/bfc/errstat.js bfc/10M.bfc33.sam.gz mapping/10M.raw.sam.gz | tail -20

	# reads:             20000000
	# perfect reads:     1069699
	# unmapped reads:    14465127
	# chimeric reads:    197867
	# chimeric events:   198363
	# reads w/ base err: 2817927
	# error bases:       12708561
	# clipped reads:     2775120
	# clipped bases:     149241539
	# better reads:      1476812
	# worse reads:       52445

	k8 ~/bfc/errstat.js bfc/10M.bfc55.sam.gz mapping/10M.raw.sam.gz | tail -20

	# reads:             20000000
	# perfect reads:     1022925
	# unmapped reads:    14540224
	# chimeric reads:    192396
	# chimeric events:   192864
	# reads w/ base err: 2859874
	# error bases:       13130166
	# clipped reads:     2740286
	# clipped bases:     145557672
	# better reads:      1221951
	# worse reads:       44290

	k8 ~/bfc/errstat.js sga/10M.sga55.sam.gz mapping/10M.raw.sam.gz | tail -20

	# reads:             16741894
	# perfect reads:     772868
	# unmapped reads:    12204729
	# chimeric reads:    159515
	# chimeric events:   159895
	# reads w/ base err: 2477273
	# error bases:       11248355
	# clipped reads:     2302145
	# clipped bases:     121038701
	# better reads:      3902756
	# worse reads:       3815741


	k8 ~/bfc/errstat.js sga/10M.sga33.sam.gz mapping/10M.raw.sam.gz | tail -20




	cd /mnt/bfc

	seqtk mergepe /mnt/raw.20M.SRR797058_1.fastq /mnt/raw.20M.SRR797058_2.fastq > inter.fq
	bfc -s 50m -k33 -t 16 inter.fq > bfc33.corr.fq

	awk '{print $1}' bfc33.corr.fq > bfc33.corr.fastq

	split-paired-reads.py bfc33.corr.fastq

	bwa mem -t16 /mnt/genome/mus bfc33.corr.fastq.1 bfc33.corr.fastq.2 \
	| gzip > 20M.bfc33.sam.gz

	k8 ~/bfc/errstat.js bfc/20M.bfc33.sam.gz mapping/20M.raw.sam.gz | tail -20


	# reads:             40000000
	# perfect reads:     2107983
	# unmapped reads:    28932073
	# chimeric reads:    397368
	# chimeric events:   398394
	# reads w/ base err: 5660601
	# error bases:       25556896
	# clipped reads:     5578768
	# clipped bases:     299573690
	# better reads:      2860000
	# worse reads:       102660

<<<<<<< HEAD
    ~/bwa.kit/k8 ~/bfc/errstat.js bfc/1000M.bfc33.sam.gz mapping/100M.raw.sam.gz | tail -20
    
    # reads:             200000000
    # perfect reads:     9875615
    # unmapped reads:    144756657
    # chimeric reads:    1978445
    # chimeric events:   1983433
    # reads w/ base err: 29002009
    # error bases:       130474785
    # clipped reads:     28117633
    # clipped bases:     1501694424
    # better reads:      12228941
    # worse reads:       461217


	~/SEECER-0.1.3/SEECER/bin/run_seecer.sh -t . -k 31 ../raw.20M.SRR797058_1.fastq ../raw.20M.SRR797058_2.fastq

	bwa mem -t16 /mnt/genome/mus raw.20M.SRR797058_1.fastq_corrected.fa raw.20M.SRR797058_1.fastq_corrected.fa \
	| gzip > 20M.seecer31.sam.gz
	
	~/bwa.kit/k8 ~/bfc/errstat.js seecer/20M.seecer31.sam.gz mapping/20M.raw.sam.gz | tail -20
	
    # reads:             40000000
    # perfect reads:     2151034
    # unmapped reads:    29081264
    # chimeric reads:    385987
    # chimeric events:   386943
    # reads w/ base err: 5613509
    # error bases:       26090041
    # clipped reads:     5492995
    # clipped bases:     292174910
    # better reads:      2521018
    # worse reads:       127985

=======
	bwa mem -t16 /mnt/genome/mus bfc33.corr.fastq.1 bfc33.corr.fastq.2 \
	| gzip > 1000M.bfc33.sam.gz
>>>>>>> origin/master

100M seecer
--

	bwa mem -t30 /mnt/genome/mus raw.100M.SRR797058_1.fastq_corrected.fa.gz raw.100M.SRR797058_2.fastq_corrected.fa.gz \
	| gzip > 1000M.seecer31.sam.gz



    # reads:             200000000
    # perfect reads:     10897587
    # unmapped reads:    145342275
    # chimeric reads:    1927630
    # chimeric events:   1932231
    # reads w/ base err: 27940421
    # error bases:       129989815
    # clipped reads:     27469520
    # clipped bases:     1463688247
    # better reads:      13073703
    # worse reads:       678161


50M read analysis
--

	bwa mem -t16 /mnt/genome/mus raw/raw.50M.SRR797058_1.fastq.gz raw/raw.50M.SRR797058_2.fastq.gz \
	| gzip > 50M.raw.sam.gz

	cd lighter
	
	lighter -K 31 60000000 -r ../raw/raw.50M.SRR797058_1.fastq.gz \
	-r ../raw/raw.50M.SRR797058_2.fastq.gz -t 16

	bwa mem -t16 /mnt/genome/mus raw.50M.SRR797058_1.cor.fq raw.50M.SRR797058_2.cor.fq \
	| gzip > 50M.lighter31.sam.gz



	cd /mnt/bfc

	seqtk mergepe ../raw/raw.50M.SRR797058_1.fastq.gz ../raw/raw.50M.SRR797058_2.fastq.gz > inter.fq
	bfc -s 50m -k55 -t 16 inter.fq > bfc55.corr.fq
	bfc -s 50m -k33 -t 16 inter.fq > bfc33.corr.fq

	awk '{print $1}' bfc55.corr.fq > bfc55.corr.fastq
	awk '{print $1}' bfc33.corr.fq > bfc33.corr.fastq

	split-paired-reads.py bfc55.corr.fastq
	split-paired-reads.py bfc33.corr.fastq

	bwa mem -t16 /mnt/genome/mus bfc55.corr.fastq.1 bfc55.corr.fastq.2 \
	| gzip > 50M.bfc55.sam.gz

	bwa mem -t16 /mnt/genome/mus bfc33.corr.fastq.1 bfc33.corr.fastq.2 \
	| gzip > 50M.bfc33.sam.gz


run2

    cd /mnt/raw
    gzip -d raw.50M.SRR797058_1.fastq.gz
    gzip -d raw.50M.SRR797058_2.fastq.gz
    
    mkdir /mnt/bless
    cd /mnt/bless
    /openmpi/bin/mpirun --allow-run-as-root -np 16 ~/v0p24/bless -read1 /mnt/raw/raw.50M.SRR797058_1.fastq \
    -read2 /mnt/raw/raw.50M.SRR797058_2.fastq -prefix 50M_bless55 -kmerlength 55
    
    /openmpi/bin/mpirun --allow-run-as-root -np 16 ~/v0p24/bless -read1 /mnt/raw/raw.50M.SRR797058_1.fastq \
    -read2 /mnt/raw/raw.50M.SRR797058_2.fastq -prefix 50M_bless33 -kmerlength 33
    
    mkdir /mnt/sga
    cd /mnt/sga
    
    #/home/ubuntu/bamtools/build/sga/src/SGA/sga preprocess -p 1 /mnt/raw/raw.50M.SRR797058_1.fastq.gz \
    #/mnt/raw/raw.50M.SRR797058_2.fastq.gz | gzip -1 > out.pe.fq.gz
    
    /home/ubuntu/bamtools/build/sga/src/SGA/sga index -a ropebwt -t 16 --no-reverse out.pe.fq.gz
    
    /home/ubuntu/bamtools/build/sga/src/SGA/sga correct -t 16 -k 55 --learn out.pe.fq.gz -o sga.55.fq
    
    /home/ubuntu/bamtools/build/sga/src/SGA/sga correct -t 16 -k 33 --learn out.pe.fq.gz -o sga.33.fq
    
    
run3

	cd /mnt/bless/
    bwa mem -t16 /mnt/genome/mus 50M_bless55.1.corrected.fastq 50M_bless55.2.corrected.fastq \
    | gzip > 50M.bless55.sam.gz
    
    bwa mem -t16 /mnt/genome/mus 50M_bless33.1.corrected.fastq 50M_bless33.2.corrected.fastq \
    | gzip > 50M.bless33.sam.gz

	split-paired-reads.py sga.55.fq
	split-paired-reads.py sga.33.fq
	
	bwa mem -t16 /mnt/genome/mus sga.55.fq.1 sga.55.fq.2 \
	| gzip > 50M.sga55.sam.gz

	bwa mem -t16 /mnt/genome/mus sga.33.fq.1 sga.33.fq.2 \
	| gzip > 50M.sga33.sam.gz



STATS
--

	~/bwa.kit/k8 ~/bfc/errstat.js raw/50M.raw.sam.gz | tail -20
	~/bwa.kit/k8 ~/bfc/errstat.js bfc/50M.bfc55.sam.gz raw/50M.raw.sam.gz | tail -17
	~/bwa.kit/k8 ~/bfc/errstat.js lighter/50M.lighter31.sam.gz raw/50M.raw.sam.gz | tail -17

	~/bwa.kit/k8 ~/bfc/errstat.js bless/50M.bless55.sam.gz raw/50M.raw.sam.gz | tail -17
	~/bwa.kit/k8 ~/bfc/errstat.js bless/50M.bless33.sam.gz raw/50M.raw.sam.gz | tail -17
	~/bwa.kit/k8 ~/bfc/errstat.js sga/50M.sga33.sam.gz raw/50M.raw.sam.gz | tail -17
	~/bwa.kit/k8 ~/bfc/errstat.js sga/50M.sga55.sam.gz raw/50M.raw.sam.gz | tail -17








	cd /mnt/bfc/

	bwa mem -t16 /mnt/genome/mus bfc33.corr.fastq.1 bfc33.corr.fastq.2 \
	| gzip > 50M.bfc33.sam.gz

	bwa mem -t16 /mnt/genome/mus bfc55.corr.fastq.1 bfc55.corr.fastq.2 \
	| gzip > 50M.bfc55.sam.gz
	

50M seecer
--

	~/SEECER-0.1.3/SEECER/bin/run_seecer.sh -t . -k 31 ../raw/raw.50M.SRR797058_1.fastq ../raw/raw.50M.SRR797058_2.fastq

bwa
	
	PATH=$PATH:/home/ubuntu/bfc:/home/ubuntu/bwa.kit:/home/ubuntu/bwa

	bwa mem -t16 /mnt/genome/mus raw.50M.SRR797058_1.fastq_corrected.fa \
	raw.50M.SRR797058_2.fastq_corrected.fa \
	| gzip > 50M.seecer31.sam.gz

	cd ../

	~/bwa.kit/k8 ~/bfc/errstat.js seecer/50M.seecer31.sam.gz raw/50M.raw.sam.gz | tail -17

	
ALLPATHS
--

	ErrorCorrectReads.pl \
	MAX_MEMORY_GB=14 \
	PHRED_ENCODING=33 \
	READS_OUT=alp_corr.fq \
	PAIRED_READS_A_IN=/mnt/read_error_corr/reads/subsamp_1.fastq \
	PAIRED_READS_B_IN=/mnt/read_error_corr/reads/subsamp_2.fastq \
	REMOVE_DODGY_READS=0
	



	ErrorCorrectReads.pl \
	MAX_MEMORY_GB=14 \
	PHRED_ENCODING=33 \
	READS_OUT=alp_corr.fq \
	UNPAIRED_READS_IN=/mnt/read_error_corr/reads/SRR797058_1.fastq \
	REMOVE_DODGY_READS=0
	


transrate
--

	/share/transrate-1.0.0-linux-x86_64/transrate -t 30 \
	--assembly trinity_10M.P2.raw.Trinity.fasta,\
	trinity_10M.P2.bfc33.Trinity.fasta,\
	trinity_20M.P2.raw.Trinity.fasta,\
	trinity_20M.P2.bfc33.Trinity.fasta,\
	trinity_20M.P2.bfc33.first.Trinity.fasta \
	--left /mnt/data3/macmanes/feeding/SRR797058.P2_1P.fq \
	--right /mnt/data3/macmanes/feeding/SRR797058.P2_2P.fq \
	--reference /mnt/data3/macmanes/feeding/Mus_musculus.GRCm38.pep.all.fa 
	
for asembly:
--

10 and 20M bfc

50 and 100 seecer

subsamp, trimmomatic (seecer output fa)

    java -Xmx10g -jar \
    ~/trinityrnaseq/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 16 -baseout subsamp50.P2.fq \
    /mnt/reads/subsamp_1.fastq \
    /mnt/reads/subsamp_2.fastq  \
    ILLUMINACLIP:/mnt/scripts/barcodes.fa:2:40:15 \
    LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:25
    
	run_seecer.sh -t . -k 31 /mnt/reads/subsamp100.P2_1P.fq /mnt/reads/subsamp100.P2_2P.fq
	
	cd /mnt/trinity_100M \
	Trinity --seqType fq --max_memory 10G \
	--left /mnt/reads/subsamp100.P2_1P.fq \
	--right /mnt/reads/subsamp100.P2_2P.fq \
	--CPU 16 --output trinity_100M.P2.raw --inchworm_cpu 10 --full_cleanup \

	


in `/mnt/data1/error`

BUSCO on AWS:


```
for i in $(ls /mnt/assemblies/*fasta); do
   F=`basename $i .fasta`;
   python3 ~/BUSCO_v1.1b1/BUSCO_v1.1b1.py -g $i -m Trans --cpu 32 -o $F -l vertebrata;
   gzip $i &
done
```

pull out prefect reads
--

```
for i in $(ls 2M*); do echo $i; sed -n '2p' $i ; done
```


pull out better reads
--

```
for i in $(ls 2M*); do echo $i; sed -n '10p' $i ; done
```


```
export AUGUSTUS_CONFIG_PATH=/home/ubuntu/augustus-3.0.2/config/
PATH=$PATH:/home/ubuntu/BUSCO_v1.1b1:/home/ubuntu/augustus-3.0.2/bin:/home/ubuntu/augustus-3.0.2/scripts
```




SETUP MACHINE
--

``

sudo apt-get update && sudo apt-get -y upgrade


sudo apt-get -y install hmmer cmake tmux git curl bowtie libncurses5-dev samtools gcc make ncbi-blast+ g++ python-dev libboost-iostreams-dev libboost-system-dev libboost-filesystem-dev

cd
curl -LO http://busco.ezlab.org/files/BUSCO_v1.1b1.tar.gz
tar -zxf BUSCO_v1.1b1.tar.gz
cd BUSCO_v1.1b1
curl -LO http://busco.ezlab.org/files/vertebrata_buscos.tar.gz
tar -zxf vertebrata_buscos.tar.gz
PATH=$PATH:$(pwd)


cd
curl -LO http://bioinf.uni-greifswald.de/augustus/binaries/old/augustus-3.0.2.tar.gz
tar -zxf augustus-3.0.2.tar.gz
cd augustus-3.0.2/
make -j7
PATH=$PATH:$(pwd)/bin:$(pwd)/scripts
export AUGUSTUS_CONFIG_PATH=/home/ubuntu/augustus-3.0.2/config/

sudo mount /dev/xvdf /mnt  
sudo chown -R ubuntu:ubuntu /mnt


cd /mnt/busco

tmux new -s busco


in `/mnt/data3/macmanes/error/busco`

```
for i in $(ls ../assemblies/trin*fasta); do
   F=`basename $i .fasta`;
   python3 /share/BUSCO_v1.1b1/BUSCO_v1.1b1.py -g $i -m Trans --cpu 52 -o $F -l vertebrata;
done
```
transrate



```
transrate -t 52 -a \
../assemblies/trinity_1M.P2.raw.Trinity.fasta,\
../assemblies/trinity_2M.P2.raw.Trinity.fasta,\
../assemblies/trinity_5M.P2.raw.Trinity.fasta,\
../assemblies/trinity_10M.P2.raw.Trinity.fasta,\
../assemblies/trinity_20M.P2.raw.Trinity.fasta,\
../assemblies/trinity_40M.P2.raw.Trinity.fasta,\
../assemblies/trinity_60M.P2.raw.Trinity.fasta,\
../assemblies/trinity_80M.P2.raw.Trinity.fasta,\
../assemblies/trinity_100M.P2.raw.Trinity.fasta,\
../assemblies/1M.trinity_bfc31.Trinity.fasta,\
../assemblies/2M.trinity_bfc31.Trinity.fasta,\
../assemblies/5M.trinity_bfc31.Trinity.fasta,\
../assemblies/10M.trinity_bfc31.Trinity.fasta,\
../assemblies/20M.trinity_bfc31.Trinity.fasta,\
../assemblies/40M.trinity_bfc31.Trinity.fasta,\
../assemblies/60M.seecer.trinity.Trinity.fasta,\
../assemblies/80M.seecer.trinity.Trinity.fasta,\
../assemblies/100M.seecer.trinity.Trinity.fasta \
-l ../reads/SRR797058_1.fastq.gz \
-r ../reads/SRR797058_2.fastq.gz


```




















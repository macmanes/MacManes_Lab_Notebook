in `/mnt/data0/macmanes/pacbio`

Make config file:

	fastqToCA -insertsize 300 100 -type sanger -innie \
	-mates \
	/mnt/data3/macmanes/pero_genome/131008/peroL1_1P.fq,\
	/mnt/data3/macmanes/pero_genome/131008/peroL1_2P.fq \
	-mates \
	/mnt/data3/macmanes/pero_genome/131008/peroL2_1P.fq,\
	/mnt/data3/macmanes/pero_genome/131008/peroL2_2P.fq \
	-mates \
	/mnt/data3/macmanes/pero_genome/131023/peroL3_1P.fq,\
	/mnt/data3/macmanes/pero_genome/131023/peroL3_2P.fq \
	-mates \
	/mnt/data3/macmanes/pero_genome/131219/peroL4_1P.fq,\
	/mnt/data3/macmanes/pero_genome/131219/peroL4_2P.fq \
	-mates \
	/mnt/data3/macmanes/pero_genome/131219/peroL5_1P.fq,\
	/mnt/data3/macmanes/pero_genome/131219/peroL5_2P.fq \
	-libraryname illumina > illumina.frg
	
May 15
--

Correct PacBio Reads

	nohup /share/wgs-8.1/Linux-amd64/bin/pacBioToCA -length 5000 -partitions 50 \
	-l pacbio -t 20 -s pacbio.spec \
	-genomeSize 2600000000 \
	-fastq /mnt/data3/macmanes/pacbio/raw.pacbio.reads/fastq/all.pb.fastq \
	illumina.frg > pbcr.out 2>&1 &
	
pacbio.spec

    \# original asm settings
    utgErrorRate = 0.25
    utgErrorLimit = 6.5
    
    cnsErrorRate = 0.25
    cgwErrorRate = 0.25
    ovlErrorRate = 0.25
    
    merSize=14
    
    merylMemory = 128000
    merylThreads = 8
    
    ovlStoreMemory = 8192
    
    # grid info
    useGrid = 0
    scriptOnGrid = 0
    frgCorrOnGrid = 0
    ovlCorrOnGrid = 0
    
    ovlHashBits = 24
    ovlThreads = 2
    ovlHashBlockLength = 20000000
    ovlRefBlockSize =  50000000
    
    frgCorrThreads = 2
    frgCorrBatchSize = 100000
    
    ovlCorrBatchSize = 100000
    
    ovlConcurrency = 6
    cnsConcurrency = 16
    frgCorrConcurrency = 8
    ovlCorrConcurrency = 16
    cnsConcurrency = 16
Pero genome NYGC work
--

    cat \
    /mnt/data3/macmanes/pero_genome/131008/peroL1_1P.fq \
    /mnt/data3/macmanes/pero_genome/131219/peroL5_1P.fq \
    /mnt/data3/macmanes/pero_genome/131023/peroL3_1P.fq \
    /mnt/data3/macmanes/pero_genome/131008/peroL2_1P.fq \
    /mnt/data3/macmanes/pero_genome/131219/peroL4_1P.fq > hcgs.300.1.fq
    
    cat \
    /mnt/data3/macmanes/pero_genome/131008/peroL1_2P.fq \
    /mnt/data3/macmanes/pero_genome/131219/peroL5_2P.fq \
    /mnt/data3/macmanes/pero_genome/131023/peroL3_2P.fq \
    /mnt/data3/macmanes/pero_genome/131008/peroL2_2P.fq \
    /mnt/data3/macmanes/pero_genome/131219/peroL4_2P.fq > hcgs.300.2.fq

MP data

    /mnt/data3/macmanes/pero-mate-pair/peer3kb.clipped.1.fq
    /mnt/data3/macmanes/pero-mate-pair/peer3kb.clipped.2.fq
    
    /mnt/data3/macmanes/pero-mate-pair/peer7kb.clipped.1.fq
    /mnt/data3/macmanes/pero-mate-pair/peer7kb.clipped.2.fq

8kb MP data from NYGC

	nextclip -e -n 281635903 -i <(gzip -cd Pero360-8K-10K_ATGTCA_AC6718ANXX_L006_001.R1.fastq.gz) \
	-j <(gzip -cd Pero360-5K.R2.fastq.gz) -o Pero360_8kb

5kb MP data from NYGC

	nextclip -n 331635903 -i <(gzip -cd Pero360-5K.R1.fastq.gz) \
	-j <(gzip -cd Pero360-5K.R2.fastq.gz) -o Pero360_5kb


    SUMMARY
    
        Strict match parameters: 34, 18
            Minimum read size: 25
                    Trim ends: 19
    
            Number of read pairs: 388169206
    Number of duplicate pairs: 136734512 35.23 %
    Number of pairs containing N: 953706    0.25 %
    
    R1 Num reads with adaptor: 141406189 36.43 %
    R1 Num with external also: 986042    0.25 %
        R1 long adaptor reads: 95010130  24.48 %
            R1 reads too short: 46396059  11.95 %
        R1 Num reads no adaptor: 246763017 63.57 %
    R1 no adaptor but external: 482876    0.12 %
    
    R2 Num reads with adaptor: 139471629 35.93 %
    R2 Num with external also: 990535    0.26 %
        R2 long adaptor reads: 93652434  24.13 %
            R2 reads too short: 45819195  11.80 %
        R2 Num reads no adaptor: 248697577 64.07 %
    R2 no adaptor but external: 461670    0.12 %
    
    Total pairs in category A: 18035296  4.65 %
            A pairs long enough: 13872720  3.57 %
            A pairs too short: 4162576   1.07 %
    A external clip in 1 or both: 453       0.00 %
        A bases before clipping: 4508824000
        A total bases written: 2008805244
    
    Total pairs in category B: 121436333 31.28 %
            B pairs long enough: 77780428  20.04 %
            B pairs too short: 43655905  11.25 %
    B external clip in 1 or both: 16652     0.00 %
        B bases before clipping: 30359083250
        B total bases written: 13081640901
    
    Total pairs in category C: 123370893 31.78 %
            C pairs long enough: 79122201  20.38 %
            C pairs too short: 44248692  11.40 %
    C external clip in 1 or both: 13155     0.00 %
        C bases before clipping: 30842723250
        C total bases written: 13316001487
    
    Total pairs in category D: 125326684 32.29 %
            D pairs long enough: 124865156 32.17 %
            D pairs too short: 461528    0.12 %
    D external clip in 1 or both: 480588    0.12 %
        D bases before clipping: 31331671000
        D total bases written: 26470266432
    
            Total usable pairs: 170775349 44.00 %
                All long enough: 295640505 76.16 %
        All categories too short: 92528701  23.84 %
        Duplicates not written: 0 0.00 %
            Overall GC content: 41.68 %


Trimmomatic PE data

    java -Xmx300g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 40 -baseout Pero360_550bp.gz \
    Pero360-WGS-550_GTGAAA_AC6718ANXX_L005_001.R1.fastq.gz \
    Pero360-WGS-550_GTGAAA_AC6718ANXX_L005_001.R2.fastq.gz \
    ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
    LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:75
    
and 

    java -Xmx300g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 40 -baseout Pero360_550bp.lane2.gz \
    Pero360-WGS-550_GTGAAA-_AC62CPANXX_L003_001.R1.fastq.gz \
    Pero360-WGS-550_GTGAAA-_AC62CPANXX_L003_001.R2.fastq.gz \
    ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
    LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:75
    






AllPaths Run

in_groups.csv
--
	file_name, library_name, group_name
	/mouse/pero_genome/hcgs.300.*.cor.fq,L1,      frags1
	/mouse/pero_genome/nygc.550.*.cor.fq.gz,L2,      frags2
	/mouse/pero_genome/peer3kb.clipped.*.fq,3kb,      jumps3
	/mouse/pero_genome/peer7kb.clipped.*.fq,7kb,      jumps7
	/mouse/pero_genome/peer5kb.clipped.*.fq,5kb,      jumps5
	/mouse/pero_genome/peer8kb.clipped.*.fq,8kb,      jumps8
	

in_libs.csv
--

	library_name, project_name, organism_name,     type, paired, frag_size, frag_stddev, insert_size, insert_stddev, read_orientation, genomic_start, genomic_end
	L1,peer_genome,peer, fragment,1,300,50,            ,              ,           inward,0,0
	L2,peer_genome,peer, fragment,1,550,50,            ,              ,           inward,0,0
	3kb,peer_genome,peer,  jumping,1,          ,            ,3000,500,          outward,0,0
	7kb,peer_genome,peer,  jumping,1,          ,            ,7000,700,          outward,0,0
	5kb,peer_genome,peer,  jumping,1,          ,            ,5000,500,          outward,0,0
	8kb,peer_genome,peer,  jumping,1,          ,            ,8000,800,          outward,0,0


Actual run

    /share/allpathslg-52155/src/allpaths_cache/PrepareAllPathsInputs.pl \
    DATA_DIR=/mouse/pero_genome/allpaths_data \
    GENOME_SIZE=2600000000 OVERWRITE=True PLOIDY=2 \
    HOSTS=40 TMP_DIR=/mnt/data0 \
    JAVA_MEM_GB=500


and

    RunAllPathsLG THREADS=40 FIX_ASSEMBLY_BASE_ERRORS=TRUE \
    PRE=/mouse/pero_genome/ \
    DATA_SUBDIR=allpaths_data \
    RUN=eremicus MAXPAR=2 \
    REFERENCE_NAME=peer \
    TARGETS=standard OVERWRITE=True \
    CONNECT_SCAFFOLDS=TRUE HAPLOIDIFY=TRUE

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
	-j <(gzip -cd Pero360-8K-10K_ATGTCA_AC6718ANXX_L006_001.R2.fastq.gz) -o Pero3608kb

Trimmomatic PE data

    java -Xmx300g -jar /share/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
    -threads 40 -baseout Pero360_550bp.gz \
    Pero360-WGS-550_GTGAAA_AC6718ANXX_L005_001.R1.fastq.gz \
    Pero360-WGS-550_GTGAAA_AC6718ANXX_L005_001.R2.fastq.gz \
    ILLUMINACLIP:/share/Trimmomatic-0.32/barcodes.fa:2:40:15 \
    LEADING:2 TRAILING:2 SLIDINGWINDOW:4:2 MINLEN:75
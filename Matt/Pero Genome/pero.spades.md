mouse spades
--

in `/mouse/pero_genome` started 1/16/15 at 1830

    spades.py -t 40 -m 500 --only-assembler -o spades.mouse --continue --careful \
    --pe1-1 /mnt/data3/macmanes/pero_genome/131008/peroL1_1P.fq \
    --pe1-2 /mnt/data3/macmanes/pero_genome/131008/peroL1_2P.fq  \
    --pe2-1 /mnt/data3/macmanes/pero_genome/131219/peroL5_1P.fq \
    --pe2-2 /mnt/data3/macmanes/pero_genome/131219/peroL5_2P.fq  \
    --pe3-1 /mnt/data3/macmanes/pero_genome/131023/peroL3_1P.fq \
    --pe3-2 /mnt/data3/macmanes/pero_genome/131023/peroL3_2P.fq  \
    --pe4-1 /mnt/data3/macmanes/pero_genome/131008/peroL2_1P.fq \
    --pe4-2 /mnt/data3/macmanes/pero_genome/131008/peroL2_2P.fq  \
    --pe5-1 /mnt/data3/macmanes/pero_genome/131219/peroL4_1P.fq \
    --pe5-2 /mnt/data3/macmanes/pero_genome/131219/peroL4_2P.fq  \
    --mp1-1 /mnt/data3/macmanes/pero-mate-pair/peer3kb.clipped.1.fq \
    --mp1-2 /mnt/data3/macmanes/pero-mate-pair/peer3kb.clipped.2.fq \
    --mp2-1 /mnt/data3/macmanes/pero-mate-pair/peer7kb.clipped.1.fq \
    --mp2-2 /mnt/data3/macmanes/pero-mate-pair/peer7kb.clipped.2.fq \
    --pacbio /mnt/data3/macmanes/pacbio/raw.pacbio.reads/fastq/all.pb.fastq
    

1 lib at a time, which will get me the error correction I think, then can use all the libs together:

    spades.py -t 40 -m 500 -o spadesL1 --careful -k 65 \
    --pe1-1 /mnt/data3/macmanes/pero_genome/131008/peroL1_1P.fq \
    --pe1-2 /mnt/data3/macmanes/pero_genome/131008/peroL1_2P.fq
    
This does not work...

malloc after 52 hours with kmer=21.. I'll try something higher. 



    spades.py -k 55,65,75 -t 40 -m 500 --only-assembler -o spades.mouse --careful \
    --pe1-1 /mnt/data3/macmanes/pero_genome/131008/peroL1_1P.fq \
    --pe1-2 /mnt/data3/macmanes/pero_genome/131008/peroL1_2P.fq  \
    --pe2-1 /mnt/data3/macmanes/pero_genome/131219/peroL5_1P.fq \
    --pe2-2 /mnt/data3/macmanes/pero_genome/131219/peroL5_2P.fq  \
    --pe3-1 /mnt/data3/macmanes/pero_genome/131023/peroL3_1P.fq \
    --pe3-2 /mnt/data3/macmanes/pero_genome/131023/peroL3_2P.fq  \
    --pe4-1 /mnt/data3/macmanes/pero_genome/131008/peroL2_1P.fq \
    --pe4-2 /mnt/data3/macmanes/pero_genome/131008/peroL2_2P.fq  \
    --pe5-1 /mnt/data3/macmanes/pero_genome/131219/peroL4_1P.fq \
    --pe5-2 /mnt/data3/macmanes/pero_genome/131219/peroL4_2P.fq  \
    --mp1-1 /mnt/data3/macmanes/pero-mate-pair/peer3kb.clipped.1.fq \
    --mp1-2 /mnt/data3/macmanes/pero-mate-pair/peer3kb.clipped.2.fq \
    --mp2-1 /mnt/data3/macmanes/pero-mate-pair/peer7kb.clipped.1.fq \
    --mp2-2 /mnt/data3/macmanes/pero-mate-pair/peer7kb.clipped.2.fq \
    --pacbio /mnt/data3/macmanes/pacbio/raw.pacbio.reads/fastq/all.pb.fastq

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



    spades.py -k 55,65,75 -t 40 -m 500 --only-assembler -o spades.mouse --careful --continue \
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

pero all NYGC data : started 4/3/15 at 2030

restarted 4/12/15 at 0800. Added `--cov-cutoff 2` and changed output dir to `$RAID`

    spades.py -k 95,85,105 -t 50 -m 1000 --only-assembler --cov-cutoff 2 -o $RAID/spades.mouse --careful \
    --pe1-1 /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_550bp.P20_1P.fq.gz \
    --pe1-2 /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_550bp.P20_2P.fq.gz  \
    --pe2-1 /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_300bp.P20_1P.fq.gz \
    --pe2-2 /mnt/data3/macmanes/pero_genome/raw_reasd/Pero360_300bp.P20_2P.fq.gz  \
    --mp1-1 /mnt/data3/macmanes/pero_genome/raw_reasd/peer5kb.clipped.1.fq \
    --mp1-2 /mnt/data3/macmanes/pero_genome/raw_reasd/peer5kb.clipped.2.fq \
    --mp2-1 /mnt/data3/macmanes/pero_genome/raw_reasd/peer8kb.clipped.1.fq \
    --mp2-2 /mnt/data3/macmanes/pero_genome/raw_reasd/peer8kb.clipped.2.fq \
    --mp3-1 /mnt/data3/macmanes/pero_genome/raw_reasd/peer7kb.clipped.1.fq \
    --mp3-2 /mnt/data3/macmanes/pero_genome/raw_reasd/peer7kb.clipped.2.fq \
    --mp4-1 /mnt/data3/macmanes/pero_genome/raw_reasd/peer3kb.clipped.1.fq \
    --mp4-2 /mnt/data3/macmanes/pero_genome/raw_reasd/peer3kb.clipped.2.fq \
    --pacbio /mnt/data3/macmanes/pacbio/raw.pacbio.reads/fastq/all.pb.fastq

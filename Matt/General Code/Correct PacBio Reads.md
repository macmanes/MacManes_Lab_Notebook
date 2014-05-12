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
	
Correct PacBio Reads

	nohup /share/wgs-8.1/Linux-amd64/bin/pacBioToCA -length 5000 -partitions 100 \
	-l pacbio -t 20 -s pacbio.spec \
	-genomeSize 2600000000 \
	-fastq /mnt/data3/macmanes/pacbio/raw.pacbio.reads/fastq/all.pb.fastq \
	illumina.frg > pbcr.out 2>&1 &
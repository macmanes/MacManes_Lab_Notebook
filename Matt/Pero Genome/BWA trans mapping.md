BWA Transcript mapping
-

STAR Transcript mapping
-

in `/mnt/data3/macmanes/STAR/transcripts`

	bwa index -p perotrans /mnt/data0/macmanes/maker/peer.est.fa \
	
	





>> Do Mapping

	bwa mem -t20 perotrans  ../../pero_annotation/Pero2926.1.fastq \
	../../pero_annotation/Pero2926.2.fastq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2926
	

	bwa mem -t20 perotrans  ../../pero_annotation/Pero2925.1.fastq \
	../../pero_annotation/Pero2925.2.fastq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2925
		


	bwa mem -t20 perotrans  $RAID/pero_pigeons_ladybugs/2342.trim_1P.fq  \
	$RAID/pero_pigeons_ladybugs/2342.trim_2P.fq  | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2342
	
	#done above here
	
	bwa mem -t20 perotrans  $RAID/pero_pigeons_ladybugs/2336.trim_1P.fq  \
	$RAID/pero_pigeons_ladybugs/2336.trim_2P.fq  | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2336

	bwa mem -t20 perotrans  $RAID/pero_pigeons_ladybugs/2346.trim_1P.fq  \
	$RAID/pero_pigeons_ladybugs/2346.trim_2P.fq  | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2346

	bwa mem -t20 perotrans  $RAID/pero_pigeons_ladybugs/2345.trim_1P.fq  \
	$RAID/pero_pigeons_ladybugs/2345.trim_2P.fq  | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2345

	bwa mem -t20 perotrans  $RAID/pero_pigeons_ladybugs/2336.trim_1U.fq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2336SE

	bwa mem -t20 perotrans  $RAID/pero_pigeons_ladybugs/2342.trim_1U.fq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2342SE

	bwa mem -t20 perotrans  $RAID/pero_pigeons_ladybugs/2345.trim_1U.fq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2345SE

	bwa mem -t20 perotrans  $RAID/pero_pigeons_ladybugs/2346.trim_1U.fq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2346SE



	cd ../bam
	samtools merge -fn -@10 2346.sort.bam 2346.bam 2346SE.bam
	samtools merge -fn -@10 2345.sort.bam 2345.bam 2345SE.bam
	samtools merge -fn -@10 2336.sort.bam 2336.bam 2336SE.bam
	samtools merge -fn -@10 2342.sort.bam 2342.bam 2342SE.bam
	
	##
	

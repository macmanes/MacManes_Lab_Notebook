STAR Transcript mapping
-

in `/mnt/data3/macmanes/STAR/transcripts`

	STAR --genomeDir peer_trans --runMode genomeGenerate --genomeFastaFiles /mnt/data0/macmanes/maker/peer.est.fa \
	--runThreadN 30 --limitGenomeGenerateRAM 100000000000
	





>> Do Mapping

	STAR --genomeDir peer_trans --readFilesIn ../../pero_annotation/Pero2926.1.fastq ../../pero_annotation/Pero2926.2.fastq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2926
	
		

	STAR --genomeDir peer_trans --readFilesIn ../../pero_annotation/Pero2925.1.fastq ../../pero_annotation/Pero2925.2.fastq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2925
	

	STAR --genomeDir peer_trans --readFilesIn $RAID/pero_pigeons_ladybugs/2342.trim_1P.fq $RAID/pero_pigeons_ladybugs/2342.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2342
	
	###SE
	
	STAR --genomeDir peer_trans --readFilesIn $RAID/pero_pigeons_ladybugs/2342.trim_1U.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2342SE1
	
	STAR --genomeDir peer_trans --readFilesIn $RAID/pero_pigeons_ladybugs/2345.trim_1P.fq $RAID/pero_pigeons_ladybugs/2345.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2345
	
	STAR --genomeDir peer_trans --readFilesIn $RAID/pero_pigeons_ladybugs/2346.trim_1U.fq $RAID/pero_pigeons_ladybugs/2346.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2346
	
	STAR --genomeDir peer_trans --readFilesIn $RAID/pero_pigeons_ladybugs/2342.trim_1P.fq $RAID/pero_pigeons_ladybugs/2342.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2342
	
	STAR --genomeDir peer_trans --readFilesIn $RAID/pero_pigeons_ladybugs/2336.trim_1P.fq $RAID/pero_pigeons_ladybugs/2336.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2336


	STAR --genomeDir peer_trans --readFilesIn $RAID/pero_pigeons_ladybugs/2345.trim_1U.fq \
	--runThreadN 10 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2345SE1
	
	STAR --genomeDir peer_trans --readFilesIn $RAID/pero_pigeons_ladybugs/2346.trim_1U.fq \
	--runThreadN 10 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2346SE1
	
	STAR --genomeDir peer_trans --readFilesIn $RAID/pero_pigeons_ladybugs/2336.trim_1U.fq \
	--runThreadN 10 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2336SE1

Make Bams

	cat 2342Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2342
	cat 2345Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2345
	cat 2346Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2346
	cat 2336Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2336
	cat 2345SE1Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2345SE1
	cat 2346SE1Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2346SE1
	cat 2336SE1Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2336SE1
	cat 2342SE1Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2342SE1

\##Need to do

	cat 2926Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ../bam/2926	cat 2925Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - ./bam/2925

	cd ../bam
	samtools merge -fn -@10 2346.sort.bam 2346.bam 2346SE1.bam
	samtools merge -fn -@10 2345.sort.bam 2345.bam 2345SE1.bam
	samtools merge -fn -@10 2336.sort.bam 2336.bam 2336SE1.bam
	samtools merge -fn -@10 2342.sort.bam 2342.bam 2342SE1.bam
	
	##
	

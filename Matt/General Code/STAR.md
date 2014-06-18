STAR Mapping
-

in `$RAID/STAR`

>> Make genome index


	STAR --genomeDir peer_genome --runMode genomeGenerate --genomeFastaFiles pero.genes.fa \
	--runThreadN 30 --limitGenomeGenerateRAM 100000000000
	
>> Do Mapping

	STAR --genomeDir peer_genome --readFilesIn ../pero_annotation/Pero2926.1.fastq ../pero_annotation/Pero2926.2.fastq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2926
	
		

	STAR --genomeDir peer_genome --readFilesIn ../pero_annotation/Pero2925.1.fastq ../pero_annotation/Pero2925.2.fastq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2925
	

	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2342.trim_1P.fq $RAID/pero_pigeons_ladybugs/2342.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2342
	
	###SE
	
	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2342.trim_1U.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2342SE1
	
	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2342.trim_2U.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2342SE2
	
	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2345.trim_1P.fq $RAID/pero_pigeons_ladybugs/2345.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2345
	
	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2346.trim_1P.fq $RAID/pero_pigeons_ladybugs/2346.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2346
	
	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2342.trim_1P.fq $RAID/pero_pigeons_ladybugs/2342.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2342
	
	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2336.trim_1P.fq $RAID/pero_pigeons_ladybugs/2336.trim_2P.fq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2336
	



	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2345.trim_1U.fq \
	--runThreadN 10 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2345SE1
	
	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2346.trim_1U.fq \
	--runThreadN 10 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2346SE1
	
	STAR --genomeDir peer_genome --readFilesIn $RAID/pero_pigeons_ladybugs/2336.trim_1U.fq \
	--runThreadN 10 --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix 2336SE1

 Make BAM's from SAM
 
	cat 2342Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - bam/2342
	cat 2926Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - bam/2926
	cat 2925Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - bam/2925
	
	cat 2345Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - bam/2345
	cat 2346Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - bam/2346
	cat 2336Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - bam/2336
	cat 2345SE1Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - bam/2345SE1
	cat 2346SE1Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - bam/2346SE1
	cat 2336SE1Aligned.out.sam | samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - bam/2336SE1



 Cufflinks
 
	for i in `ls *bam`; do F=`basename $i .bam`;
	cufflinks -p30 -o ../cufflinks/$F --library-type fr-firststrand \
	-G $SCRATCH/maker/pero.genes.all.gff \
	-b ../pero.genes.fa -u $F.bam; done

Cuffdiff

	cuffdiff -p10 -L wet,dry --library-type fr-firststrand \
	-b ../pero.genes.fa $SCRATCH/maker/pero.genes.all.gff \
	2925.bam,2925.bam,2342.merge.bam 2336.merge.bam,2345.merge.bam,2346.merge.bam
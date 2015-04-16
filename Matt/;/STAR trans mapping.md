STAR TRANSCRIPT Mapping
-

in `$RAID/STAR`

>> Make genome index


	STAR --genomeDir peer_star --runMode genomeGenerate --genomeFastaFiles /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa \
	--runThreadN 30 --limitGenomeGenerateRAM 100000000000
	
>> Do Mapping

	#2926

	time STAR --genomeDir peer_star --readFilesIn ../../pero_annotation/Pero2926.1.fastq ../../pero_annotation/Pero2926.2.fastq \
	--runThreadN 30 --genomeLoad LoadAndKeep --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2926
	

	#2925

	time STAR --genomeDir peer_star --readFilesIn ../../pero_annotation/Pero2925.1.fastq ../../pero_annotation/Pero2925.2.fastq \
	--runThreadN 30 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2925
	
	#2342

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2342.trim_1P.fq.gz $RAID/pero_pigeons_ladybugs/2342.trim_2P.fq.gz \
	--readFilesCommand zcat --runThreadN 30 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2342
	
	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2342.trim_1U.fq.gz --readFilesCommand zcat \
	--runThreadN 30 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2342SE1
	


	#2345

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2345.trim_1P.fq.gz $RAID/pero_pigeons_ladybugs/2345.trim_2P.fq.gz \
	--readFilesCommand zcat --runThreadN 30 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2345

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2345.trim_1U.fq.gz --readFilesCommand zcat \
	--runThreadN 10 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2345SE1

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2345a.trim_1U.fq.gz --readFilesCommand zcat \
	--runThreadN 10 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2345SE2

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2345a.trim_1P.fq.gz $RAID/pero_pigeons_ladybugs/2345a.trim_2P.fq.gz \
	--readFilesCommand zcat --runThreadN 30 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2345a


	#2346
	
	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2346.trim_1P.fq.gz $RAID/pero_pigeons_ladybugs/2346.trim_2P.fq.gz \
	--readFilesCommand zcat --runThreadN 30 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2346
	

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2346.trim_1U.fq.gz --readFilesCommand zcat \
	--runThreadN 10 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2346SE1
	
	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2346a.trim_1U.fq.gz --readFilesCommand zcat \
	--runThreadN 10 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2346SE2

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2346a.trim_1P.fq.gz $RAID/pero_pigeons_ladybugs/2346a.trim_2P.fq.gz \
	--readFilesCommand zcat --runThreadN 30 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2346a

	#2336

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2336.trim_1P.fq.gz $RAID/pero_pigeons_ladybugs/2336.trim_2P.fq.gz \
	--readFilesCommand zcat --runThreadN 30 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2336
	
	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2336.trim_1U.fq.gz --readFilesCommand zcat \
	--runThreadN 10 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2336SE1

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2336a.trim_1U.fq.gz --readFilesCommand zcat \
	--runThreadN 10 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2336SE2

	time STAR --genomeDir peer_star --readFilesIn $RAID/pero_pigeons_ladybugs/2336a.trim_1P.fq.gz $RAID/pero_pigeons_ladybugs/2336a.trim_2P.fq.gz \
	--readFilesCommand zcat --runThreadN 30 --genomeLoad LoadAndKeep  --outStd SAM | samtools view -@ 6 -Sub - | samtools sort -n -m4G -@ 16 - ../starbam/2336a

	#done




	

	
 Make BAM's from SAM
 
	cat 2342Aligned.out.sam | samtools view -@ 6 -Sub - | samtools sort -m3G -@8 - bam/2342
	cat 2926Aligned.out.sam | samtools view -@ 6 -Sub - | samtools sort -m3G -@8 - bam/2926	cat 2925Aligned.out.sam | samtools view -@ 6 -Sub - | samtools sort -m3G -@8 - bam/2925
	
	cat 2345Aligned.out.sam | samtools view -@ 6 -Sub - | samtools sort -m3G -@8 - bam/2345
	cat 2346Aligned.out.sam | samtools view -@ 6 -Sub - | samtools sort -m3G -@8 - bam/2346
	cat 2342Aligned.out.sam | samtools view -@ 6 -Sub - | samtools sort -m3G -@8 - bam/2342
	cat 2336Aligned.out.sam | samtools view -@ 6 -Sub - | samtools sort -m3G -@8 - bam/2336
 Cufflinks
 
	for i in `ls *bam`; do F=`basename $i .bam`;
	cufflinks -p30 -o ../cufflinks/$F --library-type fr-firststrand \
	-G $SCRATCH/maker/pero.genes.all.gff \
	-b ../pero.genes.fa -u $F.bam; done

Cuffdiff

	cuffdiff -p10 -L wet,dry --library-type fr-firststrand \
	-b ../pero.genes.fa $SCRATCH/maker/pero.genes.all.gff \
	2925.bam,2925.bam,2342.merge.bam 2336.merge.bam,2345.merge.bam,2346.merge.bam
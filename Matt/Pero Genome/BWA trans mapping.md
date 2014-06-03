BWA Transcript mapping
-

STAR Transcript mapping
-

in `/mnt/data3/macmanes/STAR/transcripts`

	bwa index -p pero_final /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa \
	
	





>> Do Mapping

	bwa mem -t20 pero_final  ../../pero_annotation/Pero2926.1.fastq \
	../../pero_annotation/Pero2926.2.fastq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@8 - 2926
	

	bwa mem -t20 pero_final  ../../pero_annotation/Pero2925.1.fastq \
	../../pero_annotation/Pero2925.2.fastq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - ../bam/2925
		

	bwa mem -t20 pero_final  $RAID/pero_pigeons_ladybugs/2342.trim_1P.fq  \
	$RAID/pero_pigeons_ladybugs/2342.trim_2P.fq  | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - ../bam/2342
	
	
	bwa mem -t20 pero_final  $RAID/pero_pigeons_ladybugs/2336.trim_1P.fq  \
	$RAID/pero_pigeons_ladybugs/2336.trim_2P.fq  | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - ../bam/2336

	bwa mem -t20 pero_final  $RAID/pero_pigeons_ladybugs/2346.trim_1P.fq  \
	$RAID/pero_pigeons_ladybugs/2346.trim_2P.fq  | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - ../bam/2346

	bwa mem -t20 pero_final  $RAID/pero_pigeons_ladybugs/2345.trim_1P.fq  \
	$RAID/pero_pigeons_ladybugs/2345.trim_2P.fq  | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - ../bam/2345

	bwa mem -t20 pero_final  $RAID/pero_pigeons_ladybugs/2336.trim_1U.fq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - ../bam/2336SE

	bwa mem -t20 pero_final  $RAID/pero_pigeons_ladybugs/2342.trim_1U.fq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - ../bam/2342SE

	bwa mem -t20 pero_final  $RAID/pero_pigeons_ladybugs/2345.trim_1U.fq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - ../bam/2345SE

	bwa mem -t20 pero_final  $RAID/pero_pigeons_ladybugs/2346.trim_1U.fq | \
	samtools view -@6 -Sub - | samtools sort -n -m3G -@16 - ../bam/2346SE



	cd ../bam
	samtools merge -fn -@10 2346.sort.bam 2346.bam 2346SE.bam
	samtools merge -fn -@10 2345.sort.bam 2345.bam 2345SE.bam
	samtools merge -fn -@10 2336.sort.bam 2336.bam 2336SE.bam
	samtools merge -fn -@10 2342.sort.bam 2342.bam 2342SE.bam
	
	##
	

\#eXpress

	for i in `ls *bam`; do F=`basename $i .bam`; express -p 20 --rf-stranded /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa $i -o $F.express ; done
	
	express -p 20 --rf-stranded /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa 2345.sort.bam -o 2345.express --aux-param-file 2342.sort.express/params.xprs
	express -p 20 --rf-stranded /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa 2336.sort.bam -o 2336.express --aux-param-file 2342.sort.express/params.xprs
	express -p 20 --rf-stranded /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa 2346.sort.bam -o 2346.express --aux-param-file 2342.sort.express/params.xprs




\#process eXpress

    cat 2925.express/results.xprs | sort -k2 | cut -f2 > 0.txt
	cat 2925.express/results.xprs | sort -k2 | cut -f8 > 0a.txt
	cat 2926.express/results.xprs | sort -k2 | cut -f8 > 1.txt
    cat 2342.sort.express/results.xprs | sort -k2 | cut -f8 > 2.txt
    cat 2345.sort.express/results.xprs | sort -k2 | cut -f8 > 3.txt
    cat 2346.sort.express/results.xprs | sort -k2 | cut -f8 > 4.txt
    cat 2336.sort.express/results.xprs | sort -k2 | cut -f8 > 5.txt
    paste 0.txt 0a.txt 1.txt 2.txt 3.txt 4.txt 5.txt > pero.effcounts.counts
   

	cat pero.effcounts.counts | awk '{print $1 "\t" int($2+0.5) "\t" int($3+0.5) "\t" int($4+0.5) "\t" int($5+0.5) "\t" int($6+0.5) "\t" int($7+0.5)} ' > pero.effcounts.txt 


 
    sed -i '1 i\names \t wet1 \t wet2 \t dry1 \t dry2 \t dry3 \t dry4' pero.effcounts.txt  


\#process eXpress for R regression

    cat 2925.express/results.xprs | sort -k2 | cut -f2 > 0.txt
	cat 2925.express/results.xprs | sort -k2 | cut -f15 > 0a.txt
	cat 2926.express/results.xprs | sort -k2 | cut -f15 > 1.txt
    cat 2342.sort.express/results.xprs | sort -k2 | cut -f15 > 2.txt
    cat 2345.sort.express/results.xprs | sort -k2 | cut -f15 > 3.txt
    cat 2346.sort.express/results.xprs | sort -k2 | cut -f15 > 4.txt
    cat 2336.sort.express/results.xprs | sort -k2 | cut -f15 > 5.txt
    paste 0.txt 0a.txt 1.txt 2.txt 3.txt 4.txt 5.txt > pero.tpm.counts
   

	cat pero.tpm.counts | awk '{print $1 "\t" int($2+0.5) "\t" int($3+0.5) "\t" int($4+0.5) "\t" int($5+0.5) "\t" int($6+0.5) "\t" int($7+0.5)} ' > 	pero.tpm.txt

 
    sed -i '1 i\names \t wet1 \t wet2 \t dry1 \t dry2 \t dry3 \t dry4' pero.tpm.counts  


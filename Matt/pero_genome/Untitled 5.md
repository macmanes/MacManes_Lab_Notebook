Titus review

	Trinity --seqType fq \	--JM 100G --trimmomatic \	--bflyHeapSpaceMax 10G \	--inchworm_cpu 10 \	--left SRR1197972_1.fastq.gz SRR1197965_1.fastq.gz SRR1197522_1.fastq.gz \	--right SRR1197972_2.fastq.gz SRR1197965_2.fastq.gz SRR1197522_2.fastq.gz \	--CPU 20 \	--output titus_SS_no_norm \	--group_pairs_distance 999 \	--quality_trimming_params "ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic-0.32/adapters/TruSeq3-PE.fa:2:40:15 \	LEADING:2 TRAILING:2 MINLEN:25"
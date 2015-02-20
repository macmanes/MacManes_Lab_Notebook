Mc_Transcriptome
--

    lighter -t 60 \
    -r Thomas_McOr3_R2.PF.fastq \
    -r Thomas_McOr3_R1.PF.fastq \
    -r Thomas_McOr2_R2.PF.fastq \
    -r Thomas_McOr2_R1.PF.fastq \
    -r Thomas_McOr1_R2.PF.fastq \
    -r Thomas_McOr1_R1.PF.fastq \
    -r Thomas_McBr3_R1.PF.fastq \
    -r Thomas_McBr3_R2.PF.fastq \
    -r Thomas_McBr1_R1.PF.fastq \
    -r Thomas_McBr1_R2.PF.fastq \
    -r Thomas_McBr2_R1.PF.fastq \
    -r Thomas_McBr2_R2.PF.fastq \
    -k 32 600000000 .05
    
trinity

	Trinity --seqType fq --max_memory 200G --inchworm_cpu 10 --trimmomatic \
	--left Thomas_McBr3_R1.PF.cor.fq,\
	Thomas_McOr1_R1.PF.cor.fq,\
	Thomas_McOr2_R1.PF.cor.fq,\
	Thomas_McOr3_R1.PF.cor.fq,\
	Thomas_McBr2_R1.PF.cor.fq,\
	Thomas_McBr1_R1.PF.cor.fq \
	--right Thomas_McBr3_R2.PF.cor.fq,\
	Thomas_McOr1_R2.PF.cor.fq,\
	Thomas_McOr2_R2.PF.cor.fq,\
	Thomas_McOr3_R2.PF.cor.fq,\
	Thomas_McBr2_R2.PF.cor.fq,\
	Thomas_McBr1_R2.PF.cor.fq \
	--CPU 60 --output mc_lighter_trinity --group_pairs_distance 999
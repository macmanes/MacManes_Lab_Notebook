mapping

	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/HYB_wt_rep1_1_pe \
	../trimmed_x/HYB_wt_rep1_2_pe  | \
	express --no-bias-correct -o express_trin/HYB_wt_rep1.xprs \
	-p4 trin_all_index/trin.fasta
	

	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/HYB_wt_rep2_1_pe \
	../trimmed_x/HYB_wt_rep2_2_pe  | \
	express --no-bias-correct -o express_trin/HYB_wt_rep2.xprs \
	-p4 trin_all_index/trin.fasta	

	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/HYB_sdE3_rep1_1_pe \
	../trimmed_x/HYB_sdE3_rep1_2_pe  | \
	express --no-bias-correct -o express_trin/HYB_sdE3_rep1.xprs \
	-p4 trin_all_index/trin.fasta

	
	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/HYB_sdE3_rep2_1_pe \
	../trimmed_x/HYB_sdE3_rep2_2_pe  | \
	express --no-bias-correct -o express_trin/HYB_sdE3_rep2.xprs \
	-p4 trin_all_index/trin.fasta
	

	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/SAM_sdE3_rep1_1_pe \
	../trimmed_x/SAM_sdE3_rep1_2_pe  | \
	express --no-bias-correct -o express_trin/SAM_sdE3_rep1.xprs \
	-p4 trin_all_index/trin.fasta
	
	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/SAM_sdE3_rep2_1_pe \
	../trimmed_x/SAM_sdE3_rep2_2_pe  | \
	express --no-bias-correct -o express_trin/SAM_sdE3_rep2.xprs \
	-p4 trin_all_index/trin.fasta
	
	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/SAM_wt_rep1_1_pe \
	../trimmed_x/SAM_wt_rep1_2_pe  | \
	express --no-bias-correct -o express_trin/SAM_wt_rep1.xprs \
	-p4 trin_all_index/trin.fasta
	
	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/SAM_wt_rep2_1_pe \
	../trimmed_x/SAM_wt_rep2_2_pe  | \
	express --no-bias-correct -o express_trin/SAM_wt_rep2.xprs \
	-p4 trin_all_index/trin.fasta
	

	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/ORE_sdE3_rep1_1_pe \
	../trimmed_x/ORE_sdE3_rep1_2_pe  | \
	express --no-bias-correct -o express_trin/ORE_sdE3_rep1.xprs \
	-p4 trin_all_index/trin.fasta

	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/ORE_sdE3_rep2_1_pe \
	../trimmed_x/ORE_sdE3_rep2_2_pe  | \
	express --no-bias-correct -o express_trin/ORE_sdE3_rep2.xprs \
	-p4 trin_all_index/trin.fasta

	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/ORE_wt_rep2_1_pe \
	../trimmed_x/ORE_wt_rep2_2_pe  | \
	express --no-bias-correct -o express_trin/ORE_wt_rep2.xprs \
	-p4 trin_all_index/trin.fasta

	bwa mem -t 4 trin_all_index/all \
	../trimmed_x/ORE_wt_rep1_1_pe \
	../trimmed_x/ORE_wt_rep1_2_pe  | \
	express --no-bias-correct -o express_trin/ORE_wt_rep1.xprs \
	-p4 trin_all_index/trin.fasta

    bwa mem -t 4 trin_all_index/all \
    ../trimmed_x/ORE_sdE3_rep2_1_pe \
    ../trimmed_x/ORE_sdE3_rep2_2_pe  | \
    express --no-bias-correct -o express_trin/ORE_sdE3_rep2.xprs \
    -p4 trin_all_index/trin.fasta
    
    bwa mem -t 4 trin_all_index/all \
    ../trimmed_x/ORE_sdE3_rep1_1_pe \
    ../trimmed_x/ORE_sdE3_rep1_2_pe  | \
    express --no-bias-correct -o express_trin/ORE_sdE3_rep1.xprs \
    -p4 trin_all_index/trin.fasta
    



SOAP


	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/HYB_wt_rep1_1_pe \
	../trimmed_x/HYB_wt_rep1_2_pe  | \
	express --no-bias-correct -o express_soap/HYB_wt_rep1.xprs \
	-p4 soap_all_index/soap.fasta
	

	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/HYB_wt_rep2_1_pe \
	../trimmed_x/HYB_wt_rep2_2_pe  | \
	express --no-bias-correct -o express_soap/HYB_wt_rep2.xprs \
	-p4 soap_all_index/soap.fasta	

	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/HYB_sdE3_rep1_1_pe \
	../trimmed_x/HYB_sdE3_rep1_2_pe  | \
	express --no-bias-correct -o express_soap/HYB_sdE3_rep1.xprs \
	-p4 soap_all_index/soap.fasta

	
	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/HYB_sdE3_rep2_1_pe \
	../trimmed_x/HYB_sdE3_rep2_2_pe  | \
	express --no-bias-correct -o express_soap/HYB_sdE3_rep2.xprs \
	-p4 soap_all_index/soap.fasta
	

	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/SAM_sdE3_rep1_1_pe \
	../trimmed_x/SAM_sdE3_rep1_2_pe  | \
	express --no-bias-correct -o express_soap/SAM_sdE3_rep1.xprs \
	-p4 soap_all_index/soap.fasta
	
	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/SAM_sdE3_rep2_1_pe \
	../trimmed_x/SAM_sdE3_rep2_2_pe  | \
	express --no-bias-correct -o express_soap/SAM_sdE3_rep2.xprs \
	-p4 soap_all_index/soap.fasta
	
	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/SAM_wt_rep1_1_pe \
	../trimmed_x/SAM_wt_rep1_2_pe  | \
	express --no-bias-correct -o express_soap/SAM_wt_rep1.xprs \
	-p4 soap_all_index/soap.fasta
	
	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/SAM_wt_rep2_1_pe \
	../trimmed_x/SAM_wt_rep2_2_pe  | \
	express --no-bias-correct -o express_soap/SAM_wt_rep2.xprs \
	-p4 soap_all_index/soap.fasta
	

	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/ORE_sdE3_rep1_1_pe \
	../trimmed_x/ORE_sdE3_rep1_2_pe  | \
	express --no-bias-correct -o express_soap/ORE_sdE3_rep1.xprs \
	-p4 soap_all_index/soap.fasta

	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/ORE_sdE3_rep2_1_pe \
	../trimmed_x/ORE_sdE3_rep2_2_pe  | \
	express --no-bias-correct -o express_soap/ORE_sdE3_rep2.xprs \
	-p4 soap_all_index/soap.fasta

	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/ORE_wt_rep2_1_pe \
	../trimmed_x/ORE_wt_rep2_2_pe  | \
	express --no-bias-correct -o express_soap/ORE_wt_rep2.xprs \
	-p4 soap_all_index/soap.fasta

	bwa mem -t 4 soap_all_index/all \
	../trimmed_x/ORE_wt_rep1_1_pe \
	../trimmed_x/ORE_wt_rep1_2_pe  | \
	express --no-bias-correct -o express_soap/ORE_wt_rep1.xprs \
	-p4 soap_all_index/soap.fasta


    bwa mem -t 4 soap_all_index/all \
    ../trimmed_x/ORE_sdE3_rep2_1_pe \
    ../trimmed_x/ORE_sdE3_rep2_2_pe  | \
    express --no-bias-correct -o express_soap/ORE_sdE3_rep2.xprs \
    -p4 soap_all_index/soap.fasta
    
    bwa mem -t 4 soap_all_index/all \
    ../trimmed_x/ORE_sdE3_rep1_1_pe \
    ../trimmed_x/ORE_sdE3_rep1_2_pe  | \
    express --no-bias-correct -o express_soap/ORE_sdE3_rep1.xprs \
    -p4 soap_all_index/soap.fasta









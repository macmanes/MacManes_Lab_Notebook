mouse rnaseq
--

in `/mouse/mouse_rnaseq`

`mapping.mk` is the makefile that containes the STAR mapping info, in short:

    $(GENOME_DIR)/peer_genome/chrLength.txt:$(REF)
            @echo ---Quantitiating Transcripts---
            mkdir -p $(GENOME_DIR)/peer_genome
            STAR --genomeDir $(GENOME_DIR)/peer_genome --runMode genomeGenerate --genomeFastaFiles $(REF) \
            --runThreadN $(CPU) --limitGenomeGenerateRAM 100000000000
    
    2926Aligned.sortedByCoord.out.bam: name := 2926
    2926Aligned.sortedByCoord.out.bam:$(GENOME_DIR)/peer_genome/chrLength.txt
            @echo TIMESTAMP: '\n\n' `date +'%a %d%b%Y  %H:%M:%S'` ---Begin mapping of sample number $(name)--- '\n\n'
            STAR --outFilterMatchNminOverLread 0.40 --outStd Log --genomeDir $(GENOME_DIR)/peer_genome --outFilterMismatchNmax 2 \
            --readFilesIn $(DATA_DIR)/Pero2926.1.fastq $(DATA_DIR)/Pero2926.2.fastq --outFilterScoreMinOverLread 0.40 \
            --runThreadN $(CPU) --genomeLoad LoadAndKeep --outFilterIntronMotifs RemoveNoncanonical \
            --outSAMtype BAM SortedByCoordinate --outFileNamePrefix $(name) --limitBAMsortRAM 100000000000
            
now I want to run cufflinks on the bam files

    for i in `ls *bam`; do F=`basename $i .out.bam`;
    cufflinks -p24 -o cufflinks/$F --library-type fr-firststrand \
    -G gff/pero.genes.all.gff \
    -b genome/pero.genes.fa -u $i; done
    
	cuffdiff -p24 -L wet,dry --library-type fr-firststrand \
	-b ../genome/pero.genes.fa ../gff/pero.genes.all.gff \
	2346Aligned.sortedByCoord.out.bam,
	2345Aligned.sortedByCoord.out.bam,
	2336Aligned.sortedByCoord.out.bam \
	2925Aligned.sortedByCoord.out.bam,
	234Aligned.sortedByCoord.out.bam,
	2355Aligned.sortedByCoord.out.bam,
	2335Aligned.sortedByCoord.out.bam,
	336Aligned.sortedByCoord.out.bam,
	335Aligned.sortedByCoord.out.bam,
	2342Aligned.sortedByCoord.out.bam,

    
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

cuffmerge

    cuffmerge -p 24 -s ../genome/pero.genes.fa \
    -g ../gff/pero.genes.all.gff -o pero list.txt
    
cuffquant

    for i in `ls *bam`; do F=`basename $i .out.bam`;
    cuffquant -p 24 -o cuffquant/$F --library-type fr-firststrand \
    -b genome/pero.genes.fa -u cuffmerge/merged.gtf $i; done

cuffdiff

    cuffdiff -p24 -L dry,wet --library-type fr-firststrand \
    -b ../genome/pero.genes.fa ../cuffmerge/merged.gtf \
    ../cuffquant/2346Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2345Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2336Aligned.sortedByCoord/abundances.cxb \
    ../cuffquant/2925Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/234Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2355Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2335Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/336Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/335Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/334Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2926Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2342Aligned.sortedByCoord/abundances.cxb
    

    cuffdiff -p24 -L dry,wet --library-type fr-firststrand \
    -b ../genome/pero.genes.fa ../cuffmerge/merged.gtf \
    ../cuffquant/2346Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2345Aligned.sortedByCoord/abundances.cxb \
    ../cuffquant/2925Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/234Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2355Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2335Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/336Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/335Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/334Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2926Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2342Aligned.sortedByCoord/abundances.cxb
    



Annotating:


	
in `/mouse/mouse_rnaseq/cuffdiff/old`

set working directory for the maker derived transcripts.. Until a new assembly is had, this is the right working dir.

	WDIR=/mnt/data3/macmanes/maker/pero.genes.maker.output/
	
find Maker entries for the genes that diff expressed.

	grep yes gene_exp.diff | awk '{print $4}' | awk -F ':' '{print $1}' > ge.list

get the specific locations of the transcript sequenes.
	
	grep -wf ge.list $WDIR/pero.genes_master_datastore_index.log | grep FINISHED | awk '{print $2}' > loc.list

get the actual sequences. 
	
	for i in $(cat loc.list); do cat $WDIR/$i/*transcripts.fasta >> gene.exp.diff.candidates.fasta; done


get the actual sequences **FROM GENOME**. 
	
	for i in $(cat ge.list); do grep -A1 --max-count=1 -w $i >> gene.exp.diff.candidates.genome.fasta; done


will need to blast. 

in `/mouse/mouse_rnaseq/cuffdiff/blast`

downloaded refseq mammal blast

	gzip -cd *gz | makeblastdb -in - -title mammal -out mammal -dbtype nucl

	blastn -db mammal -query ../old/gene.exp.diff.candidates.genome.fasta \
	-outfmt '6 qseqid length evalue qstart qend stitle' -evalue 1e-8 \
	-num_threads 50 -max_target_seqs 1 -out gene_exp_diff.genome.blastn


cummerbund - on mac

	library(cummeRbund)
	cuff<-readCufflinks()
	
cuffnorm

    cuffnorm -p24 -L dry,wet --library-type fr-firststrand ../cuffmerge/merged.gtf \
    ../cuffquant/2346Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2345Aligned.sortedByCoord/abundances.cxb \
    ../cuffquant/2925Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/234Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2355Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2335Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/336Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/335Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/334Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2926Aligned.sortedByCoord/abundances.cxb,\
    ../cuffquant/2342Aligned.sortedByCoord/abundances.cxb



    cs <- as.matrix(read.delim("~/Dropbox/DEB_Summers_Nielsen_MacManes/candidates.xprs")) 
    for(n in 15:nrow(cs)) {  
        x <- try(summary(lm(as.numeric(cs[n,c(2:10)]) ~ as.numeric(cs[10,c(2:10)])))$coefficients[2,4], silent = TRUE)  
        try(if(x<0.0000033) {  
            cat(n,"\t",cs[n,1],"\t", "raw p= ", x, "\n", sep = "", file = "")  
        }, silent = TRUE)  
    }


pull out results

	grep P9362 cds.attr_table
	P9362	-	-	XLOC_014354	maker-Contig18648-exonerate_protein2genome-gene-0.11	TSS14564	Contig18648:10693-11370	-    




























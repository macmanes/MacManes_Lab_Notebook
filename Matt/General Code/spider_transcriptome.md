spider transcriptome
--

in `/mnt/data3/macmanes/121114_HS3B_elias_spider/raw.reads`

I concatenated all the read files together from 7L, 67L, 51L, 28W, 10L

**error correction:**


	lighter -r spider.1.fq -r spider.2.fq -k 17 50000000 0.1 -t 40

**diginorm:**

	interleave-reads.py spider.1.cor.fq spider.2.cor.fq -o interleaved.fq
	normalize-by-median.py -p -x 15e9 -k 25 -C 50 --out ec.khmer_normalized.fq interleaved.fq
	split-paired-reads.py ec.khmer_normalized.fq
	

Diginorm removed 78% of reads...
	
**Assembly**

	Trinity --seqType fq --JM 150G --trimmomatic \
    --left ec.khmer_normalized.fq.1  \
    --right ec.khmer_normalized.fq.2 \
    --CPU 60 --output ec.C50.P2 --group_pairs_distance 999 --inchworm_cpu 10 \
    --quality_trimming_params "ILLUMINACLIP:/mnt/data3/macmanes/subsamp/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25"
    
**TransDecoder**

	TransDecoder -t ec.C50.P2/Trinity.fasta --CPU 60	

**Mapping**

	bwa mem -t60 index  spider.1.cor.fq spider.2.cor.fq | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - spider.rnaseq
	samtools flagstat spider.rnaseq.bam
	

**express**

	express -p 60 ec.C50.P2/Trinity.fasta spider.rnaseq.bam

**format fasta file for subsampling**

	sed ':begin;$!N;/[ACTGNn-]\n[ACTGNn-]/s/\n//;tbegin;P;D' \
	ec.C50.P2/Trinity.fasta > $HOME/spider/ec.C50.P2.Trin.fasta
	

**subsampling**

	#save everything that looks like coding sequence
	awk '{print $1}' Trinity.fasta.transdecoder.bed > /home/macmanes/spider/list
	awk '1>$15{next}1' results.xprs  | awk '{print $2}' | \
	sed '1,1d' >> /home/macmanes/spider/list
	sort list | uniq > list2
<<<<<<< HEAD
<<<<<<< HEAD
	split -l 4000 list2

=======
	split -n20 list2
>>>>>>> FETCH_HEAD
=======
	split -n20 list2
>>>>>>> FETCH_HEAD

**extract**


    for i in `cat xaa`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa1; done &
    for i in `cat xab`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa2; done &
    for i in `cat xac`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa3; done &
    for i in `cat xad`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa4; done &
    for i in `cat xae`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa5; done &
    for i in `cat xaf`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa6; done &
    for i in `cat xag`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa7; done &
    for i in `cat xah`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa8; done &
    for i in `cat xai`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa9; done &
    for i in `cat xaj`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa11; done &
    for i in `cat xak`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa10; done &
    for i in `cat xal`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa12; done &
    for i in `cat xam`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa13; done &
    for i in `cat xan`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa14; done &
    for i in `cat xao`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa15; done &
    for i in `cat xap`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa16; done &
    for i in `cat xaq`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa17; done &
    for i in `cat xar`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa18; done &
    for i in `cat xas`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa19; done &
    for i in `cat xat`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa20; done &
    for i in `cat xau`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa21; done &
    for i in `cat xav`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa22; done &
    for i in `cat xaw`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa23; done &
    for i in `cat xax`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa24; done &
    
	cat ec.C50.P2.Trin.highexp.spider.fa* > ec.C50.P2.Trin.highexp.spider.fasta

**mapping for diff expression**

	cp /mnt/data3/macmanes/121114_HS3B_elias_spider/raw.reads/MDM* . &
	cp $RAID/131017_HS1B_spider/*gz . &
	bwa index -p index ec.C50.P2.Trin.highexp.spider.fasta

	bwa mem -t60 index  MDM_SPIDER_10L_1.fq.gz MDM_SPIDER_10L_2.fq.gz | express -p 20 -o 10L_paired.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm MDM_SPIDER_10L_1.fq.gz MDM_SPIDER_10L_2.fq.gz

	bwa mem -t60 index  MDM_SPIDER_7L_1.fq.gz MDM_SPIDER_7L_2.fq.gz | express -p 20 -o 7L_paired.xprs ec.C50.P2.Trin.highexp.spider.fasta

	rm MDM_SPIDER_7L_1.fq.gz MDM_SPIDER_7L_2.fq.gz
	bwa mem -t60 index  MDM_SPIDER_67L_1.fq.gz MDM_SPIDER_67L_2.fq.gz | express -p 20 -o 67L_paired.xprs ec.C50.P2.Trin.highexp.spider.fasta

	rm MDM_SPIDER_67L_1.fq.gz MDM_SPIDER_67L_2.fq.gz
	bwa mem -t60 index  MDM_SPIDER_28W_1.fq.gz MDM_SPIDER_28W_2.fq.gz | express -p 20 -o 28W_paired.xprs ec.C50.P2.Trin.highexp.spider.fasta

	rm MDM_SPIDER_28W_1.fq.gz MDM_SPIDER_28W_2.fq.gz

	bwa mem -t60 index  MDM_SPIDER_51L_1.fq.gz MDM_SPIDER_51L_2.fq.gz | express -p 20 -o 51L_paired.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm MDM_SPIDER_51L_1.fq.gz MDM_SPIDER_51L_2.fq.gz
	
	bwa mem -t60 index  spider110L.fq.gz | express -p 20 -o 110L_single.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm spider110L.fq.gz
	
	bwa mem -t60 index  spider39.fq.gz | express -p 20 -o 39_single.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm spider39.fq.gz

	bwa mem -t60 index  spider48.fq.gz | express -p 20 -o 48_single.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm spider48.fq.gz

	bwa mem -t60 index  spider55.fq.gz | express -p 20 -o 55_single.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm spider55.fq.gz

	bwa mem -t60 index  spider73.fq.gz | express -p 20 -o 73_single.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm spider73.fq.gz

	bwa mem -t60 index  spider83.fq.gz | express -p 20 -o 83_single.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm spider83.fq.gz

	bwa mem -t60 index  spider89.fq.gz | express -p 20 -o 89_single.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm spider89.fq.gz

	bwa mem -t60 index  spider96L.fq.gz | express -p 20 -o 96L_single.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm spider96L.fq.gz

	bwa mem -t60 index  spider9W.fq.gz | express -p 20 -o 9W_single.xprs ec.C50.P2.Trin.highexp.spider.fasta
	rm spider9W.fq.gz
	
<<<<<<< HEAD
<<<<<<< HEAD

**exporting counts**

    cat 10L_paired.xprs/results.xprs | sort -k2 | cut -f2 > 0.txt
    cat 10L_paired.xprs/results.xprs | sort -k2 | cut -f11 > 0a.txt
    cat 96_single.xprs/results.xprs | sort -k2 | cut -f11 > 12.txt
    cat 7L_paired.xprs/results.xprs | sort -k2 | cut -f11 > 1.txt
    cat 67L_paired.xprs/results.xprs | sort -k2 | cut -f11 > 2.txt
    cat 51L_paired.xprs/results.xprs | sort -k2 | cut -f11 > 3.txt
    cat 110L_single.xprs/results.xprs | sort -k2 | cut -f11 > 4.txt
    cat 96_single.xprs/results.xprs | sort -k2 | cut -f11 > 13.txt
    cat 28W_paired.xprs/results.xprs | sort -k2 | cut -f11 > 5.txt
    cat 39_single.xprs/results.xprs | sort -k2 | cut -f11 > 6.txt
    cat 48_single.xprs/results.xprs | sort -k2 | cut -f11 > 7.txt
    cat 55_single.xprs/results.xprs | sort -k2 | cut -f11 > 8.txt
    cat 73_single.xprs/results.xprs | sort -k2 | cut -f11 > 9.txt
    cat 83_single.xprs/results.xprs | sort -k2 | cut -f11 > 10.txt
    cat 89_single.xprs/results.xprs | sort -k2 | cut -f11 > 11.txt
    paste 0.txt 0a.txt 12.txt 1.txt 2.txt 3.txt 4.txt 13.txt 5.txt 6.txt 7.txt 8.txt 9.txt 10.txt 11.txt   > spider.txt 
    
    cat spider.txt | sed '1 i\names 10L 96L 7L 67L 51L 110L 96W 28W 39WL 48WL 55WL 73WL 83WL 89WL' > spider.effcounts.txt 
    
=======
=======
>>>>>>> FETCH_HEAD
**pulling out count data**

    cat 28W_paired.xprs/results.xprs | sort -k2 | cut -f2 > 0.txt
    cat 28W_paired.xprs/results.xprs | sort -k2 | cut -f8 > 0a.txt
    cat 9W.xprs/results.xprs | sort -k2 | cut -f8 > 1.txt
    cat 10L_paired.xprs/results.xprs | sort -k2 | cut -f8 > 2.txt
    cat 7L_paired.xprs/results.xprs | sort -k2 | cut -f8 > 3.txt
    cat 67L_paired.xprs/results.xprs | sort -k2 | cut -f8 > 4.txt
    cat 51L_paired.xprs/results.xprs | sort -k2 | cut -f8 > 5.txt
    cat 110L_single.xprs/results.xprs | sort -k2 | cut -f8 > 6.txt
    cat 96L_single.xprs/results.xprs | sort -k2 | cut -f8 > 7.txt
    cat 39_single.xprs/results.xprs | sort -k2 | cut -f8 > 8.txt
    cat 48_single.xprs/results.xprs | sort -k2 | cut -f8 > 9.txt
    cat 55_single.xprs/results.xprs | sort -k2 | cut -f8 > 10.txt
    cat 73_single.xprs/results.xprs | sort -k2 | cut -f8 > 11.txt
    cat 83_single.xprs/results.xprs | sort -k2 | cut -f8 > 12.txt
    cat 89_single.xprs/results.xprs | sort -k2 | cut -f8 > 13.txt
    paste 0.txt 0a.txt 1.txt 2.txt 3.txt 4.txt 5.txt 6.txt 7.txt 8.txt 9.txt 10.txt 11.txt 12.txt 13.txt  > spider.fpkm.txt 
    
    
    
    cat spider.fpkm.txt | awk '{print $1 "\t" int($2+0.5) "\t" int($3+0.5) "\t" int($4+0.5) "\t" int($5+0.5) "\t" int($6+0.5) "\t" int($7+0.5) "\t" int($8+0.5) "\t" int($9+0.5) "\t" int($10+0.5) \
    "\t" int($11+0.5) "\t" int($12+0.5) "\t" int($13+0.5) "\t" int($14+0.5) "\t" int($15+0.5)}' > spider.effcounts
    
    cat spider.effcounts | sed '1 i\names 28W 9W 10L 7L 67L 51L 110L 96L 39W 48W 55WL 73L 83L 89W' > spider.effcounts.txt 
    
    awk '{print $1 "\t" $2 "\t" $3 "\t" $10 "\t" $11 "\t" $15 "\t" $4 "\t" $5 "\t" $6 "\t" $7 "\t" $8 "\t" $9}' spider.effcounts.txt > final.spider.effcounts.txt
    sed -i '$ d' foo.txt
    
**edgeR**

    #edgeR
    source("http://bioconductor.org/biocLite.R")
    biocLite("edgeR")
    library(edgeR)
    x <- read.delim("~/Dropbox/spider.genomics/final.spider.effcounts.txt", row.names='names')
    group <- factor(c(1,1,1,1,1,2,2,2,2,2,2))
    y <- DGEList(counts=x, group=group)
    keep <- rowSums(cpm(y) > 10) >= 2
    y <- y[keep,]
    dim(y)
    y <- calcNormFactors(y)
    y <- estimateCommonDisp(y)
    y <- estimateTagwiseDisp(y)
    et <- exactTest(y)
    summary(de <- decideTestsDGE(et, p=0.05, adjust="BH"))
	topTags(et, n=205)
	
	detags <- rownames(y)[as.logical(de)]
	plotSmear(et, de.tags=detags)


**Annotation**

in `~/spider/blast`

	TransDecoder -t ec.C50.P2.Trin.highexp.spider.fasta --CPU 60 /home/macmanes/cpg_project/prot/Pfam-A.hmm
	
<<<<<<< HEAD
=======


**Trinity style annotation**

	/share/trinityrnaseq_r20140717/util/abundance_estimates_to_matrix.pl \
	--est_method eXpress --name_sample_by_basedir \
	28W_paired.xprs/results.xprs \
	9W.xprs/results.xprs \
	39_single.xprs/results.xprs \
	48_single.xprs/results.xprs \
	89_single.xprs/results.xprs \
	10L_paired.xprs/results.xprs \
	7L_paired.xprs/results.xprs \
	67L_paired.xprs/results.xprs \
	51L_paired.xprs/results.xprs \
	110L_single.xprs/results.xprs \
	96L_single.xprs/results.xprs
	

	/share/trinityrnaseq_r20140717/Analysis/DifferentialExpression/run_DE_analysis.pl \
	--matrix matrix.counts.matrix --method DESeq \
	--samples_file samples_described.txt
	
in `/home/macmanes/spider/diffexp/DESeq.14921.dir`
>>>>>>> FETCH_HEAD

	/share/trinityrnaseq_r20140717/Analysis/DifferentialExpression/analyze_diff_expr.pl \
	--matrix ../matrix.TMM.fpkm.matrix -P 1e-2 -C 2 --samples ../samples_described.txt

<<<<<<< HEAD
**Trinity style annotation**

	/share/trinityrnaseq_r20140717/util/abundance_estimates_to_matrix.pl \
	--est_method eXpress --name_sample_by_basedir \
	28W_paired.xprs/results.xprs \
	9W.xprs/results.xprs \
	39_single.xprs/results.xprs \
	48_single.xprs/results.xprs \
	89_single.xprs/results.xprs \
	10L_paired.xprs/results.xprs \
	7L_paired.xprs/results.xprs \
	67L_paired.xprs/results.xprs \
	51L_paired.xprs/results.xprs \
	110L_single.xprs/results.xprs \
	96L_single.xprs/results.xprs
	

	/share/trinityrnaseq_r20140717/Analysis/DifferentialExpression/run_DE_analysis.pl \
	--matrix matrix.counts.matrix --method DESeq \
	--samples_file samples_described.txt
	
in `/home/macmanes/spider/diffexp/DESeq.14921.dir`

	/share/trinityrnaseq_r20140717/Analysis/DifferentialExpression/analyze_diff_expr.pl \
	--matrix ../matrix.TMM.fpkm.matrix -P 1e-2 -C 2 --samples ../samples_described.txt

	---
	
	/share/trinityrnaseq_r20140717/Analysis/DifferentialExpression/define_clusters_by_cutting_tree.pl \
	-R diffExpr.P1e-2_C2.matrix.RData -K 10
	
>>>>>>> FETCH_HEAD

There are lost of BS diff expression hits (+ a few good ones), maybe i need to think about how better to filter the assembly. 
--

**download invert refseq and blast**

	wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/invertebrate/invertebrate.*.rna.fna.gz
	gzip -d
	gzip -cd complete*gz | makeblastdb -dbtype prot -title refseq -out refseq -in -
	
	blastx -db refseq/refseq -query ec.C50.P2.Trin.fasta -outfmt 6 \
	-evalue 1e-5 -num_threads 60 -out spider.blastx
	

tool every contig that has a conserved coding domain + things that blast to inverts. 

in `/home/macmanes/spider/refined`

	split -l 2000 final.list

    for i in `cat xaa`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa1; done &
    for i in `cat xab`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa2; done &
    for i in `cat xac`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa3; done &
    for i in `cat xad`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa4; done &
    for i in `cat xae`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa5; done &
    for i in `cat xaf`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa6; done &
    for i in `cat xag`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa7; done &
    for i in `cat xah`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa8; done &
    for i in `cat xai`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa9; done &
    for i in `cat xaj`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa11; done &
    for i in `cat xak`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa10; done &
    for i in `cat xal`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa12; done &
    for i in `cat xam`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa13; done &
    for i in `cat xan`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa14; done &
    for i in `cat xao`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa15; done &
    for i in `cat xap`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa16; done &
    for i in `cat xaq`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa17; done &
    

	cat ec.C50.P2.Trin.highexp.spider* > ec.C50.P2.Trin.highexp.blasted.spider.fasta

**mapping**

	cp /mnt/data3/macmanes/121114_HS3B_elias_spider/raw.reads/MDM* . &
	bwa index -p index ec.C50.P2.Trin.highexp.blasted.spider.fasta

    bwa mem -t60 index  MDM_SPIDER_10L_1.fq.gz MDM_SPIDER_10L_2.fq.gz | express -p 30 -o 10L_paired ec.C50.P2.Trin.highexp.blasted.spider.fasta
    
    rm MDM_SPIDER_10L_1.fq.gz MDM_SPIDER_10L_2.fq.gz
    bwa mem -t60 index  MDM_SPIDER_7L_1.fq.gz MDM_SPIDER_7L_2.fq.gz | express -p 30 -o  7L_paired ec.C50.P2.Trin.highexp.blasted.spider.fasta
    
    rm MDM_SPIDER_7L_1.fq.gz MDM_SPIDER_7L_2.fq.gz
    bwa mem -t60 index  MDM_SPIDER_67L_1.fq.gz MDM_SPIDER_67L_2.fq.gz | express -p 30 -o  67L_paired ec.C50.P2.Trin.highexp.blasted.spider.fasta
    
    rm MDM_SPIDER_67L_1.fq.gz MDM_SPIDER_67L_2.fq.gz
    bwa mem -t60 index  MDM_SPIDER_28W_1.fq.gz MDM_SPIDER_28W_2.fq.gz | express -p 30 -o  28W_paired ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm MDM_SPIDER_28W_1.fq.gz MDM_SPIDER_28W_2.fq.gz
    #done
    
    bwa mem -t60 index  MDM_SPIDER_51L_1.fq.gz MDM_SPIDER_51L_2.fq.gz | express -p 30 -o  51L_paired ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm MDM_SPIDER_51L_1.fq.gz MDM_SPIDER_51L_2.fq.gz
    
    bwa mem -t60 index  spider110L.fq.gz | express -p 30 -o  110L_single ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm spider110L.fq.gz
    
    bwa mem -t60 index  spider39.fq.gz | express -p 30 -o  39_single ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm spider39.fq.gz
    
    bwa mem -t60 index  spider48.fq.gz | express -p 30 -o  48_single ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm spider48.fq.gz
    
    bwa mem -t60 index  spider55.fq.gz | express -p 30 -o  55_single ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm spider55.fq.gz
    
    bwa mem -t60 index  spider73.fq.gz | express -p 30 -o  73_single ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm spider73.fq.gz
    
    bwa mem -t60 index  spider83.fq.gz | express -p 30 -o  83_single ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm spider83.fq.gz
    
    bwa mem -t60 index  spider89.fq.gz | express -p 30 -o  89_single ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm spider89.fq.gz
    
    bwa mem -t60 index  spider96L.fq.gz | express -p 30 -o  96L_single ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm spider96L.fq.gz
    
    bwa mem -t60 index  spider9W.fq.gz | express -p 30 -o  9W_single ec.C50.P2.Trin.highexp.blasted.spider.fasta
    rm spider9W.fq.gz
    

Need to do some recapping on the filtering stuff
--

1. 1st pass was to filter based on expression and coding regions. Things that were expressed over TMP>1 and looked like they were coding were kept. The issue is that there is a low ot low complexxity contigs that ended up in the dataset --> bad.

2. Then I did some filtering based on Pfam hits + searching Refseq invert database. This ws fine (33k contigs, so pretty small), but in looking around I saw that this secretin contig that showed up as differentially expressed had been filtered out as there was no conserved coding domain. It hit a protein in RefSeq that was not in the invert collection. 

3. What I am doing right now, is to blast against the complete protein RefSeq - this is taking a long time, given the large database and blastX search. It is recovering new things, not included in the last dataset, so I think this is worth doing, even if it is slow...

 So, once blastx is done, I will: 


Extract out hits that are uniq, and pull down the contigs.


	awk '{print $1}' spider.blastx | sort | uniq > blast.list
	diff blast.list list.final | grep '<' | awk '{print $2}' > diff.list
	split -l 2000 diff.list
	
	#pull down contigs. 
	#mapping and express
	#Trinity style diff expression. 
    
=======
	---
	
	/share/trinityrnaseq_r20140717/Analysis/DifferentialExpression/define_clusters_by_cutting_tree.pl \
	-R diffExpr.P1e-2_C2.matrix.RData -K 10
	

There are lost of BS diff expression hits (+ a few good ones), maybe i need to think about how better to filter the assembly. 
--

**download invert refseq and blast**

	wget ftp://ftp.ncbi.nlm.nih.gov/refseq/release/invertebrate/invertebrate.*.rna.fna.gz
	gzip -d
	gzip -cd complete*gz | makeblastdb -dbtype prot -title refseq -out refseq -in -
	
	blastx -db refseq/refseq -query ec.C50.P2.Trin.fasta -outfmt 6 \
	-evalue 1e-5 -num_threads 60 -out spider.blastx
	

tool every contig that has a conserved coding domain + things that blast to inverts. 

in `/home/macmanes/spider/refined`

	split -l 2000 final.list

    for i in `cat xaa`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa1; done &
    for i in `cat xab`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa2; done &
    for i in `cat xac`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa3; done &
    for i in `cat xad`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa4; done &
    for i in `cat xae`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa5; done &
    for i in `cat xaf`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa6; done &
    for i in `cat xag`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa7; done &
    for i in `cat xah`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa8; done &
    for i in `cat xai`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa9; done &
    for i in `cat xaj`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa11; done &
    for i in `cat xak`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa10; done &
    for i in `cat xal`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa12; done &
    for i in `cat xam`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa13; done &
    for i in `cat xan`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa14; done &
    for i in `cat xao`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa15; done &
    for i in `cat xap`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa16; done &
    for i in `cat xaq`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa17; done &
    

	cat ec.C50.P2.Trin.highexp.spider* > ec.C50.P2.Trin.highexp.blasted.spider.fasta

**mapping**

	cp /mnt/data3/macmanes/121114_HS3B_elias_spider/raw.reads/MDM* . &
	bwa index -p index ec.C50.P2.Trin.highexp.blasted.spider.fasta

    bwa mem -t25 index  ../MDM_SPIDER_10L_1.fq.gz ../MDM_SPIDER_10L_2.fq.gz | express -p 30 -o 10L_paired ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../MDM_SPIDER_7L_1.fq.gz ../MDM_SPIDER_7L_2.fq.gz | express -p 30 -o  7L_paired ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../MDM_SPIDER_67L_1.fq.gz ../MDM_SPIDER_67L_2.fq.gz | express -p 30 -o  67L_paired ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../MDM_SPIDER_28W_1.fq.gz ../MDM_SPIDER_28W_2.fq.gz | express -p 30 -o  28W_paired ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../MDM_SPIDER_51L_1.fq.gz ../MDM_SPIDER_51L_2.fq.gz | express -p 30 -o  51L_paired ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../spider110L.fq.gz | express -p 30 -o  110L_single ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../spider39.fq.gz | express -p 30 -o  39_single ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../spider48.fq.gz | express -p 30 -o  48_single ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../spider55.fq.gz | express -p 30 -o  55_single ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../spider73.fq.gz | express -p 30 -o  73_single ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../spider83.fq.gz | express -p 30 -o  83_single ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../spider89.fq.gz | express -p 30 -o  89_single ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../spider96L.fq.gz | express -p 30 -o  96L_single ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
    bwa mem -t25 index  ../spider9W.fq.gz | express -p 30 -o  9W_single ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
    
	ls
    

Need to do some recapping on the filtering stuff
--

1. 1st pass was to filter based on expression and coding regions. Things that were expressed over TMP>1 and looked like they were coding were kept. The issue is that there is a low ot low complexity contigs that ended up in the dataset --> bad.

2. Then I did some filtering based on Pfam hits + searching Refseq invert database. This ws fine (33k contigs, so pretty small), but in looking around I saw that this secretin contig that showed up as differentially expressed had been filtered out as there was no conserved coding domain. It hit a protein in RefSeq that was not in the invert collection. 

3. What I am doing right now, is to blast against the complete protein RefSeq - this is taking a long time, given the large database and blastX search. It is recovering new things, not included in the last dataset, so I think this is worth doing, even if it is slow...

 So, once blastx is done, I will: 


Extract out hits that are uniq, and pull down the contigs.


	awk '{print $1}' spider.blastx | sort | uniq | diff - list.final | grep '<' | awk '{print $2}' | wc -l
	split -l 2000 diff.list
	
	#pull down contigs. 
	#mapping and express
	#Trinity style diff expression. 
    

I have been blasting for 5 days, and am 50% done. I decided to stop the blast and use what I hafe thus far, then restart when I am ready. I stopped blasting at contig `c94840_g1_i1` which is line `184317`

This is the file that contains the good contigs + the contigs from the 1st set of refseq blast hits. 

	ec.C50.P2.Trin.highexp.spider.fa19 ec.C50.P2.Trin.highexp.blasted.spider.fasta > ec.C50.P2.Trin.highexp.blasted.first.refseq.spider.fasta
	cd-hit-est -M 5000 -T 24 -c .97 -i ec.C50.P2.Trin.highexp.blasted.first.refseq.spider.fasta \
	-o ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta
	
When I restart blast, I need to use a modified quert file in `$HOME/spider/refined`

	sed '1,184318d' ec.C50.P2.Trin.fasta

restarted blast Thursday AM. wen done, need to do this:

	awk '{print $1}' spider.blastx | sort | uniq | diff - list.final | grep '<' | awk '{print $2}' > diff.list
	
	for i in `cat diff.list`; do  grep --max-count=1 -A1 -w $i ec.C50.P2.Trin.fasta >> ec.C50.P2.Trin.highexp.spider.fa1; done &
	
	cat ec.C50.P2.Trin.highexp.spider.fa1 ec.C50.P2.Trin.highexp.blasted.first.refseq.cdhit.spider.fasta \
	> ec.C50.P2.Trin.highexp.blasted.second.refseq.spider.fasta
	
	cd-hit-est -M 5000 -T 24 -c .97 -i ec.C50.P2.Trin.highexp.blasted.second.refseq.spider.fasta \
	-o ec.C50.P2.Trin.highexp.blasted.second.refseq.cdhit.spider.fasta
	




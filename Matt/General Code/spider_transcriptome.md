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
    

**mapping for diff expression**

	cp /mnt/data3/macmanes/121114_HS3B_elias_spider/raw.reads/MDM* . &
	bwa index -p index ec.C50.P2.Trin.highexp.spider.fasta

	#done	
	bwa mem -t60 index  MDM_SPIDER_10L_1.fq.gz MDM_SPIDER_10L_2.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 10L_paired
	
	rm MDM_SPIDER_10L_1.fq.gz MDM_SPIDER_10L_2.fq.gz
	bwa mem -t60 index  MDM_SPIDER_7L_1.fq.gz MDM_SPIDER_7L_2.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 7L_paired

	rm MDM_SPIDER_7L_1.fq.gz MDM_SPIDER_7L_2.fq.gz
	bwa mem -t60 index  MDM_SPIDER_67L_1.fq.gz MDM_SPIDER_67L_2.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 67L_paired

	rm MDM_SPIDER_67L_1.fq.gz MDM_SPIDER_67L_2.fq.gz
	bwa mem -t60 index  MDM_SPIDER_28W_1.fq.gz MDM_SPIDER_28W_2.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 28W_paired
	rm MDM_SPIDER_28W_1.fq.gz MDM_SPIDER_28W_2.fq.gz
	#done
	
	bwa mem -t60 index  MDM_SPIDER_51L_1.fq.gz MDM_SPIDER_51L_2.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 51L_paired
	rm MDM_SPIDER_51L_1.fq.gz MDM_SPIDER_51L_2.fq.gz
	
	bwa mem -t60 index  spider110L.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 110L_single
	rm spider110L.fq.gz
	
	bwa mem -t60 index  spider39.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 39_single
	rm spider39.fq.gz

	bwa mem -t60 index  spider48.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 48_single
	rm spider48.fq.gz

	bwa mem -t60 index  spider55.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 55_single
	rm spider55.fq.gz

	bwa mem -t60 index  spider73.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 73_single
	rm spider73.fq.gz

	bwa mem -t60 index  spider83.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 83_single
	rm spider83.fq.gz

	bwa mem -t60 index  spider89.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 89_single
	rm spider89.fq.gz

	bwa mem -t60 index  spider96L.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 96L_single
	rm spider96L.fq.gz

	bwa mem -t60 index  spider9W.fq.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - 9W_single
	rm spider9W.fq.gz
	
	ls





	
	
	
	
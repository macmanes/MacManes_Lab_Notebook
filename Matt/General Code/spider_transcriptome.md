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
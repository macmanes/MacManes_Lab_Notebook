starling transcriptome
--

    Trinity --seqType fq \
    --JM 100G --trimmomatic \
    --bflyHeapSpaceMax 10G \
    --inchworm_cpu 10 \
    --SS_lib_type RF \
    --normalize_reads \
    --left Sample_SS15_L_001_002_R1.fastq \
    --right Sample_SS15_L_001_002_R2.fastq \
    --CPU 32 \
    --output starling_SS_norm \
    --group_pairs_distance 999 \
    --quality_trimming_params "ILLUMINACLIP:/share/trinityrnaseq_r20140717/trinity-plugins/Trimmomatic/adapters/TruSeq3-PE.fa:2:40:15 \
    LEADING:2 TRAILING:2 MINLEN:25" > starling_SS_norm.log
    

stats
--

    macmanes@davinci:/mouse/starling/blast$ abyss-fac ../rnaseq/starling_SS_norm/Trinity.fasta
    
    n	n:500	n:N50	min	N80	N50	N20	E-size	max	sum	name
    824415	372543	90813	500	830	1579 3084	2145	27713	488.8e6	../rnaseq/starling_SS_norm/Trinity.fasta


blastdb
--

	ftp://climb.genomics.cn/pub/10.5524/100001_101000/100005/phylogeny_study_update/Aptenodytes_forsteri.cds.gz
	ftp://climb.genomics.cn/pub/10.5524/101001_102000/101029/Merops_nubicus.cds.gz
	ftp://climb.genomics.cn/pub/10.5524/101001_102000/101022/Chlamydotis_macqueenii.cds.gz
	ftp://climb.genomics.cn/pub/10.5524/101001_102000/101020/Cariama_cristata.cds.gz
	ftp://climb.genomics.cn/pub/10.5524/101001_102000/101018/Buceros_rhinoceros.cds.gz
	ftp://climb.genomics.cn/pub/10.5524/101001_102000/101017/Balearica_regulorum.cds.gz
	ftp://climb.genomics.cn/pub/10.5524/101001_102000/101016/Apaloderma_vittatum.cds.gz
	ftp://climb.genomics.cn/pub/10.5524/101001_102000/101003/Nipponia_nippon.cds.gz
	ftp://climb.genomics.cn/pub/10.5524/101001_102000/101038/Tauraco_erythrolophus.cds.gz
	ftp://climb.genomics.cn/pub/10.5524/101001_102000/101037/Pterocles_gutturalis.cds.gz
	ftp://ftp.ensembl.org/pub/release-77/fasta/gallus_gallus/cdna/Gallus_gallus.Galgal4.cdna.abinitio.fa.gz
	ftp://ftp.ensembl.org/pub/release-77/fasta/gallus_gallus/ncrna/Gallus_gallus.Galgal4.ncrna.fa.gz
	ftp://ftp.ensembl.org/pub/release-77/fasta/anas_platyrhynchos/cdna/Anas_platyrhynchos.BGI_duck_1.0.cdna.abinitio.fa.gz
	ftp://ftp.ensembl.org/pub/release-77/fasta/anas_platyrhynchos/ncrna/Anas_platyrhynchos.BGI_duck_1.0.ncrna.fa.gz
	ftp://ftp.ensembl.org/pub/release-77/fasta/meleagris_gallopavo/cdna/Meleagris_gallopavo.UMD2.cdna.abinitio.fa.gz
	ftp://ftp.ensembl.org/pub/release-77/fasta/meleagris_gallopavo/ncrna/Meleagris_gallopavo.UMD2.ncrna.fa.gz
	ftp://ftp.ensembl.org/pub/release-77/fasta/taeniopygia_guttata/cdna/Taeniopygia_guttata.taeGut3.2.4.cdna.abinitio.fa.gz
	ftp://ftp.ensembl.org/pub/release-77/fasta/taeniopygia_guttata/ncrna/Taeniopygia_guttata.taeGut3.2.4.ncrna.fa.gz
	
blastn
--

	blastn -db bird -query ../rnaseq/starling_SS_norm/Trinity.fasta \
	-outfmt 6 -evalue 1e-3 -num_threads 50 -out bird.blast
	

format trinity.fasta
--

	sed ':begin;$!N;/[ACTGNn-]\n[ACTGNn-]/s/\n//;tbegin;P;D' ../rnaseq/starling_SS_norm/Trinity.fasta > format.Trinity.fa


Transdecoder 
--

	TransDecoder -t format.Trinity.fa
	grep '>' Trinity.fasta.transdecoder.pep | awk '{print $1}' | sed 's_>__g' > transd.list
	cat *domtbl > ../starling.pfam
	awk '{print $4}' starling.pfam | sed '1,3d' | awk -F '|' '{print $1}' > pfam.list

	
Extract out contigs
--

	for i in `cat xaa`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa1; done &
	for i in `cat xab`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa2; done &
	for i in `cat xac`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa3; done &
	for i in `cat xad`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa4; done &
	for i in `cat xae`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa5; done &
	for i in `cat xaf`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa6; done &
	for i in `cat xag`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa7; done &
	for i in `cat xah`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa8; done &
	for i in `cat xai`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa9; done &
	for i in `cat xaj`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa10; done &
	for i in `cat xak`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa11; done &
	for i in `cat xal`; do  grep --max-count=1 -A1 -w $i format.Trinity.fa >> starling.Trinity.fa12; done &	
	cat starling.Trinity.fa* > starling.Trinity.fa

cd-hit
--

	cd-hit-est -M 5000 -T 24 -c .97 -i starling.Trinity.fa \
	-o starling.Trinity.cdhit.fa
	

bwa
--

	bwa index -p starling.cdhit ../cdhit/starling.Trinity.cdhit.fa
	bwa mem -t40 starling.cdhit  \
	../rnaseq/starling_SS_norm/Sample_SS15_L_001_002_R1.fastq.P.qtrim.gz \
	../rnaseq/starling_SS_norm/Sample_SS15_L_001_002_R2.fastq.P.qtrim.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@18 - starling
	
eXpress
--

	express -p 40 --rf-stranded ../cdhit/starling.Trinity.cdhit.fa starling.bam
	
filter based on tpm
--

	awk '1>$15{next}1' results.xprs  | awk '{print $2}' | sed '1,1d' > express.list
	split 10000 express.list
	
	for i in `cat xaa`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa1; done &
	for i in `cat xab`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa2; done &
	for i in `cat xac`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa3; done &
	for i in `cat xad`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa4; done &
	for i in `cat xae`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa5; done &
	for i in `cat xaf`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa6; done &
	for i in `cat xag`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa7; done &
	for i in `cat xah`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa8; done &
	for i in `cat xai`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa9; done &
	for i in `cat xaj`; do  grep --max-count=1 -A1 -w $i ../cdhit/starling.Trinity.cdhit.fa >> highexp.starling.fa10; done &
	cat highexp.starling.fa* > highexp.starling.fa


mapping high exp dataset
--

	bwa index -p highexp highexp.starling.fa
	
	bwa mem -t60 highexp  \
	../rnaseq/starling_SS_norm/Sample_SS15_L_001_002_R1.fastq.P.qtrim.gz \
	../rnaseq/starling_SS_norm/Sample_SS15_L_001_002_R2.fastq.P.qtrim.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - highexp.starling
	

eXpress on final dataset
--

	express -p 40 --rf-stranded highexp.starling.fa highexp.starling.bam
	
final stats
--
abyss-fac highexp.starling.fa
n	n:500	n:N50	min	N80	N50	N20	E-size	max	sum	name
96724	76262	18718	500	1230	2291	4098	2895	27713	138.1e6	highexp.starling.fa



Starling STAR mapping
--

	STAR --genomeDir genome --runMode genomeGenerate --genomeFastaFiles ../pbjelly/run/jelly.out.fasta \
	--runThreadN 60 --limitGenomeGenerateRAM 100000000000  
	
	STAR --genomeDir genome --readFilesIn \
	<(gzip -cd ../../rnaseq/starling_SS_norm/Sample_SS15_L_001_002_R1.fastq.P.qtrim.gz) \
	<(gzip -cd ../../rnaseq/starling_SS_norm/Sample_SS15_L_001_002_R2.fastq.P.qtrim.gz) \
	--runThreadN 60 --outFilterIntronMotifs RemoveNoncanonical --outFileNamePrefix SS15  


Starling bwa

	bwa mem -t60 index  \
	../../rnaseq/starling_SS_norm/Sample_SS15_L_001_002_R1.fastq.P.qtrim.gz \
	../../rnaseq/starling_SS_norm/Sample_SS15_L_001_002_R2.fastq.P.qtrim.gz | \
	samtools view -@16 -Sub - | samtools sort -n -m3G -@28 - starling.rnaseq
	























	

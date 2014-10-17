Error Correction
--

brain

	bless -prefix brain -kmerlength 25 -verify \
	-read1 Pero360B.1.fastq.gz \
	-read2 Pero360B.2.fastq.gz 

liver

	bless -prefix liver -kmerlength 25 -verify \
	-read1 Pero360L.1.fastq.gz \
	-read2 Pero360L.2.fastq.gz 

kidney

	bless -prefix kidney -kmerlength 25 -verify \
	-read1 Pero360K.1.fastq.gz \
	-read2 Pero360K.2.fastq.gz 

testes

	bless -prefix testes -kmerlength 25 -verify \
	-read1 Pero360T.1.fastq.gz \
	-read2 Pero360T.2.fastq.gz 


Trinity assemblies
--

>Brain Assembly

    nohup Trinity --seqType fq --JM 50G \
    --trimmomatic --SS_lib_type RF --group_pairs_distance 999 \
    --left /mnt/data3/macmanes/pero_annotation/corrected/Pero360B_corr.1.corrected.fastq  \
    --right /mnt/data3/macmanes/pero_annotation/corrected/Pero360B_corr.2.corrected.fastq \
    --CPU 24 --output brainSS --bflyGCThreads 32 --inchworm_cpu 10 \
    --quality_trimming_params "ILLUMINACLIP:/mnt/data3/macmanes/subsamp/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25" &

>Mapping Brain reads to brain assembly and calculating expression
	
	bwa index -p brain brainSS/Trinity.fasta
    bwa mem -t 32 brain \
    /mnt/data3/macmanes/pero_annotation/corrected/Pero360B_corr.1.corrected.fastq \
    /mnt/data3/macmanes/pero_annotation/corrected/Pero360B_corr.2.corrected.fastq  \
    | samtools view -@6 -Sub - | express --rf-stranded -p 24 brain.final.fasta
    



> Testes Assembly

    nohup Trinity --seqType fq --JM 50G \
    --trimmomatic --SS_lib_type RF --group_pairs_distance 999 \
    --left /mnt/data3/macmanes/pero_annotation/corrected/Pero360T_corr.1.corrected.fastq  \
    --right /mnt/data3/macmanes/pero_annotation/corrected/Pero360T_corr.2.corrected.fastq \
    --CPU 24 --output testesSS --bflyGCThreads 32 --inchworm_cpu 10 \
    --quality_trimming_params "ILLUMINACLIP:/mnt/data3/macmanes/subsamp/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25" &

>Mapping testes reads to testes assembly and calculating expression
    
    bwa index -p testesSS testesSS/Trinity.fasta
    bwa mem -t 8 testesSS \
    /mnt/data3/macmanes/pero_annotation/corrected/Pero360T_corr.1.corrected.fastq \
    /mnt/data3/macmanes/pero_annotation/corrected/Pero360T_corr.2.corrected.fastq  | samtools view -@6 -Sub - > testes.bam
    
    express --rf-stranded -o testesSS -p 8 testesSS/Trinity.fasta testes.bam
 
> Liver Assembly

    nohup Trinity --seqType fq --JM 50G \
    --trimmomatic --SS_lib_type RF --group_pairs_distance 999 \
    --left /mnt/data3/macmanes/pero_annotation/corrected/Pero360L_corr.1.corrected.fastq  \
    --right /mnt/data3/macmanes/pero_annotation/corrected/Pero360L_corr.2.corrected.fastq \
    --CPU 24 --output liver --bflyGCThreads 32 --inchworm_cpu 10 \
    --quality_trimming_params "ILLUMINACLIP:/mnt/data3/macmanes/subsamp/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25" &
    
>Mapping liver reads to liver assembly and calculating expression



    bwa index -p liverSS liverSS/Trinity.fasta
    bwa mem -t 8 liverSS \
    /mnt/data3/macmanes/pero_annotation/corrected/Pero360L_corr.1.corrected.fastq \
    /mnt/data3/macmanes/pero_annotation/corrected/Pero360L_corr.2.corrected.fastq  \
    | samtools view -@6 -Sub - > liverSS.bam
    express --rf-stranded -o liverSS -p 8 liver/Trinity.fasta liverSS.bam



> Kidney Assembly

    nohup Trinity --seqType fq --JM 50G \
    --trimmomatic --SS_lib_type RF --group_pairs_distance 999 \
    --left /mnt/data3/macmanes/pero_annotation/corrected/Pero360K_corr.1.corrected.fastq  \
    --right /mnt/data3/macmanes/pero_annotation/corrected/Pero360K_corr.2.corrected.fastq \
    --CPU 24 --output kidneySS --bflyGCThreads 32 --inchworm_cpu 10 \
    --quality_trimming_params "ILLUMINACLIP:/mnt/data3/macmanes/subsamp/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25" &


>Mapping kidney reads to kidney assembly and calculating expression



    bwa index -p kidneySS kidneySS/Trinity.fasta
    bwa mem -t 8 kidneySS \
    /mnt/data3/macmanes/pero_annotation/corrected/Pero360K_corr.1.corrected.fastq \
    /mnt/data3/macmanes/pero_annotation/corrected/Pero360K_corr.2.corrected.fastq  \
    | samtools view -@6 -Sub - > kidneySS.bam
    express --rf-stranded -o kidneySS -p 8 kidneySS/Trinity.fasta kidneySS.bam

BLASTing
---
      
> BLAST brain assembly (the others were done identically, but with the other assemblies)
	
	cat *fa | makeblastdb -dbtype nucl -out blast -title mouse_pema

    blastn -query brain.Trinity.fasta -db blast \
    -evalue 1e-10 -num_threads 15 -outfmt \
    "6 qseqid sacc pident length evalue" > brain.blast &

> Extract out Trinity contigs ID's that match.
    
    cat brain.blast | awk '{print $1}' | sort | uniq > brain.list

> Make unwrapped FASTA file
    
    sed -i ':begin;$!N;/[ACTGNn-]\n[ACTGNn-]/s/\n//;tbegin;P;D' brain.Trinity.fasta.tmp

> Extract out the matches
    
    for i in `cat brain.list`; do  grep --max-count=1 -A1 -w $i \
    brain.Trinity.fasta.tmp >> brain.final.fasta; done

> Simplify headers and rename file name.

    cat testes.final.fasta | awk '{print $1}' > testes.fasta    
    mv testes.fasta testes.final.fasta

CD-HIT-EST
--

> on concatenated dataset (filtered brain/testes/liver/kidney)

	cd-hit-est -M 5000 -T 30 -c .95 -i concat.Trin.fasta -o Pero.BLTK.fasta
	
TransDecoder
---

	TransDecoder -S -cpu 30 -t Pero.BLTK.fasta


HMMER3/Pfam
---

	hmmscan --cpu 48 --domtblout pero.pfam \
	/home/macmanes/cpg_project/prot/Pfam-A.hmm \
	../transdecoder/keep.fasta.transdecoder.pep






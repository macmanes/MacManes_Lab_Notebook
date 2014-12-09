Feeding
--

	svn checkout svn://svn.code.sf.net/p/trinityrnaseq/code/trunk trinityrnaseq-code
	...
	Checked out revision 3991
	make -j8
	
in `/mouse/feeding/`

    ./assembly.mk --dry-run
    Trinity --seqType fq --JM 50G --trimmomatic \
        --left /mouse/feeding/20M_corr/20M_corrk19.1.corrected.fastq.gz  \
        --right /mouse/feeding/20M_corr/20M_corrk19.2.corrected.fastq.gz \
        --CPU 32 --output 20M.ec.P2 \
        --quality_trimming_params "ILLUMINACLIP:/mouse/feeding/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25"
    Trinity --seqType fq --JM 50G --trimmomatic \
        --left /mouse/feeding/100M_corr/100M_corrk19.1.corrected.fastq.gz  \
        --right /mouse/feeding/100M_corr/100M_corrk19.2.corrected.fastq.gz \
        --CPU 32 --output 100M.ec.P2 \
        --quality_trimming_params "ILLUMINACLIP:/mouse/feeding/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25"
    Trinity --seqType fq --JM 50G --trimmomatic \
        --single /mouse/feeding/20M_corr/20M.corr.inter.norm.fastQ.gz \
        --run_as_paired \
        --CPU 32 --output 20M.ec.P2.C50 \
        --quality_trimming_params "ILLUMINACLIP:/mouse/feeding/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25"
    Trinity --seqType fq --JM 50G --trimmomatic \
        --single /mouse/feeding/100M_corr/100M.corr.inter.norm.fastQ.gz \
        --run_as_paired \
        --CPU 32 --output 100M.ec.P2.C50 \
        --quality_trimming_params "ILLUMINACLIP:/mouse/feeding/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25"

>Transrate

in `/mouse/feeding/transrate`

	transrate -a ../20M.ec.P2/Trinity.fasta -r ../Mus_musculus.GRCm38.pep.abinitio.fa -l ../SRR797058_1.fastq.gz -i ../SRR797058_2.fastq.gz -o 20M.ec.P2 -t 40	
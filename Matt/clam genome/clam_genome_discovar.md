Clam genome
--

Discovar make BAM

	java -jar /share/picard-tools-1.121/FastqToSam.jar \
	FASTQ=clam_trim_1P \
	FASTQ2=clam_trim_2P \
	OUTPUT=clam.bam \
	SAMPLE_NAME=Mya_genome TMP_DIR=/mouse
	

Discovar assembly in `/mouse/clam` started 10/8 at 0600

	DiscovarExp READS=clam.bam OUT_DIR=disc_assembly
	
Maybe I should try SPAdes? Shoudld first normalize:


	interleave-reads.py clam_trim_1P.gz clam_trim_2P.gz -o paired.fq.gz


	normalize-by-median.py -p -k 20 -C 50 -N 4 -x 15e9 \
	--savetable normC50k20.kh paired.fq


Spades

	spades.py -t 30 -m 350  --careful \
	--12 norm1.fq \
	-o clam_SPAdes
	


	interleave-reads.py clam_trim_1P.gz clam_trim_2P.gz -o paired.fq.gz | \
	normalize-by-median.py -p -k 20 -C 50 -N 4 -x 15e9 \
	--savetable normC50k20.kh /dev/stdin

SPAdes wont work, more than 2 bullion characters

Lets try SGA

	
    sga preprocess --pe-mode=2 -o sga_preproc.fq paired.clam.fq
    sga index -t 60 -a ropebwt --no-reverse sga_preproc.fq
    sga correct -k 31 --discard -r 2 --learn -t 60 -d 32 -o reads.ec.k31.fastq sga_preproc.fq
    sga index -a ropebwt -t 60 reads.ec.k31.fastq
    sga filter -d 32 -x 2 -t 60 --low-complexity-check reads.ec.k31.fastq
<<<<<<< HEAD
    sga fm-merge -m 45 -t 60 -o merged.k31.fa reads.ec.k31.filter.pass.fa
    sga index -t 60 merged.k31.fa
=======
    sga fm-merge -m 45 -t 60 -o merged.k41.fa reads.ec.k31.filter.pass.fa
    sga index -a ropebwt -t 10 merged.k31.fa
>>>>>>> FETCH_HEAD
    sga rmdup -d 32 -t 60 merged.k31.fa
    sga overlap -e 0.04 -t 60 merged.k31.rmdup.fa
    sga assemble -b 10 -m 50 -r 10 -o assemble.m50 merged.k31.rmdup.asqg.gz
    /share/sga/src/bin/sga-align -t 60 --name=clam.align assemble.m50-contigs.fa clam_trim_1P.gz clam_trim_2P.gz
    /share/sga/src/bin/sga-bam2de.pl -n 5 --prefix libPE clam.align.refsort.bam
	/share/sga/src/bin/sga-astat.py -m 200 clam.align.refsort.bam > libPE.astat
	sga scaffold -m 200 --pe libPE.de -a libPE.astat \
	-o scaffolds.n5.scaf assemble.m75-contigs.fa
	

	sga scaffold2fasta -m 200 -a assemble.m50-graph.asqg.gz \
	-o scaffolds.n5.fa -d 1 --use-overlap --write-unplaced scaffolds.n5.scaf
	



	
Maybe I shoult try this new tool for scaffolding with RNAseq data 
--

in `/mouse/clam/scaffold`

	blat -noHead -t=DNA -q=DNA old_scaffolds.n5.fa reduced.Trin.fasta clam.psl
	$HOME/L_RNA_scaffolder/L_RNA_scaffolder.sh -d $HOME/L_RNA_scaffolder/ -i clam.psl -j old_scaffolds.n5.fa -o .
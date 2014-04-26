
This is the code for running the training module of Augustus

	~/augustus-3.0.2/scripts/autoAug.pl --genome=jelly.out.fasta --pasa --pasapolyAhints -singleCPU --cdna=augustus.complete.cds --species=peer --utr --hints=augustus.gff3 --optrounds=2

	export PASAHOME

	~/augustus-3.0.2/scripts/autoAug.pl --genome jelly.out.fasta --species peer --hints augustus.gff3 --optrounds 2 --trainingset augustus.complete.cds --singleCPU

	macmanes@macmanes:/media/macmanes/hd3/pero-genome/augustus$ ~/augustus-3.0.2/scripts/autoAug.pl --genome jelly.out.fasta --pasa --pasapolyAhints -singleCPU --cdna augustus.complete.cds --species peer --utr --hints augustus.gff3 --optrounds 2
	
This is what I really did: (in `/media/macmanes/hd3/maker/augustus`)

	~/augustus-3.0.2/scripts/autoAug.pl --genome=../../pero-genome/jelly.out.fasta --species=peer \
	--cdna=../augustus.complete.cds --trainingset=../cegma/genome.gff3 --singleCPU -v --useexisting
	
I got an error message: `Number of training genes is with 17 too low (at least 100 genes required)! Training aborted.`

> I'll have to run maker on Blacklight a little *or maybe a lot* longer...


17 Apr 14
--
take 2 (in `/media/macmanes/hd3/maker/pero.genes.maker.output`):

	~/maker/bin/gff3_merge -d pero.genes_master_datastore_index.log
	~/maker/bin/maker2zff pero.gff
	/home/macmanes/maker/exe/snap/fathom genome.ann genome.dna -categorize 1000
	/home/macmanes/maker/exe/snap/zff2gff3.pl genome.ann | perl -plne 's/\t(\S+)$/\t\.\t$1/' > for-augustus.gff3
	
nof for the actual training (in .

	~/augustus-3.0.2/scripts/autoAug.pl --genome=../../pero-genome/jelly.out.fasta --species=peer \
	--cdna=../augustus.complete.cds --trainingset=for-augustus.gff3 --singleCPU -v --useexisting


25 Apr 14
--

I killed the last run, remade the `for-augustus.gff` file, and started with slightly different command. Specifically, I lost the --singleCPU command in hopes that this will run faster. 

	nohup ~/augustus-3.0.2/scripts/autoAug.pl --genome=../../pero-genome/jelly.out.fasta --species=peer \
	--cdna=../augustus.complete.cds --trainingset=for-augustus.gff3 --noninteractive --useexisting --optrounds=1 &